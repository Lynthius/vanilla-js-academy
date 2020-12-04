---
title: 27. API Cache
date: 2020-12-03 18:48:32
---

<div class="output-container">

  <style type="text/css">
    #app {
      margin-top: 10px;
    }

    .article {
      margin: 0;
    }

    .title {
      list-style-type: none !important;
      padding: 0 !important;
      margin: 0 !important;
    }

    .container {
      display: flex;
      flex-direction: column;
    }
  </style>
  <div id="app">
    Loading...
  </div>
  <script>
    const appOutput = document.querySelector('#app');
    let storageID;
    var numberOfArticles = 2;
    const sanitizeHTML = function (str) {
      return str.replace(/[^\w. ]/gi, function (c) {
        return '&#' + c.charCodeAt(0) + ';';
      })
    };
    const isDataValid = function (saved, expirationDate) {
      if (!saved || !saved.data || !saved.timestamp) return false;
      const difference = new Date().getTime() - saved.timestamp;
      return difference < expirationDate;
    }
    const saveData = function (data) {
      const cache = {
        data: data,
        timestamp: new Date().getTime()
      }
      localStorage.setItem(storageID, JSON.stringify(cache));
    }
    const getData = function () {
      const saved = JSON.parse(localStorage.getItem(storageID));
      if (!saved) return;
      if(isDataValid(saved, 1000 * 10)) {
        return saved.data;
      }
    }
    const render = function (articles) {
      appOutput.innerHTML = '<h3 class="category">Pirate articles:</h3>' + articles.map(function(article) {
        return (`
            <div class="container">
              <ul class="title">
                <li> <strong>Title:</strong> ${sanitizeHTML(article.title)}</li>
                <li> <strong>Author:</strong> ${sanitizeHTML(article.author)}</li>
                <li> <strong>Publication date:</strong> ${sanitizeHTML(article.pubdate)}</li>
              </ul>
              <div class="article"><p>${sanitizeHTML(article.article)}</p></div>
            </div>
            <hr>
            <br>
            `);
      }).join('');
    }
    const getFirstFewArticles = function (articles) {
      return articles.slice(0, numberOfArticles);
    }
    const getNews = function () {
      // Check for valid cached data,
      // If exist, use it
      const saved = getData();
      if (saved) {
        render(saved);
        console.log("Loaded from cache");
        return;
      }
      fetch('https://vanillajsacademy.com/api/pirates.json').then(function(response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function(data) {
        const articles = getFirstFewArticles(data.articles);
        saveData(articles);
        render(articles);
        console.log("Fetched from API");
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
