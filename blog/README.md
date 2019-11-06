---
title: Blog
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
    
    h4 {
      margin: 0;
      font-weight: bold;
    }
    
    p {
      text-align: justify;
    }
    
    img {
      border-radius: 5px 5px 0 0;
    }
</style>

<script type="text/javascript">
    function goTo(where) {
        if (where === 'data-science') {
            window.location.href = "/blog/data-science/";
        } else {
            window.location.href = "/blog/news/";
        }
    }
</script>

<div class="container">
    <div class="card" onclick="goTo('data-science');">
       <img src="../assets/img/data-science.png" alt="Data Science" style="width:100%">
       <div class="texts">
         <h4>Data Science</h4>
         <p>Data science is the field of study that combines domain expertise, programming skills, and knowledge of 
         mathematics and statistics to extract meaningful insights from data.</p>
       </div>
    </div>
    <div class="card" onclick="goTo('news');">
       <img src="../assets/img/news.jpg" alt="Data Science" style="width:100%">
       <div class="texts">
         <h4>News</h4>
         <p>Here are the news and curiosities of the Computer Science world.</p>
       </div>
    </div>
</div>
