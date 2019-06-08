---
layout: home
image: '/assets/images/cover4.jpg'
permalink: /tech
sitemap: yes
tags: [tech]
pagination:
    enabled: true
    category: tech
    permalink: page/:num/
    sort_reverse: false
---

<script>
    $("#menu li").removeClass("active").eq(0).addClass("active");
</script>

<ul id="post-list">
    {% for post in paginator.posts %}
        {% include item.html %}
    {% endfor %}
</ul>

{% include pagination.html %}
