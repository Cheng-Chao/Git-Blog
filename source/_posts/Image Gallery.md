title: Image Gallery
date: 2017/1/2 13:21
categories:
- JavaScript
- HTML
tags:
- JavaScript
- HTML
- CSS
---
这是《JavaScript DOM编程艺术》第四章的一个Demo，包括HTML，JavaScript和CSS，以图片库来演示DOM操作。
<!--more-->

## HTML
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">   
    <script type="text/javascript" src="gallery.js"></script>
    <link rel="stylesheet" type="text/css" href="gallery.css"/>
    <title>Image gallery</title>
  </head>
  <body>
    <h1>SnapShots</h1>
    <ul>
      <li>
        <a href="images/Emma Roberts.jpg" 
           title="Emma Roberts" 
           onclick="showPic(this);return false;">Emma Roberts</a>
      </li>
      <li>
        <a href="images/Emmy Rossum.jpg" 
           title="Emmy Rossum" 
           onclick="showPic(this);return false;">Emmy Rossum</a>
        </li>
      <li>
        <a href="images/Eva Green.jpg" 
           title="Eva Green" 
           onclick="showPic(this);return false;">Eva Green</a>
      </li>
      <li>
        <a href="images/Kaya Scodelario.jpg" 
           title="Kaya Scodelario" 
           onclick="showPic(this);return false;">Kaya Scodelario</a>
      </li>
      <li>
        <a href="images/Kiriko Takemura.jpg" 
           title="Kiriko Takemura" 
           onclick="showPic(this);return false;">Kiriko Takemura</a>
      </li>
      <li>
        <a href="images/Selena Gomez.jpg" 
           title="Selena Gomez" 
           onclick="showPic(this);return false;">Selena Gomez</a>
      </li>
      <li>
        <a href="images/Sophie Turner.jpg" 
           title="Sophie Turner" 
           onclick="showPic(this);return false;">Sophie Turner</a>
      </li>
    </ul>
    <img id="placeholder" 
         src="images/startup.jpg" 
         alt="My Image gallery" width="30%" height="20%"/>
    <p id="description">Choose the actress you like.</p>
  </body>
</html>
```

## JavaScript
```javascript 
function showPic(whichPic){
    debugger;
    var imageSource = whichPic.getAttribute('href');
    var placeholder = document.getElementById('placeholder');
    placeholder.setAttribute('src',imageSource);
    var text = whichPic.getAttribute('title');
    var description = document.getElementById('description');
    description.firstChild.nodeValue = text;
}
```

## CSS
```css
body{
    font-family: Helvetica, Arial, sans-serif;
    color: #333;
    background-color: #ccc;
    margin: 1em 10%;
}
h1{
    color: #333;
    background-color: transparent;
}
p{
   font-family: Helvetica, Arial, sans-serif; 
   color: #c60;
   font-weight: bold;
}
a{
    color: #c60;
    background-color: transparent;
    font-weight: bold;
    text-decoration: none;
}
ul{
    padding: 0;
}
li{
    float: left;
    padding: 1em;
    list-style: none;
}
img{
    display: block;
    clear: both;
}
```

## GitHub
[Image Gallery](https://github.com/Cheng-Chao/Image-Gallery)