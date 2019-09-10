---
layout: page
title: "Categories"
---

<div style="line-height:20%;"> <br> </div>

{% for category in site.categories %}
  <h4>{{ category[0] }}</h4>
  <ul>
    {% for post in category[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a> &nbsp; <span style="color:darkblue; font-family:Calibri; font-size: 100%;"> <em> {{post.tags}} </em></span> </li>
    {% endfor %}
  </ul>
{% endfor %}


