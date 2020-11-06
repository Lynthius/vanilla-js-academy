---
title: 07. Random Ron
date: 2020-10-24
---

<div class="output-container">

  <style type="text/css">
    .fetch-button {
      border-color: white;
      outline: none;
      border: none;
      margin-top: 5px;
      padding: 5px 10px;
      border-radius: 3px;
      font-weight: 600px;
      cursor: pointer;
    }

    .fetch-button:focus {
      border: red;
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }

    .fetch-button:active {
      color: #8e45ff;
    }

     .quote-container {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      background: rgb(142,69,255);
      background: linear-gradient(63deg, rgba(142,69,255,1) 16%, rgba(74,62,184,1) 49%, rgba(142,69,255,1) 83%);
      border-radius: 3px;
      padding: 8px;
      min-height: 200px;
      width: 98%;
      font-size: 16px;
    }

    .quote-output {
      text-align: center;
      color: white;
      font-size: 16px;
      font-family: 'helvetica';
    }

    .quote-mark{
      position: absolute;
      top: 0;
      left: 20px;
      color: rgba(250,250,250 ,1);
      font-size: 90px;
      font-family: 'lato';
    }

    .quote-paragraph {
      padding: 0 60px;
      font-size: 16px;
      font-family: 'helvetica';
    }
  </style>

  <p>Show some random quote.</p>

  <div class="quote-container">
    <blockquote aria-live="polite">
      <span class="quote-mark">&ldquo;</span><span class="quote-output">Waiting for a new quote...</span>
    </blockquote>
  </div>

  <p>
    <button class="fetch-button">More Ron</button>
  </p>

  <script>
    const fetchBtn = document.querySelector('.fetch-button');
    const quoteOutput = document.querySelector('.quote-output');
    const quoteContainer = document.querySelector('.quote-container');

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

    function renderQuote(data) {
      quoteOutput.innerHTML = `<p class="quote-paragraph"> ${data[0]}</p>`;
    }

    function alterGradient() {
      quoteContainer.style.background = `linear-gradient(${Math.floor(Math.random() * (90 - 35)) + 90}deg, rgba(142,69,${Math.floor(Math.random() * (255 - 100)) + 255},1), ${Math.floor(Math.random() * (20 - 10)) + 20}%, rgba(74,${Math.floor(Math.random() * (90 - 60)) + 90},${Math.floor(Math.random() * (280 - 140)) + 280},.8) ${Math.floor(Math.random() * (40 - 30)) + 40}%, rgba(142,69,255,1) 83%)`
    }

    getQuote()

    fetchBtn.addEventListener('click', getQuote);
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

function renderQuote(data) {
  quoteOutput.innerHTML = `<p class="quote-paragraph"> ${data[0]}</p>`;
}

function alterGradient() {
  quoteContainer.style.background = `linear-gradient(${Math.floor(Math.random() * (90 - 35)) + 90}deg, rgba(142,69,${Math.floor(Math.random() * (255 - 100)) + 255},1), ${Math.floor(Math.random() * (20 - 10)) + 20}%, rgba(74,${Math.floor(Math.random() * (90 - 60)) + 90},${Math.floor(Math.random() * (280 - 140)) + 280},.8) ${Math.floor(Math.random() * (40 - 30)) + 40}%, rgba(142,69,255,1) 83%)`
}

getQuote()

fetchBtn.addEventListener('click', getQuote);
```

</dvi>
