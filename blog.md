---
layout: blog
title: Posts
permalink: /blog/
---

<script type="text/javascript">
  function filterUsingCategory(selectedCategory) {
    var id = 0;
    {% for post in site.posts %}
      var cats = {{ post.categories | jsonify }}

      var postDiv = document.getElementById(++id);
      postDiv.style.display = (selectedCategory == 'all' || cats.includes(selectedCategory)) 
        ? 'unset' 
        : 'none';
    {% endfor %}
  }
</script>

<div class="tag-div">
  <h3>Tags</h3>
  <button id="all" onclick="filterUsingCategory('All')"><b>Show All Posts</b></button>
  {% assign categories = site.categories | sort %}
  {% for category in categories %}
    {% assign cat = category | first %}
    <button id="{{ cat }}" onclick="filterUsingCategory(this.id)">{{ cat }}</button>
  {% endfor %}
  <hr />
</div>

<div class="posts-wrapper">
  {% assign id = 0 %}
  {% for post in site.posts %}
    {% assign id = id | plus:1 %}
    <div class="post" id="{{id}}">
      <p class="itemInteriorSection">
        <a href="{{post.url}}">{{ post.articletitle }}</a><br />
          {% if post.author != "Jeff Langr" %}by {{ post.author }}{% endif %}
          <span><b>&middot;</b></span>
          {{ post.date | date: "%B %d, %Y" }}
   
          {% assign stringToCheck = ' ' %}
          {% assign checkArray = post.ncomments | split:stringToCheck %}
          {% unless checkArray[0] == '0' %}
            <span><b>&middot;</b></span>
            {{ post.ncomments }}
          {% endunless %}
      </p>
    </div>
  {% endfor %}
</div>