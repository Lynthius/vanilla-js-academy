---
title: 19. Weather App Plugin
date: 2020-11-17
---

<div class="output-container">

  <style type="text/css">
    #app {
      margin-top: 10px;
    }

    .weather_container {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .weather_icon {
      margin: 0 !important;
      padding: 0 !important;
    }

    .weather_temperature {
      letter-spacing: 1.5px;
      font-size: 3.2em !important;
      margin: 0 !important;
    }

    .weather_city-name {
      font-size: 2.4em !important;
      margin: 10px 0 0 !important;
    }

    .weather_desc {
      text-transform: uppercase;
      color: #8e45ff;
      margin: 10px 0 0 !important;
    }

  </style>

  <div id="app">Checking the weather near you...</div>

  <script>
    // const app = document.querySelector('#app');
    const apiKeyIp = 'd9f7add9f68440818a0659381720a532';
    const apiKeyWeather = '5e995a3338fe2917188f0f98d08abcec';
    let userCity;

    const sanitizeHTML = function (str) {
      return str.replace(/[^\w. ]/gi, function (c) {
        return '&#' + c.charCodeAt(0) + ';';
      });
    }

    const render = function (data) {

      // cons app = document.querySelector(settings.selector);
      // cons degree = document.querySelector(settings.degree);

      app.innerHTML = (`
      <div class="weather_container">
        <div class="weather_icon"><img src="https://openweathermap.org/img/wn/${settings.icon}@2x.png"></div>
        <h3 class="weather_temperature">${Math.round(settings.temp)} &#x2103;</h3>
        <h4 class="weather_city-name">${settings.city}</h4>
        <p class="weather_desc">${settings.conditions}</p>
      </div>
      `)
    };

    const getWeatherInfo = function (options) {

      // Default settings
      const defaults = {
        apiKeyIp: null,
        apiKeyWeather: null,
        selector: '#app',
        converTemp: false,
        orderInfo: '{{temp}} {{city}} {{conditions}}',
        noWeather: 'Unable to get weather data at this time. Sorry!',
        showIcon: true
      };

      // Merge user settings into default
      const settings = Object.assign(defaults, data);

      fetch(`https://api.ipgeolocation.io/ipgeo?apiKey=${apiKeyIp}`).then(function (response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function (data) {
        userCity = data.city;
        userDegree = 'metric';
        return fetch(`https://api.openweathermap.org/data/2.5/weather?q=${userCity}&appid=${apiKeyWeather}&units=${userDegree}`);
      }).then(function (response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function (userData) {
        // const defaults = {
        //   userIcon: userData.weather[0].icon,
        //   userTemp: userData.main.temp,
        //   userCity: userData.name,
        //   userSky: userData.weather[0].description
        // }
        
        render(userData);
      }).catch(function (err) {
        console.warn(err);
        app.textContent = "Something went wrong...";
      })
    }

    getWeatherInfo();
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 40px;">

## HTML

```HTML
<div id="app">Checking the weather near you...</div>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* Modify the script to let developers:
Pass in their own selector to render the weather into.
Decide whether to show temperatures in Fahrenheit of Celsius.
Change what message is shown (ex. It's currently {temperature} and {conditions} in {location}).
Enable or disable the icon for the weather conditions.*/

const app = document.querySelector('#app');
const apiKeyIp = 'd9f7add9f68440818a0659381720a532';
const apiKeyWeather = '5e995a3338fe2917188f0f98d08abcec';
let userCity;

const render = function (icon, temp, city, sky) {
  app.innerHTML = (`
  <div class="weather_container">
    <div class="weather_icon"><img src="http://openweathermap.org/img/wn/${icon}@2x.png"></div>
    <h3 class="weather_temperature">${Math.round(temp)} &#x2103;</h3>
    <h4 class="weather_city-name">${city}</h4>
    <p class="weather_desc">${sky}</p>
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
    userIcon = userData.weather[0].icon;
    userTemp = userData.main.temp;
    userCity = userData.name;
    userSky = userData.weather[0].description;

    render(userIcon, userTemp, userCity, userSky);
  }).catch(function (err) {
    console.warn(err);
    app.textContent = "Something went wrong...";
  })
}

getWeatherInfo();
```

</div>
