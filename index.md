---
layout: default
---

<body>

  <div class="index-wrapper">
    <div class="aside">
      <div class="info-card">
<<<<<<< HEAD
        <h1>CloudNotes</h1>
=======
        <h1>CloudNote</h1>
>>>>>>> e6ded5d6ed46772806eb65076457ee189d264a01
      </div>
      <div id="particles-js"></div>
    </div>


    <div class="index-content">
      <ul class="artical-list">
        {% for post in site.categories.blog %}
        <li>
          <a href="{{ post.url }}" class="title">{{ post.title }}</a>
          <div class="title-desc">{{ post.description }}</div>
        </li>
        {% endfor %}
      </ul>
    </div>
  </div>
</body>

