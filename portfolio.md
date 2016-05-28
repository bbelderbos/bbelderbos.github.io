---
layout: page
title: Portfolio
---
<script type="text/javascript" src="/assets/resources/jquery/jquery.min.js"></script>
<script type="text/javascript" src="/assets/resources/jquery/blazy.min.js"></script>
<script type="text/javascript" >
$( document ).ready(function() {
  var bLazy = new Blazy(); 
  $( "#colorToggle" ).click(function() {
    $(this).text($(this).text() == ' b&w' ? ' color' : ' b&w');
    $( this ).toggleClass( "fa-toggle-off fa-toggle-on" );
    $( "#portfolio li img" ).toggleClass( "color" );
  });
});
</script>
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
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 8px;
  width:100%;
  max-width:700px;
}
.bw {
  filter:grayscale(100%); 
  -webkit-filter: grayscale(100%);
}
.color {
  filter:grayscale(0%); 
  -webkit-filter: grayscale(0%);
}
#colorToggle {
  margin: 0 0 10px 40px;
  cursor: pointer; cursor: hand;
}
</style>

<i id="colorToggle" class="fa fa-toggle-off fa-2x" aria-hidden="true"> color</i>
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
  <img class="bw b-lazy" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==" data-src="{{ site.baseurl }}{{ image.path }}" alt="{{name}}" />
  <hr>
</li>
    {% endif %}
{% endfor %}
</ul>
