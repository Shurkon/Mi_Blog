---
layout: default
title: search
---

<h2>🔍 Buscar artículos</h2>

<input type="text" id="search-box" placeholder="Escribe para buscar..." style="width:100%; padding:10px; margin:20px 0; font-size:1rem; background-color:#bcbcbc; border:1px solid #000000; border-radius:15px;">

<ul id="search-results"></ul>

<script src="https://unpkg.com/lunr/lunr.js"></script>
<script>
  let idx = null;
  let posts = [];

  fetch("/search.json")
    .then(response => response.json())
    .then(data => {
      posts = data;
      idx = lunr(function () {
        this.ref("url");
        this.field("title", { boost: 10 }); // Prioriza coincidencias en título
        this.field("content");
        posts.forEach(doc => this.add(doc));
      });
    });

  document.addEventListener("DOMContentLoaded", function () {
    const input = document.getElementById("search-box");
    const resultList = document.getElementById("search-results");

    if (!input) return;

    input.addEventListener("input", function () {
      if (!idx) return;

      const query = this.value.trim();
      resultList.innerHTML = "";
      if (query.length < 2) return;

      const results = idx.search(query);
      results.forEach(result => {
        const post = posts.find(p => p.url === result.ref);
        const li = document.createElement("li");
        li.innerHTML = `<a href="${post.url}">${post.title}</a>`;
        resultList.appendChild(li);
      });
    });
  });
</script>
