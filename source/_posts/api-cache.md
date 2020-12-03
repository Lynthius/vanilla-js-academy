---
title: 27. API Cache
date: 2020-12-03 18:48:32
---

<div class="output-container">

  <style type="text/css">
    #app {
        margin-top: 10px;
      }

    .article-entry ul, .article-entry ol, .article-entry dl {
      margin-top: 0;
    }

    .category {
      margin-top: 10px;
    }

    .title {
      margin-top: 0;
      margin-bottom: 0;
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
    Loading...
  </div>
  <script>
    const appOutput = document.querySelector('#app');
    const sanitizeHTML = function (str) {
      return str.replace(/[^\w. ]/gi, function(c) {
        return '&#' + c.charCodeAt(0) + ';';
      })
    };
    const render = function (articles) {
      appOutput.innerHTML = articles.map(function(article) {
        return (`
            <div class="container">
              <ul class="title">
              <li>${sanitizeHTML(article.url)}</li>
              <a class="link" href="${sanitizeHTML(article.url)}" target="_blank">Read more</a>
              </ul>
            </div>
            <br>
            `);
      })
      console.log('rendering...');
    }
    const getNews = function () {
      fetch('https://vanillajsacademy.com/api/pirates.json').then(function(response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function(data) {
        console.log(data)
        const articles = data.results;
        render(articles)
      }).catch(function (error) {
        console.log("something went wrong", error);
        appOutput.textContent = "Something went wrong...";
      })
    }
    getNews();
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
/* Cache the API data in localStorage for a short time, 
and use that instead of making a fresh API call on subsequent visits or page reloads. */



```

</div>
