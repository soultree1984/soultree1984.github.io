---
layout: home
title: Talk
permalink: /talks
image: '/assets/images/cover6.jpg'
sitemap: yes
tags: [refer]
---

<script>
    $("#menu li").removeClass("active").eq(1).addClass("active");
</script>

<ul id="post-list">
    {% for post in site.categories.talk %}
        {% include item_talks.html %}
    {% endfor %}
</ul>