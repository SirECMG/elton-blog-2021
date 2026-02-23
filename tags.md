---
layout: page
title: Tags
permalink: /tags/
---

<div class="tags-page">
  {% assign sorted_tags = site.tags | sort %}
  {% for tag in sorted_tags %}
    {% assign tag_name = tag[0] %}
    {% assign tag_posts = tag[1] %}
    <div class="tag-section">
      <h2 id="{{ tag_name | slugify }}">{{ tag_name }}</h2>
      <ul class="post-list">
        {% for post in tag_posts %}
          <li>
            <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
            <h3>
              <a class="post-link" href="{{ post.url | relative_url }}">
                {{ post.title | escape }}
              </a>
            </h3>
          </li>
        {% endfor %}
      </ul>
    </div>
  {% endfor %}
</div>

<style>
.tags-page .tag-section {
  margin-bottom: 2rem;
}

.tags-page h2 {
  border-bottom: 2px solid;
  padding-bottom: 0.5rem;
  margin-bottom: 1rem;
}

.tags-page .post-list {
  list-style: none;
  padding-left: 0;
}

.tags-page .post-list li {
  margin-bottom: 1rem;
  padding: 1rem;
  border-left: 3px solid;
  border-radius: 4px;
}

.tags-page .post-meta {
  font-size: 0.875rem;
  opacity: 0.7;
  margin-bottom: 0.5rem;
}

.tags-page .post-link {
  text-decoration: none;
}

.tags-page .post-link:hover {
  text-decoration: underline;
}

.tags-page h3 {
  margin: 0;
  font-size: 1.1rem;
}

/* Light mode */
@media (prefers-color-scheme: light) {
  .tags-page h2 {
    border-bottom-color: #e1e4e8;
  }
  
  .tags-page .post-list li {
    background-color: #f6f8fa;
    border-left-color: #0366d6;
  }
  
  .tags-page .post-link {
    color: #0366d6;
  }
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  .tags-page h2 {
    border-bottom-color: #30363d;
  }
  
  .tags-page .post-list li {
    background-color: #21262d;
    border-left-color: #58a6ff;
  }
  
  .tags-page .post-link {
    color: #58a6ff;
  }
}
</style>
