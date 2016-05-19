---
layout: page
title: Portfolio
---
<style>
#portfolio li h2, #portfolio li h2 a {
  font-family: 'Ubuntu', sans-serif; 
}
#portfolio li {
  position: relative;
  list-style: none; 
}
#portfolio li h2 {
  position: absolute;
  bottom: 20px; 
  left: 15px;
  border-top: 1px solid #fff;
  padding: 5px;
  z-index: 10;
  background: rgba(0,0,0,0.7);
}
#portfolio li h2 a {
  font-size: 1em;
  color: #fff;
}
@media screen and (max-width: 480px) {
   #portfolio li h2 a { font-size: 0.6em; }
}
@media screen and (max-width: 360px) {
   #portfolio li h2 a { font-size: 0.3em; }
}
#portfolio li img {
  z-index:1;
}
#portfolio li img {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 8px;
  filter:grayscale(100%); 
  -webkit-filter: grayscale(100%);
  width:100%;
  max-width:700px;
}
</style>

<ul id="portfolio">
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
