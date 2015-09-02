---
layout: page
title: Tags
---
<style>
table{
    border-collapse: collapse;
    border-spacing: 0;
    border:2px solid #FFFFFF;
}

th{
    border:2px solid #FFFFFF;
}

td{
    border:1px solid #FFFFFF;
}
</style>

{% capture tags %}
  {% for tag in site.tags %}
    {{ tag[0] }}
  {% endfor %}
{% endcapture %}
{% assign sortedtags = tags | split:' ' | sort %}

<center>
<table style="width:75%;border:none;">
<tr>
{% for tag in sortedtags %}
  <td><a href="#{{ tag }}">{{ tag }}</a> </td>
{% endfor %}
</tr>
</table>
</center>
<hr>

{% for tag in sortedtags %}
  <h4 id="{{ tag }}">{{ tag }}</h4>
  <ul>
  {% for post in site.tags[tag] %}
   <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
{% endfor %}
