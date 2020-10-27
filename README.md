# Tic Tac Toe
A simple Tic Tac Toe game made with HTML, CSS and JavaScript.

Made by Edrees Husseini. edreeshuss@gmail.com

# Table of Contents
[Install](#Install)
 </br></br>
[HTML Code](#HTML)
</br></br>
[JS Code](#JS)
</br></br>
[CSS Code](#CSS)
</br>
</br>






1. # Install

1. Go to [Repo](https://github.com/edgerees/tic-tac-toe.git) on GitHub profile
2. `Fork` and `clone` repo
3. Clone to local machine
 ```text
git  clone https://github.com/edgerees/tic-tac-toe.git
```
4. Go to tic-tac-toe directory
5. Open `index.html` in browser
```text
open index.html
```



2. # HTML

1. Make an html file and setup boiler plate by using '!' shortcut in VSCODE
```text
Type ! in VSCODE and click on html: boiler plate.
```

2. Link `CSS` and `JS` files
```html
<head>
  <link rel="stylesheet" type="text/css" href="css/style.css">
</head>
<body>
  <script type="text/javascript" src="js/app.js"></script>
</body>
```

3. Insert `div` elements that will be presented for the game.
```html

<body>
  <h1 class="title"> Tic Tac Toe</h1>
  <div class="grid-container">
    <div id="tictactoe"></div>
    <div id="player">
      <span id="turn" > </span>
    </div>
  </div>
  <script type="text/javascript" src="js/app.js"></script>
</body>
```

3. # JS

1. Setup the game.
```js
var AREA = 3, //setting up the game and creating new variables
  EMPTY = '&nbsp;',
  boxes = [],
  turn = 'X',
  score,
  moves;
  ```

2. Initialize the game and give its parameters with the `fuction(run)`
```js
function run() {
  var board = document.createElement('table');
  board.setAttribute('border', 1);
  board.setAttribute('cellspacing', 0);

  var identifier = 1;
  for (var i = 0; i < AREA; i++) {
    var row = document.createElement('tr');       
    board.appendChild(row);
    for (var j = 0; j < AREA; j++) {
      var cell = document.createElement('td');
      cell.setAttribute('height', 120);
      cell.setAttribute('width', 120);
      cell.setAttribute('align', 'center');
      cell.setAttribute('valign', 'center');
      cell.classList.add('col' + j, 'row' + i);
      if (i == j) {
        cell.classList.add('diagonal0');
      }
      if (j == AREA - i - 1) {
        cell.classList.add('diagonal1');
      }
      cell.identifier = identifier;
      cell.addEventListener('click', set);
      row.appendChild(cell);
      boxes.push(cell);
      identifier += identifier;
    }
  }

  document.getElementById('tictactoe').appendChild(board);
  startNewGame();
}
```
3. Setup a function that will start a new game with the `function startNewGame()` 
```js
function startNewGame() {
  score = {
    'X': 0,
    'O': 0
  };
  moves = 0;
  turn = 'X';
  boxes.forEach(function (square) {
    square.innerHTML = EMPTY;
  });
}
```
4. Setup a statement to check if player won or not.
```js
function win(clicked) {
 
  var memberOf = clicked.className.split(/\s+/);
  
  for (var i = 0; i < memberOf.length; i++) {
    var testClass = '.' + memberOf[i];
    var items = contains('#tictactoe ' + testClass, turn);
    if (items.length == AREA) {
      return true;
    }
  }
  return false;
}
function contains(selector, text) {
  var elements = document.querySelectorAll(selector);
  return [].filter.call(elements, function (element) {
    return RegExp(text).test(element.textContent);
  });
}
```
5. This function sets the square clicked and also changes turns.
```js
function set() {
  if (this.innerHTML !== EMPTY) {
    return;
  }
  this.innerHTML = turn;
  moves += 1;
  score[turn] += this.identifier;
  if (win(this)) {
    alert('Winner: Player ' + turn);
    startNewGame();
  } else if (moves === AREA * AREA) {
    alert('Draw');
    startNewGame();
  } else {
    turn = turn === 'X' ? 'O' : 'X';
    document.getElementById('turn').textContent = 'Player ' + turn;
  }
}
run();
```
4. # CSS 

1. After creating the class called `grid-container`, fix the parameters of the layout using `flex`.
```css

.grid-container {
  display: flex;
  flex-direction: column;
  background: rgb(191, 183, 255);
  align-content: center;
  justify-content: center;
  min-height: 800px;
  border-radius: 5%;
  min-width: 1000px;
  margin: auto;
 
}
```

2. Style and layout of the table and position the body using `flex`.
```CSS
table {
  border-collapse: collapse;
  margin: auto;
}
body {
  display: flex;
  height: 50vh;
  width: 10%;
  overflow: hidden;
}
```
3. Style the colors and sizes of the title, player, and player turn parts of the game.

```CSS
#player {
  padding: 5px;
  color: blue;
  font-size: 50px;
  border: 10px solid blue;
  align; center 
}

td {
  background-color:rgb(21, 255, 0);
  border: 5px solid white;
  font-size: 100px;
  color: #fff;
  border-radius: 5%;
}

.title {
  color: blue;
}
```


