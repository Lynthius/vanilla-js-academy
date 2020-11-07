---
title: 11. Sanitizing the NYT API Data
date: 2020-11-01
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

  <div id="app"></div>

  <script>
    const appOutput = document.querySelector('#app');
    const apiKey = 'T6l8P8ICK6XZr1u3OeA0qoGUFrEcSM5R';
    const sections = ['Technology', 'Science', 'Magazine'];
    const articleNum = 3;

    const render = function (articles, section) {
      appOutput.innerHTML += '<h3 class="category">' + section + ':' + '</h3>' + articles.map(function (article) {
        return (`
                <div class="container">
                  <ul class="title">
                  <li>${article.title}</li>
                  <a class="link" href="${article.url}" target="_blank">Read more</a>
                  </ul>
                </div>
                <br>
                `);
      }).join('')
    };

    const getLastNStories = function (articles) {
      return articles.slice(0, articleNum)
    }

    const getStories = function (section) {
      fetch(`https://api.nytimes.com/svc/topstories/v2/${section}.json?api-key=${apiKey}`).then(
        function (response, resolve) {
          if (response.ok) {
            return response.json();
          } else {
            return Promise.reject(response);
          };
        }).then(function (data) {
        const lastNStories = getLastNStories(data.results);
        render(lastNStories, section);
      }).catch(response => {
        console.log("something went wrong", response);
        appOutput.textContent = "Something went wrong...";
      });
    };

    sections.forEach(function (section) {
      getStories(section);
    });
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
/* Get articles from three to five categories, then render the API data
into markup and inject it into the #app element. Instead of rendering all of the articles,
use the first five from each category. Add a heading before each section so that you know
what category the articles are from. */

const appOutput = document.querySelector('#app');
const apiKey = 'T6l8P8ICK6XZr1u3OeA0qoGUFrEcSM5R';
const sections = ['Technology', 'Science', 'Magazine'];
const articleNum = 3;

const render = function (articles, section) {
  appOutput.innerHTML += '<h3 class="category">' + section + ':' + '</h3>' + articles.map(function (article) {
    return (`
            <div class="container">
              <ul class="title">
              <li>${article.title}</li>
              <a class="link" href="${article.url}" target="_blank">Read more</a>
              </ul>
            </div>
            <br>
            `);
  }).join('')
};

const getLastNStories = function (articles) {
  return articles.slice(0, articleNum)
}

const getStories = function (section) {
  fetch(`https://api.nytimes.com/svc/topstories/v2/${section}.json?api-key=${apiKey}`).then(
    function (response, resolve) {
      if (response.ok) {
        return response.json();
      } else {
        return Promise.reject(response);
      };
    }).then(function (data) {
    const lastNStories = getLastNStories(data.results);
    render(lastNStories, section);
  }).catch(response => {
    console.log("something went wrong", response);
    appOutput.textContent = "Something went wrong...";
  });
};

sections.forEach(function (section) {
  getStories(section);
});
```

</dvi>
