---
title: 18. Weather App
date: 2020-11-15
---

<div class="output-container">

  <style type="text/css">
    #app {
      margin-top: 10px;
    }
  </style>

  <div id="app">Checking the weather near you...</div>

  <script>
    const apiKey = 'a6acd35ed9f245b382e2d839dc911f09';
    let userCity;

    fetch('https://ipapi.co/json').then(function (response) {
      if (response.ok) {
        return response.json();
      } else {
        return Promise.reject(response);
      }
    }).then(function (data) {
      userCity = data.city;
      return fetch(`https://api.weatherbit.io/v2.0/current?city=${userCity},NC&key=${apiKey}`)
    }).then(function (response) {
      if (response.ok) {
        return response.json();
      } else {
        return Promise.reject(response);
      }
    }).then(function (userData) {
      console.log(userData);
    }).catch(function (err) {
      console.warn(err);
    })

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
/* For today’s project, we’re going to build an app that gets a user’s location
and displays their current weather information.


```

</div>
