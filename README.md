# Online-calculator
Accurate online calculator

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Joseph's Online Calculator</title>
    <style>
        body { background-color: #121212; font-family: Arial, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; color: #fff; }
        .calculator { background-color: #1e1e1e; border-radius: 12px; padding: 20px; box-shadow: 0 4px 20px rgba(0,0,0,0.5); width: 300px; }
        .display { background-color: #333; border-radius: 8px; padding: 20px; text-align: right; font-size: 36px; margin-bottom: 20px; overflow: hidden; white-space: nowrap; text-overflow: ellipsis; }
        .buttons { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; }
        button { background-color: #424242; border: none; border-radius: 8px; color: #fff; font-size: 24px; padding: 15px; cursor: pointer; transition: background-color 0.2s; }
        button:hover { background-color: #616161; }
        button.operator { background-color: #ff9800; }
        button.operator:hover { background-color: #ffb74d; }
        button.equals { background-color: #4caf50; grid-column: span 2; }
        button.equals:hover { background-color: #66bb6a; }
        button.clear { background-color: #f44336; }
        button.clear:hover { background-color: #ef5350; }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="clear" onclick="clearDisplay()">C</button>
            <button onclick="backspace()">⌫</button>
            <button class="operator" onclick="append('%')">%</button>
            <button class="operator" onclick="append('÷')">÷</button>
            
            <button onclick="append('7')">7</button>
            <button onclick="append('8')">8</button>
            <button onclick="append('9')">9</button>
            <button class="operator" onclick="append('×')">×</button>
            
            <button onclick="append('4')">4</button>
            <button onclick="append('5')">5</button>
            <button onclick="append('6')">6</button>
            <button class="operator" onclick="append('-')">-</button>
            
            <button onclick="append('1')">1</button>
            <button onclick="append('2')">2</button>
            <button onclick="append('3')">3</button>
            <button class="operator" onclick="append('+')">+</button>
            
            <button onclick="append('0')">0</button>
            <button onclick="append('.')">.</button>
            <button class="equals" onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let currentInput = '0';

        function append(value) {
            if (currentInput === '0' && value !== '.') currentInput = '';
            currentInput += value;
            updateDisplay();
        }

        function clearDisplay() {
            currentInput = '0';
            updateDisplay();
        }

        function backspace() {
            currentInput = currentInput.slice(0, -1);
            if (currentInput === '') currentInput = '0';
            updateDisplay();
        }

        function updateDisplay()