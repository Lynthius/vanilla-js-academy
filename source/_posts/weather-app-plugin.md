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
    const getWeather = function (options) {

      // Default settings for weather app
      const defaults = {
        apiKeyIp: null,
        apiKeyWeather: null,
        selector: '#app',
        convertTemp: false,
        noWeather: 'Unable to get weather data at this time. Sorry!',
        showIcon: true,
        showTemp: true,
        showCity: true,
        showConditions: true,
      };

      // Merge user settings into default
      const settings = Object.assign(defaults, options);

      // Get the #app element to render content
      const app = document.querySelector(settings.selector);

      // Secure your data
      const sanitizeHTML = function (str) {
        const temp = document.createElement('div');
        temp.textContent = str;
        return temp.innerHTML;
      }

      // Convert Celcius to Farenheit and round value
      const FarenheitToCelcius = function (temp) {
        if (settings.convertTemp) {
          return `${(Math.round((temp) * 9/5)) + 32} &#x2109`;
        }

        return `${Math.round(temp)} &#x2103`;
      };

      // Get weather icon form fetch data
      const getIcon = function (fetchData) {
        if (!settings.showIcon) return '';

        const html = `
          <div class="weather_icon">
            <img src="https://openweathermap.org/img/wn/${sanitizeHTML(fetchData.weather[0].icon)}@2x.png">
          </div>`
        return html;
      };

      // Get weather temperature from fetch data
      const getTemp = function (fetchData) {
        if (!settings.showTemp) return '';

        const html = `
          <h3 class="weather_temperature">
            ${FarenheitToCelcius(sanitizeHTML(fetchData.main.temp))};
          </h3>`
        return html;
      };

      // Get weather city location from fetch data
      const getCity = function (fetchData) {
        if (!settings.showCity) return '';

        const html = `
          <h4 class="weather_city-name">
            ${sanitizeHTML(fetchData.name)}
          </h4>`
        return html;
      };

      // Get weather conditions from fetch data
      const getConditions = function (fetchData) {
        if (!settings.showConditions) return '';

        const html = `
          <p class="weather_desc">
            ${sanitizeHTML(fetchData.weather[0].description)}
          </p>`
        return html;
      };

      // Render your weather data
      const renderWeather = function (fetchData) {
        app.innerHTML = (`
      <div class="weather_container">
        ${getIcon(fetchData)}
        ${getTemp(fetchData)}
        ${getCity(fetchData)}
        ${getConditions(fetchData)}
      </div>
      `)
      };

      // Render warning info when renderWeather doesn't work
      const renderNoWeather = function () {
        app.innerHTML = settings.noWeather;
      };

      // Check for API
      if (!settings.apiKeyIp || !settings.apiKeyWeather) {
        console.warn('Please provide an API key.');
        return;
      }

      // Get the user's location by IP address
      // Then, pass that into the weather API and get the current weather
      fetch(`https://api.ipgeolocation.io/ipgeo?apiKey=${settings.apiKeyIp}`).then(function (response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function (data) {
        return fetch(`https://api.openweathermap.org/data/2.5/weather?q=${data.city}&appid=${settings.apiKeyWeather}&units=metric`);
      }).then(function (response) {
        if (response.ok) {
          return response.json();
        } else {
          return Promise.reject(response);
        }
      }).then(function (data) {
        renderWeather(data);
      }).catch(function (err) {
        console.warn(err);
        renderNoWeather();
      })
    }

    // Init function - customize your settings
    getWeather({
      apiKeyIp: 'd9f7add9f68440818a0659381720a532', // Replace this with your API key
      apiKeyWeather: '5e995a3338fe2917188f0f98d08abcec', // Replace this with your API key
      selector: '#app',
      convertTemp: false,
      noWeather: 'Unable to get weather data at this time. Sorry!',
      showIcon: true,
      showTemp: true,
      showCity: true,
      showConditions: true,
    });
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
Change what message is shown.
Enable or disable the icon for the weather conditions.*/

const getWeather = function (options) {

  // Default settings for weather app
  const defaults = {
    apiKeyIp: null,
    apiKeyWeather: null,
    selector: '#app',
    convertTemp: false,
    noWeather: 'Unable to get weather data at this time. Sorry!',
    showIcon: true,
    showTemp: true,
    showCity: true,
    showConditions: true,
  };

  // Merge user settings into default
  const settings = Object.assign(defaults, options);

  // Get the #app element to render content
  const app = document.querySelector(settings.selector);

  // Secure your data
  const sanitizeHTML = function (str) {
    const temp = document.createElement('div');
    temp.textContent = str;
    return temp.innerHTML;
  }

  // Convert Celcius to Farenheit and round value
  const FarenheitToCelcius = function (temp) {
    if (settings.convertTemp) {
      return `${(Math.round((temp) * 9/5)) + 32} &#x2109`;
    }

    return `${Math.round(temp)} &#x2103`;
  };

  // Get weather icon form fetch data
  const getIcon = function (fetchData) {
    if (!settings.showIcon) return '';

    const html = `
      <div class="weather_icon">
        <img src="https://openweathermap.org/img/wn/${sanitizeHTML(fetchData.weather[0].icon)}@2x.png">
      </div>`
    return html;
  };

  // Get weather temperature from fetch data
  const getTemp = function (fetchData) {
    if (!settings.showTemp) return '';

    const html = `
      <h3 class="weather_temperature">
        ${FarenheitToCelcius(sanitizeHTML(fetchData.main.temp))};
      </h3>`
    return html;
  };

  // Get weather city location from fetch data
  const getCity = function (fetchData) {
    if (!settings.showCity) return '';

    const html = `
      <h4 class="weather_city-name">
        ${sanitizeHTML(fetchData.name)}
      </h4>`
    return html;
  };

  // Get weather conditions from fetch data
  const getConditions = function (fetchData) {
    if (!settings.showConditions) return '';

    const html = `
      <p class="weather_desc">
        ${sanitizeHTML(fetchData.weather[0].description)}
      </p>`
    return html;
  };

  // Render your weather data
  const renderWeather = function (fetchData) {
    app.innerHTML = (`
  <div class="weather_container">
    ${getIcon(fetchData)}
    ${getTemp(fetchData)}
    ${getCity(fetchData)}
    ${getConditions(fetchData)}
  </div>
  `)
  };

  // Render warning info when renderWeather doesn't work
  const renderNoWeather = function () {
    app.innerHTML = settings.noWeather;
  };

  // Check for API
  if (!settings.apiKeyIp || !settings.apiKeyWeather) {
    console.warn('Please provide an API key.');
    return;
  }

  // Get the user's location by IP address
  // Then, pass that into the weather API and get the current weather
  fetch(`https://api.ipgeolocation.io/ipgeo?apiKey=${settings.apiKeyIp}`).then(function (response) {
    if (response.ok) {
      return response.json();
    } else {
      return Promise.reject(response);
    }
  }).then(function (data) {
    return fetch(`https://api.openweathermap.org/data/2.5/weather?q=${data.city}&appid=${settings.apiKeyWeather}&units=metric`);
  }).then(function (response) {
    if (response.ok) {
      return response.json();
    } else {
      return Promise.reject(response);
    }
  }).then(function (data) {
    renderWeather(data);
  }).catch(function (err) {
    console.warn(err);
    renderNoWeather();
  })
}

// Init function - customize your settings
getWeather({
  apiKeyIp: 'd9f7add9f68440818a0659381720a532', // Replace this with your API key
  apiKeyWeather: '5e995a3338fe2917188f0f98d08abcec', // Replace this with your API key
  selector: '#app',
  convertTemp: false,
  noWeather: 'Unable to get weather data at this time. Sorry!',
  showIcon: true,
  showTemp: true,
  showCity: true,
  showConditions: true,
});
```

</div>
