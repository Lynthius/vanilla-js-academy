---
title: 12. Monster Shuffle
date: 2020-11-03
---

<div class="output-container">

  <style type="text/css">
    .row {
      display: grid;
      grid-template-columns: auto auto auto;
      text-align: center;
      margin-top: 60px;
    }

    .grid {
      min-height: 6em;
      padding: 1em;
    }

    img {
      height: auto;
      max-width: 100%;
    }
  </style>

  <div id="app">
    <div class="row">
      <div class="grid">1</div>
      <div class="grid">2</div>
      <div class="grid">3</div>
      <div class="grid">4</div>
      <div class="grid">5</div>
      <div class="grid">6</div>
    </div>
  </div>

  <footer>
    <hr>
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

    const shuffleArr = function (arr) {
      
    }


  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<div id="app"></div>

<footer>
  <hr>
  <p class="text-small text-muted">Icons by <a href="https://thenounproject.com/term/door/311732/">Jamie Dickinson</a>, <a href="https://thenounproject.com/term/monster/184225/">Nicky Knicky</a>, <a href="https://thenounproject.com/term/monster/1510400/">Alvaro Cabrera</a>, <a href="https://thenounproject.com/term/monster/28460/">Eliricon</a>, <a href="https://thenounproject.com/term/monster/82823/">April Yang</a>, <a href="https://thenounproject.com/term/monster/1062009/">tk66</a>, <a href="https://thenounproject.com/term/monster/24990/">Alex WaZa</a>, <a href="https://thenounproject.com/term/monster/37212/">Husein Aziz</a>, <a href="https://thenounproject.com/term/monster/2236082">iconcheese</a>,<br/> and <a href="https://thenounproject.com/term/socks/38451/">Yazmin Alanis</a>.</p>
</footer>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* Each monster (or sock) has a matching SVG in the source code.
For example, there’s a monster3 in the array, and a monster3.svg in the source code.
Shuffle the array of monsters, and render the matching SVG files into the #app element. */


```

</div>
