---
title: 09. Latest 5 top stories
date: 2020-10-28
---

<div class="output-container">

  <style type="text/css">
    .container {
      display: flex;
      flex-direction: column;
    }

    .details {
      margin-bottom: 10px;
    }

    .link {
      text-decoration: none;
      margin: 5px 0 14px;
      color: white;
      max-width: 80px;
    }

    .link:hover {
      text-decoration: underline;
      color: white;
    }
  </style>

  <div id="app"></div>

  <script>
    const appOutput = document.querySelector('#app');
    const getStories = function () {
      fetch('https://api.nytimes.com/svc/topstories/v2/science.json?api-key=T6l8P8ICK6XZr1u3OeA0qoGUFrEcSM5R').then(
        function (response, resolve) {
          if (response.ok) {
            return response.json()
          } else {
            return Promise.reject(response)
          };
        }).then(function (data) {
        appOutput.innerHTML = data.results.map(function (result) {
          return (`
          <div class="container"> 
            <h3 class="title">${result.title}</h3>
            <div class="details">
            </div>
            <a class="link" href="${result.url}" target="_blank">Read more</a>
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
<p>Show some random quote.</p>

<div class="quote-container">
  <blockquote aria-live="polite">
    <span class="quote-mark">&ldquo;</span><span class="quote-output">Waiting for a new quote...</span>
  </blockquote>
</div>

<p>
  <button class="fetch-button">More Ron</button>
</p>
```

</div>
<div class="js-container">

## JavaScript

```JS
const fetchBtn = document.querySelector('.fetch-button');
const quoteOutput = document.querySelector('.quote-output');
const quoteContainer = document.querySelector('.quote-container');

const quotesArr = [];

var getQuote = function () {
  fetch('http://ron-swanson-quotes.herokuapp.com/v2/quotes').then(function (response) {
    if (response.ok) {
      return response.json();
    } else {
      return Promise.reject(response);
    }
  }).then(function (data) {
    console.log(data[0]);
    if (quotesArr.length === 50) {
      quotesArr.shift()
    }

    if (quotesArr.indexOf(data[0]) > -1) {
      getQuote()
      alterGradient()
      return;
    }
    quotesArr.push(data[0])
    quoteOutput.innerHTML = `<p class="quote-paragraph"> ${quotesArr[quotesArr.length - 1]}</p>`;

    console.log(quotesArr);
  }).catch(function (error) {
      quoteOutput.innerHTML = '[Something went wrong, sorry!] I have a joke for you... The government in this town is excellent, and uses your tax dollars efficiently.';
  });
};

function getQuote() {
  fetch('https://ron-swanson-quotes.herokuapp.com/v2/quotes').then(function (response) {
    if (response.ok) {
      return response.json()
    } else {
      return Promise.reject(response);
    }
  }).then(function (data) {
    renderQuote(data)
    alterGradient()
  }).catch(function (err) {
    console.log(err);
    return err;
  })
}

function alterGradient() {
  quoteContainer.style.background = `linear-gradient(${Math.floor(Math.random() * (90 - 35)) + 90}deg, rgba(142,69,${Math.floor(Math.random() * (255 - 100)) + 255},1), ${Math.floor(Math.random() * (20 - 10)) + 20}%, rgba(74,${Math.floor(Math.random() * (90 - 60)) + 90},${Math.floor(Math.random() * (280 - 140)) + 280},.8) ${Math.floor(Math.random() * (40 - 30)) + 40}%, rgba(142,69,255,1) 83%)`
}

getQuote()
fetchBtn.addEventListener('click', getQuote, false);
```

</dvi>
