---
layout: page
title: Posts
permalink: /posts/
---

<div class="posts-page">
  <h1>All Posts</h1>
  
  <ul class="post-list">
    {% for post in site.posts %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>
        {% if post.excerpt %}
          <p class="post-excerpt">{{ post.excerpt | strip_html | truncate: 160 }}</p>
        {% endif %}
        {% if post.tags.size > 0 %}
          <div class="post-tags">
            {% for tag in post.tags %}
              <span class="tag">{{ tag }}</span>
            {% endfor %}
          </div>
        {% endif %}
      </li>
    {% endfor %}
  </ul>
</div>

<style>
.posts-page h1 {
  margin-bottom: 2rem;
}

.posts-page .post-list {
  list-style: none;
  padding-left: 0;
}

.posts-page .post-list li {
  margin-bottom: 2rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid;
}

.posts-page .post-list li:last-child {
  border-bottom: none;
}

.posts-page .post-meta {
  font-size: 0.875rem;
  opacity: 0.7;
  margin-bottom: 0.5rem;
  display: block;
}

.posts-page .post-link {
  text-decoration: none;
}

.posts-page .post-link:hover {
  text-decoration: underline;
}

.posts-page h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.25rem;
}

.posts-page .post-excerpt {
  margin: 0.5rem 0;
  opacity: 0.8;
  line-height: 1.5;
}

.posts-page .post-tags {
  margin-top: 0.5rem;
}

.posts-page .tag {
  display: inline-block;
  padding: 0.2rem 0.5rem;
  margin-right: 0.5rem;
  font-size: 0.75rem;
  border-radius: 12px;
  text-decoration: none;
}

/* Light mode */
@media (prefers-color-scheme: light) {
  .posts-page .post-list li {
    border-bottom-color: #e1e4e8;
  }
  
  .posts-page .post-link {
    color: #0366d6;
  }
  
  .posts-page .tag {
    background-color: #f1f8ff;
    color: #0366d6;
  }
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  .posts-page .post-list li {
    border-bottom-color: #30363d;
  }
  
  .posts-page .post-link {
    color: #58a6ff;
  }
  
  .posts-page .tag {
    background-color: #0d1117;
    color: #58a6ff;
    border: 1px solid #30363d;
  }
}
</style>
