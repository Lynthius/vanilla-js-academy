---
title: 33. Places
date: 2020-12-16 17:55:05
---

<div class="output-container">

  <style type="text/css">
  </style>

  <h1>Explore</h1>
  <p>Explore cool, quirky places in your own backyard.</p>
  <div id="app">Loading...</div>

  <script src="https://cdn.jsdelivr.net/npm/reefjs@7/dist/reef.js"></script>
  <script>
    var app = new Reef('#app', {
      data: {},
      template: function (props) {
        console.log(props)
        let html = '<ul>' + props.posts.map(function (post) {
          return `<li>${post.place}</li><p>${post.description}</p><img src="${post.img}">`;
        }).join('') + '</ul>';
        return html;
      }
    });
    fetch('https://vanillajsacademy.com/api/places.json').then(function (response) {
      return response.json();
    }).then(function (data) {
      app.data.posts = data;
    });

  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML

```

</div>
<div class="js-container">

## JavaScript

```JS
/* In today’s project, we’re going to build an app that
lets you find interesting things to do near where you live.
I have a simple API setup with some data from the quirkiest state
in the United States: Rhode Island. */



```

</div>
