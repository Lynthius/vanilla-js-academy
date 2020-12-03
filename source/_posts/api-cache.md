---
title: 27. API Cache
date: 2020-12-03 18:48:32
---

<div class="output-container">

  <style type="text/css">
  </style>
  <div id="app">
    Loading...
  </div>
  <script>
    const app = document.querySelector('#app');
    const getNews = function () {
      fetch('https://vanillajsacademy.com/api/pirates.json').then(function(response) {
        if (response.ok) {
          return response.json();
        } else {
          reutrn Promise.reject(response);
        }
      });
    }
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
