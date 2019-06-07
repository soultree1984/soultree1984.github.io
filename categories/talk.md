---
layout: home
image: '/assets/images/cover6.jpg'
permalink: /talk
sitemap: yes
tags: [talk]
pagination:
    enabled: true
    category: talk
    permalink: page/:num/
    sort_reverse: false
---

<script>
    $("#menu li").removeClass("active").eq(1).addClass("active");
</script>

<ul id="post-list">
    {% for post in paginator.posts %}
        {% include item.html %}
    {% endfor %}
</ul>

{% include pagination_talk.html %}