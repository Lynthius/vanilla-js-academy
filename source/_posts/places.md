---
title: 33. Places
date: 2020-12-16 17:55:05
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

    .miniature-container {
      max-width: 380px;
    }

    .minature {
      height: auto;
      max-width: 100%;
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
