---
title: 32. Countdown Timer - Reactive Data
date: 2020-12-13 18:25:46
---

<div class="output-container">

  <style type="text/css">
    #app {
      margin-top: 20px;
    }

    .buttons-container {
      display: flex;
      justify-content: space-between;
      max-width: 130px;
    }

    .button {
        border-color: white;
        outline: none;
        border: none;
        margin-top: 5px;
        min-width: 60px;
        padding: 5px 10px;
        border-radius: 3px;
        font-weight: 600px;
        cursor: pointer;
      }

      .button:focus {
        border: red;
        outline: none;
        box-shadow: 0 0 3px 1px #8e45ff;
      }

      .button:active {
        color: #8e45ff;
      }

      .counter {
        color: #8e45ff;
      }
  </style>
  <div id="app" aria-live="polite"></div>
  <script>
    const timeValue = 120;
    let timer;
    const handler = function (instance) {
      return {
        get: function (obj, prop) {
          if (['[object Object]', '[object Array]'].indexOf(Object.prototype.toString.call(obj[prop])) > -1) {
            return new Proxy(obj[prop], handler(instance));
          }
          return obj[prop];
          instance.render();
        },
        set: function (obj, prop, value) {
          obj[prop] = value;
          instance.render();
          return true;
        },
        deleteProperty: function (obj, prop) {
          delete obj[prop];
          instance.render();
          return true;
        }
      }
    }
    const Rue = function (selector, options) {
      const _this = this;
      _this.elem = document.querySelector(selector);
      const data = options.data;
      _this.template = options.template;
      Object.defineProperty(this, 'data', {
        get: function () {
          return _data;
        }, 
        set: function (data) {
          _data = new Proxy(data, handler(_this));
          _this.render();
          return true;
        }
      })
    };
    Rue.prototype.render = function () {
      this.elem.innerHTML = this.template(this.data);
    };
    const formatTime = function (time) {
      let minutes = Math.floor(time / 60);
      let seconds = time % 60;
      return `${(minutes.toString())}:${seconds.toString().padStart(2,'0')}`;
    }
    const startTimer = function (e) {
      if (!e.target.hasAttribute('data-start-timer')) return;
      if (app.data.time < 1) {
        app.data.time = timeValue;
      }
      app.data.paused = false;
      app.render();
      stopTimer();
      timer = setInterval(countdown, 1000);
    };
    const countdown = function () {
      app.data.time--
      if (app.data.time < 1) {
        stopTimer();
        app.data.paused = true;
      }
      app.render();
    }
    const stopTimer = function () {
      clearInterval(timer)
    }
    const pauseTimer = function (e) {
      if (!e.target.hasAttribute('data-pause-timer')) return;
      stopTimer();
      app.data.paused = true;
      app.render();
    }
    const restartTimer = function (e) {
      if (!e.target.hasAttribute('data-restart-timer') || app.data.time === timeValue) return;
      stopTimer();
      app.data.time = timeValue;
      app.data.paused = false;
      app.render();
      timer = setInterval(countdown, 1000);
    }
    const clickHandler = function (e) {
      startTimer(e);
      restartTimer(e);
      pauseTimer(e);
    }
    const app = new Rue('#app', {
      data: {
        time: timeValue,
        paused: true,
        altMsg: true
      },
      template: function (props) {
        if (!props) return;
        if (props.time === 0 && props.altMsg) {
          let html = `<h2>It's over, start again:</h2><button data-restart-timer class="button stop">Restart</button></div>`
          return html;
        }
        let html = `<h2>You've got only <span class="counter">${formatTime(props.time)}</span> seconds!</h2>` +
          (props.paused ? `<div class="buttons-container"><button data-start-timer class="button start">Start</button>` : `<div class="buttons-container"><button data-pause-timer class="button start">Pause</button>`) + `<button data-restart-timer class="button stop">Restart</button></div>`
        return html;
      }
    })
    app.render();
    document.addEventListener('click', clickHandler);
  </script>
</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<div id="app" aria-live="polite"></div>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* Instead of manually updating data properties and explicitly calling the render() method,
use Proxies and reactive data to automatically update the UI when you update your data. */

const timeValue = 120;
let timer;
const Rue = function (selector, options) {
  this.elem = document.querySelector(selector);
  this.data = options.data;
  this.template = options.template;
};
Rue.prototype.render = function () {
  this.elem.innerHTML = this.template(this.data);
};
const formatTime = function (time) {
  let minutes = Math.floor(time / 60);
  let seconds = time % 60;
  return `${(minutes.toString())}:${seconds.toString().padStart(2,'0')}`;
}
const startTimer = function (e) {
  if (!e.target.hasAttribute('data-start-timer')) return;
  if (app.data.time < 1) {
    app.data.time = timeValue;
  }
  app.data.paused = false;
  app.render();
  stopTimer();
  timer = setInterval(countdown, 1000);
};
const countdown = function () {
  app.data.time--
  if (app.data.time < 1) {
    stopTimer();
    app.data.paused = true;
  }
  app.render();
}
const stopTimer = function () {
  clearInterval(timer)
}
const pauseTimer = function (e) {
  if (!e.target.hasAttribute('data-pause-timer')) return;
  stopTimer();
  app.data.paused = true;
  app.render();
}
const restartTimer = function (e) {
  if (!e.target.hasAttribute('data-restart-timer') || app.data.time === timeValue) return;
  stopTimer();
  app.data.time = timeValue;
  app.data.paused = false;
  app.render();
  timer = setInterval(countdown, 1000);
}
const clickHandler = function (e) {
  startTimer(e);
  restartTimer(e);
  pauseTimer(e);
}
const app = new Rue('#app', {
  data: {
    time: timeValue,
    paused: true,
    altMsg: true
  },
  template: function (props) {
    if (!props) return;
    if (props.time === 0 && props.altMsg) {
      let html = `<h2>It's over, start again:</h2><button data-restart-timer class="button stop">Restart</button></div>`
      return html;
    }
    let html = `<h2>You've got only <span class="counter">${formatTime(props.time)}</span> seconds!</h2>` +
      (props.paused ? `<div class="buttons-container"><button data-start-timer class="button start">Start</button>` : `<div class="buttons-container"><button data-pause-timer class="button start">Pause</button>`) + `<button data-restart-timer class="button stop">Restart</button></div>`
    return html;
  }
})
app.render();
document.addEventListener('click', clickHandler);
```

</div>
