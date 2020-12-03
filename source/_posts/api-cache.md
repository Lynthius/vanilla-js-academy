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
    const saveToLocalStorage = function (articles) {
      if (!articles) return;
      localStorage.setItem('pirate-news', JSON.stringify(articles));
    }
    const getArticleFromLocalStorage = function () {
      const articles = JSON.parse(localStorage.getItem('pirate-news'));
      if(isDataValid(articles, 1000 * 60)) {
        render(articles);
      } else {
        console.log("Nope, fetch another one");
        // render(articles);
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
      fetch('https://vanillajsacademy.com/api/pirates.json').then(function(response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function(data) {
        const articles = getFirstFewArticles(data.articles);
        console.log(articles);
        saveToLocalStorage(articles);
      }).catch(function (error) {
        console.log("something went wrong", error);
        appOutput.textContent = "Something went wrong...";
      })
    }
    getNews();
    getArticleFromLocalStorage();
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
