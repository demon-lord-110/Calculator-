# Calculator-

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Simple Calculator</title>
<style>
  body {
    font-family: Arial, sans-serif;
    max-width: 400px;
    margin: 20px auto;
    background: #222;
    color: #eee;
    padding: 20px;
    border-radius: 10px;
    user-select: none;
  }
  h1 {
    text-align: center;
    margin-bottom: 15px;
  }
  #display {
    width: 100%;
    height: 50px;
    font-size: 24px;
    padding: 10px;
    border-radius: 8px;
    border: none;
    margin-bottom: 10px;
    background: #333;
    color: #fff;
    text-align: right;
  }
  #buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  button {
    padding: 15px 0;
    font-size: 20px;
    border: none;
    border-radius: 8px;
    background: #444;
    color: #eee;
    cursor: pointer;
    transition: background 0.3s;
  }
  button:hover {
    background: #666;
  }
  button.wide {
    grid-column: span 2;
  }
  #nav {
    margin-top: 20px;
    text-align: center;
  }
  #nav a {
    color: #f57c00;
    text-decoration: none;
    font-weight: bold;
    font-size: 16px;
  }
  #nav a:hover {
    text-decoration: underline;
  }
  @media (orientation: landscape) {
    body {
      max-width: 700px;
    }
    #buttons {
      grid-template-columns: repeat(8, 1fr);
      gap: 8px;
    }
    button {
      font-size: 22px;
      padding: 18px 0;
    }
    button.wide {
      grid-column: span 4;
    }
  }
</style>
</head>
<body>

<h1>Simple Calculator</h1>
<input type="text" id="display" readonly />
<div id="buttons">
  <button onclick="appendNumber('7')">7</button>
  <button onclick="appendNumber('8')">8</button>
  <button onclick="appendNumber('9')">9</button>
  <button onclick="appendOperator('/')">÷</button>

  <button onclick="appendNumber('4')">4</button>
  <button onclick="appendNumber('5')">5</button>
  <button onclick="appendNumber('6')">6</button>
  <button onclick="appendOperator('*')">×</button>

  <button onclick="appendNumber('1')">1</button>
  <button onclick="appendNumber('2')">2</button>
  <button onclick="appendNumber('3')">3</button>
  <button onclick="appendOperator('-')">−</button>

  <button onclick="clearDisplay()">C</button>
  <button onclick="appendNumber('0')">0</button>
  <button onclick="backspace()">⌫</button>
  <button onclick="appendOperator('+')">+</button>

  <button class="wide" onclick="calculate()">=</button>
</div>

<div id="nav">
  <a href="scientific.html">Go to Scientific Calculator →</a>
</div>

<script>
  const display = document.getElementById('display');

  function appendNumber(num) {
    display.value += num;
  }
  function appendOperator(op) {
    if (display.value === '') {
      if(op === '-') {
        display.value += op;
      }
      return;
    }
    const last = display.value.slice(-1);
    if ('+-*/'.includes(last)) return;
    display.value += op;
  }
  function clearDisplay() {
    display.value = '';
  }
  function backspace() {
    display.value = display.value.slice(0, -1);
  }
  function calculate() {
    try {
      let expr = display.value.replace(/÷/g, '/').replace(/×/g, '*');
      let res = Function('"use strict";return (' + expr + ')')();
      if (res === undefined) {
        display.value = 'Error';
      } else {
        display.value = res;
      }
    } catch {
      display.value = 'Error';
    }
  }
</script>

</body>
</html>
