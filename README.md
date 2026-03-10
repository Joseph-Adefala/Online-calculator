<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Simple Calculator</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      min-height: 100vh;
      background: #0d1b2a;
      font-family: Arial, Helvetica, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .calculator {
      width: 100%;
      max-width: 340px;
      background: #1b263b;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 10px 30px rgba(0,0,0,0.6);
    }

    .display {
      background: #0a9396;
      color: white;
      font-size: 2.8rem;
      text-align: right;
      padding: 30px 20px;
      min-height: 100px;
      word-break: break-all;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 2px;
      background: #415a77;
      padding: 10px;
    }

    button {
      height: 70px;
      font-size: 1.6rem;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: all 0.12s;
      color: white;
    }

    button:hover {
      filter: brightness(1.15);
      transform: scale(1.03);
    }

    button:active {
      transform: scale(0.97);
    }

    .number {
      background: #778da9;
    }

    .operator {
      background: #e07a5f;
    }

    .equal {
      background: #81b29a;
      grid-row:
.clear {
      background: #ca6702;
      grid-column: span 2;
    }

    .zero {
      grid-column: span 2;
    }

    .dot {
      background: #778da9;
    }
  </style>
</head>
<body>

  <div class="calculator">
    <div class="display" id="display">0</div>

    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button class="operator" onclick="appendToDisplay('/')">/</button>

      <button class="number" onclick="appendToDisplay('7')">7</button>
      <button class="number" onclick="appendToDisplay('8')">8</button>
      <button class="number" onclick="appendToDisplay('9')">9</button>
      <button class="operator" onclick="appendToDisplay('*')">×</button>

      <button class="number" onclick="appendToDisplay('4')">4</button>
      <button class="number" onclick="appendToDisplay('5')">5</button>
      <button class="number" onclick="appendToDisplay('6')">6</button>
      <button class="operator" onclick="appendToDisplay('-')">-</button>

      <button class="number" onclick="appendToDisplay('1')">1</button>
      <button class="number" onclick="appendToDisplay('2')">2</button>
      <button class="number" onclick="appendToDisplay('3')">3</button>
      <button class="operator" onclick="appendToDisplay('+')">+</button>

      <button class="number zero" onclick="appendToDisplay('0')">0</button>
      <button class="dot" onclick="appendToDisplay('.')">.</button>
      <button class="equal" onclick="calculate()">=</button>
    </div>
  </div>

  <script>
    const display = document.getElementById('display');
    let currentInput = '0';

    function updateDisplay() {
      display.textContent = currentInput || '0';
    }

    function appendToDisplay(value) {
      if (currentInput === '0' && value !== '.') {
        currentInput = value;
      } else {
        currentInput += value;
      }
      updateDisplay();
    }

    function clearDisplay() {
      currentInput = '0';
      updateDisplay();
    }

    function calculate() {
      try {
        // Replace × with * so eval understands multiplication
        const expression = currentInput.replace(/×/g, '*');
        const result = eval(expression);
        
        // Show nicer number (no .00000)
        if (Number.isInteger(result)) {
          currentInput = result.toString();
        } else {
          currentInput = result.toFixed(8).replace(/\.?0+$/, '');
        }
      } catch (error) {
        currentInput = 'Error';
      }
      updateDisplay();
    }

    // Bonus: allow keyboard input
    document.addEventListener('keydown', (e) => {
      if (e.key >= '0' && e.key <= '9') appendToDisplay(e.key);
      else if (e.key === '.') appendToDisplay('.');
      else if (e.key === '+' || e.key === '-' || e.key === '*' || e.key === '/') {
        appendToDisplay(e.key === '*' ? '×' : e.key);
      }
      else if (e.key === 'Enter' || e.key === '=') calculate();
      else if (e.key === 'Backspace' || e.key === 'Delete') {
        if (currentInput.length > 1) {
          currentInput = currentInput.slice(0, -1);
        } else {
          currentInput = '0';
        }
        updateDisplay();
      }
      else if (e.key === 'Escape' || e.key === 'c' || e.key === 'C') clearDisplay();
    });
  </script>

</body>
</html>
