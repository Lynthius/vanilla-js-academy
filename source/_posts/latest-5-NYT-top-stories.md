---
title: 09. Latest 5 top stories
date: 2020-10-28
---

<div class="output-container">

  <style type="text/css">
    #app {
      margin-top: 10px;
    }

    .title {
      margin-bottom: 0px;
    }

    .container {
      display: flex;
      flex-direction: column;
      max-height: 45px;
    }

    .details {
      margin-bottom: 0;
    }

    .link {
      text-decoration: none;
      color: white;
      max-width: 80px;
    }

    .link:hover {
      text-decoration: underline;
    }
  </style>

  <div id="app">
    <span id="placeholder"></span>
  </div>

  <script>
    const appOutput = document.querySelector('#app');
    const getStories = function () {
    fetch('https://api.nytimes.com/svc/topstories/v2/science.json?api-key=T6l8P8ICK6XZr1u3OeA0qoGUFrEcSM5R').then(
      function (response) {
        if (response.ok) {
          return response.json()
        } else {
          return Promise.reject(response)
        };
      }).then(function (data) {
      const allStories = [...data.results];
      const lastFiveStories = allStories.slice(0, 5)
      appOutput.innerHTML = lastFiveStories.map(function (result) {
        return (`
        <div class="container"> 
          <ul class="title">
          <li>${result.title}</li>
          <a class="link" href="${result.url}" target="_blank">Read more</a>
          </ul>
        </div>
        <br>
        `);
      }).join('')
    }).catch(response => {
      console.log("something went wrong", response);
      appOutput.textContent = "Something went wrong...";
    });
  };

  getStories();
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<div id="app">
  <span id="placeholder"></span>
</div>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* For this project, get an array of stories from the New York Times API,
turn them into markup, and inject them into the #app element. */

const appOutput = document.querySelector('#app');
const getStories = function () {
fetch('https://api.nytimes.com/svc/topstories/v2/science.json?api-key=T6l8P8ICK6XZr1u3OeA0qoGUFrEcSM5R').then(
  function (response) {
    if (response.ok) {
      return response.json()
    } else {
      return Promise.reject(response)
    };
  }).then(function (data) {
  const allStories = [...data.results];
  const lastFiveStories = allStories.slice(0, 5)
  appOutput.innerHTML = lastFiveStories.map(function (result) {
    return (`
    <div class="container"> 
      <ul class="title">
      <li>${result.title}</li>
      <a class="link" href="${result.url}" target="_blank">Read more</a>
      </ul>
    </div>
    <br>
    `);
  }).join('')
}).catch(response => {
  console.log("something went wrong", response);
  appOutput.textContent = "Something went wrong...";
});
};

getStories();
```

</div>
