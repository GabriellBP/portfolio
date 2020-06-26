---
title: Blog
layout: page
description: >
 Here you should be able to find the categories of my blog.
hide_description: false
permalink: /blog/
---

<style>
    .container {
        display: flex;
        flex-direction: row;
    }

    .card {
      max-width: 300px;
      min-height: 500px;
      box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
      transition: 0.3s;
      border-radius: 5px; /* 5px rounded corners */
      margin: 5px;
    }
    
    .card:hover {
      cursor: pointer;
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
    }
    
    .texts {
      padding: 2px 16px;
    }
    
    .card-title {
      margin: 0;
      font-weight: bold;
    }
    
    .card-subtitle {
      text-align: justify;
    }
    
    .card-img {
      border-radius: 5px 5px 0 0;
      width:100%
    }
</style>

<script type="text/javascript">
    function goTo(where) {
        if (where === 'data-science') {
            window.location.href = "data-science/";
        } else {
            window.location.href = "news/";
        }
    }
</script>

<div class="container">
    <div class="card" onclick="goTo('data-science');">
       <img src="/assets/img/data-science.png" alt="Data Science" class="card-img">
       <div class="texts">
         <h4 class="card-title">Data Science</h4>
         <p class="card-subtitle">Data science is the field of study that combines domain expertise, programming skills, and knowledge of 
         mathematics and statistics to extract meaningful insights from data.</p>
       </div>
    </div>
    <!--
    <div class="card" onclick="goTo('news');">
       <img src="/assets/img/news.jpg" alt="News" class="card-img">
       <div class="texts">
         <h4 class="card-title">News</h4>
         <p class="card-subtitle">Here are the news and curiosities of the Computer Science world.</p>
       </div>
    </div>
    -->
</div>
