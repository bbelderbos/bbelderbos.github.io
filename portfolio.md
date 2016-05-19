---
layout: page
title: Portfolio
---
<style>
h2, h2 a {
  font-family: 'Ubuntu', sans-serif; 
}
li {
  position: relative;
  list-style: none; 
}
li h2 {
  position: absolute;
  bottom: 20px; 
  border-top: 1px solid #fff;
  padding: 5px;
  left: 15px;
  z-index: 10;
  background: rgba(0,0,0,0.7);
}
li h2 a {
  color: #fff;
}
li img {
  z-index:1;
}
img {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 8px;
  filter:grayscale(100%); 
  -webkit-filter: grayscale(100%);
}
</style>

<ul>
{% for image in site.static_files reversed %}
    {% if image.path contains 'portfolio/' %}
<li>
  {% assign fields = image.path | replace: '/assets/portfolio/', '' | replace: ':', '/' | remove: ".jpg" | split: '__' %}
  {% assign name = fields[0] | replace_first: '.', '. ' | replace: '-', ' ' %}
  {% assign link = "http://" | append: fields[1] %}
  {% assign target = "blank" %}
  {% if link contains "null" %}
    {% assign link = '#' %}
    {% assign target = "self" %}
  {% endif %}
  <h2><a href="{{link}}" target="_{{target}}">{{name}}</a></h2>
  <img src="{{ site.baseurl }}{{ image.path }}" alt="{{name}}" />
  <hr>
</li>
    {% endif %}
{% endfor %}
</ul>
