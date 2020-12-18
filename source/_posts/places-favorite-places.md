---
title: 34. Places - Favorite Places
date: 2020-12-17 17:55:05
---

<div class="output-container">

  <style type="text/css">
  .article-entry ul, .article-entry ol, .article-entry dl {
      margin-top: 0;
    }

    .category {
      margin-top: 10px;
    }

    .title {
      margin-top: 0;
      margin-bottom: 0;
      font-weight: 600;
      font-size: 20px;
    }

    .post-container {
      display: flex;
      flex-direction: row;
      margin: 20px 0;
    }

    @media screen and (max-width: 860px) {
      .post-container {
        flex-direction: column;
        margin: 20px auto;
        text-align: center;
      }
    }

    .info-container {
      margin-left: 40px;
    }

     @media screen and (max-width: 860px) {
      .info-container {
        margin-left: 0;
      }
    }

    .header {
      display: flex;
      justify-content: space-between;
    }

    .miniature-container {
      max-width: 380px;
    }

    .minature {
      height: auto;
      max-width: 100%;
    }

    .fave-btn {
      color: #ffffff;
      font-size: 26px;
      font-family: "system-ui";
      background-color: transparent;
      border: none;
      height: 40px;
      width: 40px;
      border-radius: 50%;
      cursor: pointer;
      outline: none;
    }

    .fave-btn[aria-pressed="true"] {
      color: #8e45ff;
    }

    .fave-btn:focus {
      border: red;
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }

    .fave-btn:active {
      color: #8e45ff;
    }
  </style>

  <p>Explore cool, quirky places in your own backyard.</p>
  <div id="app">Loading...</div>

  <script src="https://cdn.jsdelivr.net/npm/reefjs@7/dist/reef.js"></script>
  <script>
    var app = new Reef('#app', {
      data: {},
      template: function (props) {
        if (props.posts && props.posts.length) {
          let html = '<div class="container">' + props.posts.map(function (post) {
            return `<div class="post-container"><div class="miniature-container"><img class="minature" src="${post.img}" /></div><div class="info-container"><div class="header"><h2 class="title">${post.place}</h2><button data-fave="${post.id}" class="fave-btn" aria-label="add ${post.place} to favorite" aria-pressed="s" title="Add to favorite!">&#x2665;</button></div><p>${post.description}</p><p><em>${post.location}</em></p><a href=${post.url} target="_blank">Read more</a></div></div>`;
          }).join('') + '</div>';
          return html;
        }
        let html = '<p>Unable to find any places right now.</p>'
        return html;
      }
    });
    const getFaves = function () {
      const faves = localStorage.getItem(favesID);
      const favesObj = faves ? JSON.parse(faves) : {};
      return favesObj;
    }
    const saveFaves = function () {
      localStorage.setItem(favesId, JSON.stringify(faves));
    }
    const getPosts = function () {
      fetch('https://vanillajsacademy.com/api/places.json').then(function (response) {
        if (response.ok) {
          return response.json();
        }
        return Promise.reject(response);
      }).then(function (data) {
        app.data.faves = getFaves();
        app.data.posts = data;
      }).catch(function (error) {
        console.warn(error);
        app.data.posts = null;
      })
    }
    const clickHandler = function (e) {
      const postPlace = e.target.getAttribute('data-fave');
      if (!postPlace) return;
      console.log(postPlace);
      app.data.faves[postPlace] = app.data.faves[postPlace] ? false : true;
    }
    getPosts();
    document.addEventListener('click', clickHandler);
    // document.addEventListener('render', renderHandler);
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<p>Explore cool, quirky places in your own backyard.</p>
<div id="app">Loading...</div>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* For each place, add a “favorite” button. Give the button a different appearance
when the place is “favorited” versus when it’s not. When the user revisits the page,
their favorites should reload. You do not need to filter
or show only the favorite anywhere (that’s a future project). */

var app = new Reef('#app', {
  data: {},
  template: function (props) {
    if (props.posts && props.posts.length) {
      let html = '<div class="container">' + props.posts.map(function (post) {
        return `<div class="post-container"><div class="miniature-container"><img class="minature" src="${post.img}" /></div><div class="info-container"><h2 class="title">${post.place}</h2><p>${post.description}</p><p><em>${post.location}</em></p><a href=${post.url} target="_blank">Read more</a></div></div>`;
      }).join('') + '</div>';
      return html;
    }
    let html = '<p>Unable to find any places right now.</p>'
    return html;
  }
});
const getPosts = function () {
  fetch('https://vanillajsacademy.com/api/places.json').then(function (response) {
    if (response.ok) {
      return response.json();
    }
    return Promise.reject(response);
  }).then(function (data) {
    app.data.posts = data;
  }).catch(function (error) {
    console.warn(error);
    app.data.posts = null;
  })
}
getPosts();
```

</div>
