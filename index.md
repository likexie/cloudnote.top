# lua语言

## 1. 注释

1. 单行注释

   ```lua
   -- print("hello world");
   ```

   

2. 多行注释

   ```lua
   --[[
   多行注释
   多行注释
   --]]
   ```

## 2. 数据类型

1. nil空类型

   ```lua
   -- 使用nil进行比较时需要加上字符串
   print(type(w)=='nil')
   -- 使用nil 置为空
   tab1 = { key1 = "val1", key2 = "val2", "val3", "val4" }
   for k, v in pairs(tab1) do
     print(k .. " - " .. v)
   end
   tab1.key1 = nil
   for k, v in pairs(tab1) do
     print(k .. " - " .. v)
   end
   print(type(w)=='nil')
   print(type(type(X))=='string')
   输出：
   true
   1 - val3
   2 - val4
   key2 - val2
   key1 - val1
   1 - val3
   2 - val4
   key2 - val2
   true
   true
   ```

2. boolean

   boolean 类型只有两个可选值：true（真） 和 false（假），Lua 把 false 和 nil 看作是 false，其他的都为 true，数字 0 也是 true

   ```lua
   if 0 then
     print(123)
   end
   输出：123
   ```

   

3. number 数字

   默认只有一种number类型--double（双精度）类型(默认类型可以修改 luaconf.h 里的定义)

   ```lua
   print(type(2))
   print(type(2.2))
   print(type(0.2))
   print(type(2e+1))
   print(type(0.2e-1))
   print(type(7.8263692594256e-06))
   输出：
   number
   number
   number
   number
   number
   number
   ```

4. string(字符串)

   字符串由一对双引号或单引号来表示

   ```lua
   string1 = "this is string1"
   string2 = 'this is string2'
   ```

   也可以用2个方括号[[]] 来表示一块字符串

   ```lua
   html = [[
   <html>
   <head></head>
   <body>
       <a href="http://www.runoob.com/">菜鸟教程</a>
   </body>
   </html>
   ]]
   print(html)
   输出：
   <html>
   <head></head>
   <body>
       <a href="http://www.runoob.com/">菜鸟教程</a>
   </body>
   </html>
   ```

   在对一个数字字符串上进行算术操作时，Lua 会尝试将这个数字字符串转成一个数字:

   ```lua
   > print("2" + 6)
   8.0
   > print("2" + "6")
   8.0
   > print("2 + 6")
   2 + 6
   > print("-2e2" * "6")
   -1200.0
   > print("error" + 1)
   stdin:1: attempt to perform arithmetic on a string value
   stack traceback:
           stdin:1: in main chunk
           [C]: in ?
   >
   字符串链接使用的是..
   > print('11s'..'9')
   11s9
   计算字符串长度
   >print(#'11s')
   3
   ```

5. table(表格)

   ```lua
   -- 创建一个空的 tablelocal tbl1 = {}-- 直接初始表local tbl2 = {"apple", "pear", "orange", "grape"}
   ```

   Lua 中的表（table）其实是一个"关联数组"（associative arrays），数组的索引可以是数字或者是字符串。

   ```lua
   -- table_test.lua 脚本文件a = {}a["key"] = "value"key = 10a[key] = 22a[key] = a[key] + 11for k, v in pairs(a) do    print(k .. " : " .. v)end# 输出key : value10 : 33
   ```

   不同于其他语言的数组把 0 作为数组的初始索引，在 Lua 里表的默认初始索引一般以 1 开始。

   ```lua
   -- table_test2.lua 脚本文件local tbl = {"apple", "pear", "orange", "grape"}for key, val in pairs(tbl) do    print("Key", key)end输出：Key    1Key    2Key    3Key    4
   ```

6. function

   在 Lua 中，函数是被看作是"第一类值（First-Class Value）"，函数可以存在变量里:

   ```lua
   function factorial1(n)    if n == 0 then        return 1    else        return n*factorial1(n-1)    endend   print(factorial1(5))factorial2=factorial1print(factorial2(5))输出：120120# 匿名函数function add(a1,a2)    a2(a1)endadd(3,function(val)    print(val*19)end)
   ```

## 3. 变量

1. 变量类型

   全局变量、局部变量、表中的域

   ```lua
   -- test.lua 文件脚本a = 5               -- 全局变量local b = 5         -- 局部变量function joke()    c = 5           -- 全局变量    local d = 6     -- 局部变量endjoke()print(c,d)          --> 5 nildo    local a = 6     -- 局部变量    b = 6           -- 对局部变量重新赋值    print(a,b);     --> 6 6endprint(a,b)      --> 5 6输出结果5    nil6    65    6
   ```

2. table定义方法

   ```lua
   # 定义方法1-- table定义方法1tab1 = {    'blue',    'green',    'red'}-- print(tab1[1])-- print(tab1[2])-- print(tab1[3])--[[输出：    blue    green    red]]# 定义方法2-- table 定义方法2tab2 = {    sky='blue',    grass='green',    lava='red'}print(tab2['sky'])print(tab2['grass'])print(tab2['lava'])--[[输出：    blue    green    red]]# 定义方法3-- table 定义方法3tab3 = {    [0]=0,    [1]=1,    [6]=6}print(tab3[0])print(tab3[1])print(tab3[6])--[[输出：    0    1    6]]# 定义方法4-- table 定义方法4tab4 = {}tab4[0] =1tab4['3'] = '中国'print(tab4[0])print(tab4['3'])--[[输出：    1    中国]]
   ```


## 4. 循环语句

1. while

   ```lua
   -- 循环语句 -- while --[[swhile(condition)do   statementsend--]]print("while 循环：")i = 3while (i>0)do      print(i)    i=i-1end-- 输出--[[    3    2    1]]
   ```

2. 循环语句for

   ```lua
   -- for 循环--[[for var=exp1,exp2,exp3 do      <执行体>  end var 从 exp1 变化到 exp2，每次变化以 exp3 为步长递增 var，并执行一次 "执行体"。exp3 是可选的，如果不指定，默认为1。]]print("for 循环：")for var=1,5,21 do    print(var)end-- function f(x)      print("function")      return x*2  end  for i=1,f(5) do print(i)  end-- 打印数组a的所有值  a = {"one", "two", "three"}for i,v in ipairs(a) do    print(i,v)end-- 循环数组days = {"Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"}  for i,v in ipairs(days) do  print(v) end  
   ```

3. repeat...until 循环语句

   ```lua
   -- 循环先执行后判断i = 3repeat    print(i)    i=i-1until (i<1)
   ```

## 5. 流程控制

1. if 语句

   ```lua
   -- if语句if(0)then     print("0 is true")end
   ```

2. if else 语句

   ````lua
   --[[if(布尔表达式)then   --[ 布尔表达式为 true 时执行该语句块 --]else   --[ 布尔表达式为 false 时执行该语句块 --]end]]i = 10while i>0do     print("i 大于0",i)    if i==5    then         print('i==5跳出',i)        break    else        print('d')    end    i=i-1end
   ````

3. if elseif 语句

   ````lua
   i = 10while i>0do     print("i 大于0",i)    if i==5    then         print('i==5跳出',i)        break    elseif i==8    then        print("i==8不用跳出"..i)        print("elseif then")    else        print('d')    end    i=i-1end
   ````

## 6. 函数

1. 函数定义

   ```lua
   --[[optional_function_scope function function_name( argument1, argument2, argument3..., argumentn)    function_body    return result_params_comma_separatedendoptional_function_scope: 该参数是可选的制定函数是全局函数还是局部函数，未设置该参数默认为全局函数，如果你需要设置函数为局部函数需要使用关键字 local。function_name: 指定函数名称。argument1, argument2, argument3..., argumentn: 函数参数，多个参数以逗号隔开，函数也可以不带参数。function_body: 函数体，函数中需要执行的代码语句块。result_params_comma_separated: 函数返回值，Lua语言函数可以返回多个值，每个值以逗号隔开。]]local function sum(a,b)    return a*bendprint(sum(2,7))s,e = string.find('we are you from beijing','you')print(s,e)
   ```

## 7. 运算符

| 操作符 | 描述                                                         | 实例                                                         |
| :----- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| ==     | 等于，检测两个值是否相等，相等返回 true，否则返回 false      | (A == B) 为 false。                                          |
| ~=     | 不等于，检测两个值是否相等，不相等返回 true，否则返回 false  | (A ~= B) 为 true。                                           |
| >      | 大于，如果左边的值大于右边的值，返回 true，否则返回 false    | (A > B) 为 false。                                           |
| <      | 小于，如果左边的值大于右边的值，返回 false，否则返回 true    | (A < B) 为 true。                                            |
| >=     | 大于等于，如果左边的值大于等于右边的值，返回 true，否则返回 false | (A >= B) 返回 false。                                        |
| <=     | 小于等于， 如果左边的值小于等于右边的值，返回 true，否则返回 false | (A <= B) 返回 true。                                         |
| and    | 逻辑与操作符。 若 A 为 false，则返回 A，否则返回 B。         | (A and B) 为 false。                                         |
| or     | 逻辑或操作符。 若 A 为 true，则返回 A，否则返回 B。          | (A or B) 为 true。                                           |
| not    | 逻辑非操作符。与逻辑运算结果相反，如果条件为 true，逻辑非为 false。 | not(A and B) 为 true。                                       |
| ..     | 连接两个字符串                                               | a..b ，其中 a 为 "Hello " ， b 为 "World", 输出结果为 "Hello World"。 |
| #      | 一元运算符，返回字符串或表的长度。                           | #"Hello" 返回 5                                              |

## 8. 字符串

1. string.upper(str) 转为大写

2. string.lower(str) 转为小写

3. string.gsub(mian String, find String, replace String, num)

   ```lua
   在字符串中替换。mainString 为要操作的字符串， findString 为被替换的字符，replaceString 要替换的字符，num 替换次数（可以忽略，则全部替换），如：> string.gsub("aaaa","a","z",3);zzza    3
   ```

4. string.find(str,substr,[init,[end]])

   ```lua
   在一个指定的目标字符串中搜索指定的内容(第三个参数为索引),返回其具体位置。不存在则返回 nil。> string.find("Hello Lua user", "Lua", 1) 7    9
   ```

5. string.reverse(arg)字符串反转

6. string.format("%d",4) 格式化字符串

7. string.char(97,98,99,100) 将整型数字转成字符并连接

8. string.byte(‘asdfa’,4)指定第4个字符转换为整数

9. string.len(计算字符串长度)

10. .. 连接连个字符串

11. string.gmatch(str,pattern)

    ```lua
    > for word in string.gmatch("Hello Lua user", "%a+") do print(word) endHelloLuauser
    ```

12. string.match(str,pattern,init)

    string.match()只寻找源字串str中的第一个配对. 参数init可选, 指定搜寻过程的起点, 默认为1。
    在成功配对时, 函数将返回配对表达式中的所有捕获结果; 如果没有设置捕获标记, 则返回整个配对字符串. 当没有成功的配对时, 返回nil。

    ````lua
    > = string.match("I have 2 questions for you.", "%d+ %a+")2 questions> = string.format("%d, %q", string.match("I have 2 questions for you.", "(%d+) (%a+)"))2, "questions"
    ````

## 9. 数组

1. 一维数组

   ```lua
   -- 一维数组a = {    1,12,3,4}for i,v in ipairs(a) do     print(i,v)endfor i=0,4 do    print(a[i])end
   ```

2. 二维数组

   ```lua
   -- 二维数组array = {}for i=1,3 do    array[i] = {}    for j=4,6 do        array[i][j] = i*j    endendprint(array)for i=1,3 do    for j=4,6 do        print(array[i][j])    endend
   ```

## 10.迭代器

1. 

   






​    





















## 总结

1. 语法格式总结

   | 语句     | 使用方式             |
   | -------- | -------------------- |
   | if       | if then xxx end      |
   | for      | for  xxx do  xxx end |
   | while    | while xxx do xxx end |
   | function | function  xxx  end   |



2. ipairs和pairs的区别

   ```lua
   ipairs:遇到nil会停止pairs：遇到nil会继续
   ```

   

   

   

   



