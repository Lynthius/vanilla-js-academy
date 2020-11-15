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
    const app = document.querySelector('#app');
    const apiKeyIp = 'd9f7add9f68440818a0659381720a532';
    const apiKeyWeather = '5e995a3338fe2917188f0f98d08abcec';
    let userCity;

    const render = function (temp, city, sky) {
      app.innerHTML = (`
      <div class="weather_container>
        <h4 class="weather_temperature">${Math.round(temp)} &#x2103;</h4>
        <h3 class="weather_city-name">${city}</h3>
        <p class="weather_icon">${sky}</p>
      </div>
      `)
    };

    const getWeatherInfo = function () {
      fetch(`https://api.ipgeolocation.io/ipgeo?apiKey=${apiKeyIp}`).then(function (response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function (data) {
        userCity = data.city;
        return fetch(`http://api.openweathermap.org/data/2.5/weather?q=${userCity}&appid=${apiKeyWeather}&units=metric`);
      }).then(function (response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function (userData) {
        userTemp = userData.main.temp;
        userCity = userData.name;
        userSky = userData.weather[0].description;
        render(userTemp, userCity, userSky);
        console.log(userData);
      }).catch(function (err) {
        console.warn(err);
        appOutput.textContent = "Something went wrong...";
      })
    }

    getWeatherInfo();

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
