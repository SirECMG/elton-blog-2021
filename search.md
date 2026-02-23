---
title: Search Posts
layout: default
---

<div class="search-container">
  <h1>Search Blog Posts</h1>
  <form class="search-form">
    <input type="text" id="searchInput" placeholder="Search posts..." autocomplete="off" />
    <button type="submit">🔍</button>
  </form>
  <div id="searchResults"></div>
</div>

<script>
// Search functionality
(function() {
  // Get all posts data
  const posts = [
    {%- for post in site.posts -%}
    {
      title: "{{ post.title | escape }}",
      url: "{{ post.url | relative_url }}",
      date: "{{ post.date }}",
      excerpt: "{{ post.excerpt | strip_html | truncate: 160 | escape }}",
      categories: [{%- for category in post.categories -%}"{{ category | escape }}",{%- endfor -%}]
    }{% unless forloop.last %},{% endunless %}
    {%- endfor -%}
  ];

  const searchInput = document.getElementById('searchInput');
  const searchResults = document.getElementById('searchResults');

  // Function to search posts
  function searchPosts(query) {
    if (!query || query.length < 2) {
      return [];
    }
    
    const searchTerm = query.toLowerCase();
    return posts.filter(post => 
      post.title.toLowerCase().includes(searchTerm) ||
      post.excerpt.toLowerCase().includes(searchTerm) ||
      post.categories.some(cat => cat.toLowerCase().includes(searchTerm))
    );
  }

  // Display search results
  function displayResults(results) {
    if (results.length === 0) {
      searchResults.innerHTML = '<p>No posts found matching your search.</p>';
      return;
    }
    
    let html = '<h2>Search Results</h2><ul class="search-results-list">';
    
    results.forEach(post => {
      html += `
        <li class="search-result-item">
          <h3><a href="${post.url}">${post.title}</a></h3>
          <p class="post-meta">${post.date}</p>
          <p>${post.excerpt}</p>
        </li>
      `;
    });
    
    html += '</ul>';
    searchResults.innerHTML = html;
  }

  // Handle search input
  searchInput.addEventListener('input', function(e) {
    const query = e.target.value.trim();
    if (query.length >= 2) {
      const results = searchPosts(query);
      displayResults(results);
    } else {
      searchResults.innerHTML = '';
    }
  });

  // Handle form submission (prevent default)
  document.querySelector('.search-form').addEventListener('submit', function(e) {
    e.preventDefault();
    const query = searchInput.value.trim();
    if (query.length >= 2) {
      const results = searchPosts(query);
      displayResults(results);
    }
  });
})();
</script>

<style>
.search-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
}

.search-form {
  display: flex;
  margin-bottom: 30px;
  gap: 10px;
}

#searchInput {
  flex: 1;
  padding: 12px 15px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 24px;
  box-sizing: border-box;
}

.search-form button {
  padding: 12px 20px;
  background: #007acc;
  color: white;
  border: none;
  border-radius: 24px;
  cursor: pointer;
  font-weight: bold;
}

.search-form button:hover {
  background: #005a9e;
}

.search-results-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.search-result-item {
  border-bottom: 1px solid #eee;
  padding: 25px 0;
}

.search-result-item h3 {
  margin-top: 0;
  margin-bottom: 10px;
}

.post-meta {
  color: #666;
  font-size: 14px;
  margin-bottom: 10px;
}

@media (max-width: 768px) {
  .search-container {
    padding: 10px;
  }
  
  .search-form {
    flex-direction: column;
  }
  
  #searchInput, .search-form button {
    width: 100%;
  }
}
</style>
