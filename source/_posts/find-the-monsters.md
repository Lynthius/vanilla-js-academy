---
title: 13. Find the Monsters
date: 2020-11-06
---

<div class="output-container">

  <style type="text/css">
    .row {
      display: grid;
      background-color: wheat;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      grid-auto-rows: 100px;
      place-items: center;
      padding: 2rem 0 2rem 0;
      gap: 2rem 0;
    }

    .grid {
      min-height: 6em;
      padding: 1em;
    }

    img {
      height: 100%;
    }

    .button {
      border-color: white;
      outline: none;
      border: none;
      margin-top: 5px;
      padding: 5px 10px;
      border-radius: 3px;
      font-weight: 600px;
      cursor: pointer;
    }

    .button:focus {
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }

    .button:active {
      color: #8e45ff;
    }

    .show_button {
      cursor: pointer;
      border: 0;
      background-color: transparent;
      padding: .5rem .5rem;
    }

    .show_button:active {
      color: #8e45ff;
    }

    .show_button:focus {
      outline: 0; 
      box-shadow: 0 0 3px 1px #8e45ff;
    }

    .show_button:hover {
      outline: 0; 
      box-shadow: 0 0 3px 1px #8e45ff;
    }

  </style>

  <button class="button" value="monsters">Click to load and play!</button>

  <div id="app"></div>

  <footer>
    <p class="text-small text-muted">Icons by 
      <a href="https://thenounproject.com/term/door/311732/">Jamie Dickinson</a>, 
      <a href="https://thenounproject.com/term/monster/184225/">Nicky Knicky</a>, 
      <a href="https://thenounproject.com/term/monster/1510400/">Alvaro Cabrera</a>, 
      <a href="https://thenounproject.com/term/monster/28460/">Eliricon</a>, 
      <a href="https://thenounproject.com/term/monster/82823/">April Yang</a>, 
      <a href="https://thenounproject.com/term/monster/1062009/">tk66</a>, 
      <a href="https://thenounproject.com/term/monster/24990/">Alex WaZa</a>, 
      <a href="https://thenounproject.com/term/monster/37212/">Husein Aziz</a>, 
      <a href="https://thenounproject.com/term/monster/2236082">iconcheese</a>,<br/> 
      and <a href="https://thenounproject.com/term/socks/38451/">Yazmin Alanis</a>.</p>
  </footer>

  <script>
    const shuffleBtn = document.querySelector('.button');
    const app = document.querySelector('#app');

    const monsters = [
      'monster1',
      'monster2',
      'monster3',
      'monster4',
      'monster5',
      'monster6',
      'monster7',
      'monster8',
      'monster9',
      'monster10',
      'monster11',
      'sock'
    ];

    const render = function () {

      app.innerHTML = '<p>Click a door to reveal a monster. Try not to find the sock.</p><div class="row">' + monsters.map(monster => {
        return (`
          <div class="grid" aria-live="polite"><button class="show_button" data-id="${monster}"><img alt= "Click this picture of door to see monster" src="../img/door.svg"/></button></div>
        `)
      }).join('') + '</div>';
    };

    const shuffleArr = function (arr) {
      var currentIndex = arr.length;
      var temporaryValue, randomIndex;

      while (0 !== currentIndex) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        temporaryValue = arr[currentIndex];
        arr[currentIndex] = arr[randomIndex];
        arr[randomIndex] = temporaryValue;
      }
      render();
      return arr;
    }

    const replaceTargetElement = function (e) {
      const monster = e.target.closest('[data-id]');
      if (!monster) return;
      const monsterID = monster.getAttribute('data-id');
      monster.parentNode.innerHTML = `<img alt="A picture of ${monsterID}" src="../img/${monsterID}.svg"/>`
    }

    document.addEventListener('click', replaceTargetElement);

    shuffleBtn.addEventListener('click', function () {
      shuffleArr(monsters);
    });
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<button class="button" value="monsters">Click to load and play!</button>

<div id="app"></div>

<footer>
  <p class="text-small text-muted">Icons by
    <a href="https://thenounproject.com/term/door/311732/">Jamie Dickinson</a>,
    <a href="https://thenounproject.com/term/monster/184225/">Nicky Knicky</a>,
    <a href="https://thenounproject.com/term/monster/1510400/">Alvaro Cabrera</a>,
    <a href="https://thenounproject.com/term/monster/28460/">Eliricon</a>,
    <a href="https://thenounproject.com/term/monster/82823/">April Yang</a>,
    <a href="https://thenounproject.com/term/monster/1062009/">tk66</a>,
    <a href="https://thenounproject.com/term/monster/24990/">Alex WaZa</a>,
    <a href="https://thenounproject.com/term/monster/37212/">Husein Aziz</a>,
    <a href="https://thenounproject.com/term/monster/2236082">iconcheese</a>,<br/>
    and <a href="https://thenounproject.com/term/socks/38451/">Yazmin Alanis</a>.</p>
</footer>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* Display this image by default, and reveal the monster behind it after it’s clicked.
People who navigate the web with a keyboard or use a screen reader
should still be able to play this game. */

const shuffleBtn = document.querySelector('.button');
const app = document.querySelector('#app');

const monsters = [
  'monster1',
  'monster2',
  'monster3',
  'monster4',
  'monster5',
  'monster6',
  'monster7',
  'monster8',
  'monster9',
  'monster10',
  'monster11',
  'sock'
];

const render = function () {

  app.innerHTML = '<p>Click a door to reveal a monster. Try not to find the sock.</p><div class="row">' + monsters.map(monster => {
    return (`
      <div class="grid" aria-live="polite"><button class="show_button" data-id="${monster}"><img alt= "Click this picture of door to see monster" src="../img/door.svg"/></button></div>
    `)
  }).join('') + '</div>';
};

const shuffleArr = function (arr) {
  var currentIndex = arr.length;
  var temporaryValue, randomIndex;

  while (0 !== currentIndex) {
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex -= 1;

    temporaryValue = arr[currentIndex];
    arr[currentIndex] = arr[randomIndex];
    arr[randomIndex] = temporaryValue;
  }
  render();
  return arr;
}

const replaceTargetElement = function (e) {
  const monster = e.target.closest('[data-id]');
  if (!monster) return;
  const monsterID = monster.getAttribute('data-id');
  monster.parentNode.innerHTML = `<img alt="A picture of ${monsterID}" src="../img/${monsterID}.svg"/>`
}

document.addEventListener('click', replaceTargetElement);

shuffleBtn.addEventListener('click', function () {
  shuffleArr(monsters);
});
```

</div>
