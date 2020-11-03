---
title: 07. Random Ron
date: 2020-10-24
---

<div class="output-container">

  <style type="text/css">
    .quote-container {
      background-color: grey;
      padding: 5px;
      min-height: 74px;
    }

    .quote-output {
      text-align: left;
      font-family: cursive;
    }
  </style>

  <div class="quote-container">
    <blockquotev class="quote-output" aria-live="polite"><em>Waiting for a new quote...</em></blockquotev>
  </div>

  <p>
    <button class="fetch-button">More Ron</button>
  </p>

  <script>
 const fetchBtn = document.querySelector('.fetch-button');
    const quoteOutput = document.querySelector('.quote-output');

    function getQuote() {
      fetch('https://ron-swanson-quotes.herokuapp.com/v2/quotes').then(function (response) {
        if (response.ok) {
          return response.json()
        } else {
          return Promise.reject(response);
        }
      }).then(function (data) {
        renderQuote(data)
      }).catch(function (err) {
        console.log(err);
        return err;
      })
    }

    getQuote()

    function renderQuote(data) {
      quoteOutput.innerHTML = data[0];
    }


    fetchBtn.addEventListener('click', getQuote);
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
s
```

</div>
<div class="js-container">

## JavaScript

```JS
s
```

</dvi>
