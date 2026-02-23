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
  border-bottom: 2px solid var(--border-color-01, #eee);
  padding-bottom: 0.5rem;
}

.tags-page .post-list {
  list-style: none;
  padding-left: 0;
}

.tags-page .post-list li {
  margin-bottom: 1rem;
  padding: 0.5rem;
  border-left: 3px solid #007acc;
  background-color: var(--background-color, #f9f9f9);
}

.tags-page .post-meta {
  font-size: 0.875rem;
  color: var(--text-color-light, #666);
}

.tags-page .post-link {
  text-decoration: none;
  color: var(--link-color, #007acc);
}

.tags-page .post-link:hover {
  text-decoration: underline;
}
</style>
