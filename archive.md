---
layout: page
title: Archive
---

<div style="line-height:80%;"> <br> </div>

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{site.baseurl}}{{ post.url }})
{% endfor %}

