---
layout: page
title: search
---

## 🔍 Buscar artículos

<input type="text" id="search-box" placeholder="Escribe para buscar..." style="width:100%; padding:10px; margin:20px 0; font-size:1rem; background-color:#bcbcbc; border:1px solid #000000; border-radius:15px;">

<ul id="search-results"></ul>

<script>
  let idx = null;
  let posts = [];

  fetch("/search.json")
    .then(response => response.json())
    .then(data => {
      posts = data;
      idx = lunr(function () {
        this.ref("url");
        this.field("title");
        this.field("content");
        data.forEach(doc => this.add(doc));
      });
    });

  document.getElementById("search-box").addEventListener("input", function () {
    const query = this.value;
    const results = idx.search(query);
    const resultList = document.getElementById("search-results");
    resultList.innerHTML = "";

    if (query.length < 2) return;

    results.forEach(result => {
      const post = posts.find(p => p.url === result.ref);
      const li = document.createElement("li");
      li.innerHTML = `<a href="${post.url}">${post.title}</a>`;
      resultList.appendChild(li);
    });
  });
</script>
