---
layout: home
image: '/assets/images/cover4.jpg'
permalink: /tech/
pagination:
    enabled: true
    category: tech
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
