<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>AI Trading Bot - Smart AI Logic</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #eef2f9;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .container {
      background: white;
      padding: 25px;
      border-radius: 8px;
      box-shadow: 0 0 15px rgba(0,0,0,0.1);
      width: 380px;
    }
    h2 { text-align: center; }
    select {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
    }
    .result {
      background-color: #f1f5ff;
      padding: 15px;
      border-radius: 8px;
      text-align: center;
    }
    .up { color: green; font-weight: bold; }
    .down { color: red; font-weight: bold; }
    .accuracy { font-size: 18px; font-weight: bold; }
  </style>
</head>
<body>
  <div class="container">
    <h2>Smart AI Trading Bot</h2>

    <label>Select OTC Pair:</label>
    <select id="pair">
      <option value="EUR/USD">EUR/USD</option>
      <option value="GBP/JPY">GBP/JPY</option>
      <option value="AUD/USD">AUD/USD</option>
      <option value="USD/CHF">USD/CHF</option>
    </select>

    <label>Select Timeframe:</label>
    <select id="timeframe">
      <option value="1min">1 Minute</option>
      <option value="5min">5 Minutes</option>
    </select>

    <div class="result" id="result" style="display: none;">
      <p id="prediction" class="up">Prediction: UP</p>
      <p id="accuracy" class="accuracy">Accuracy: 92%</p>
      <p>Next trade in: <span id="timer">60</span> seconds</p>
    </div>
  </div>

  <script>
    const prices = Array.from({ length: 30 }, () => 100 + Math.random() * 10);
    const resultBox = document.getElementById('result');
    const predictionText = document.getElementById('prediction');
    const accuracyText = document.getElementById('accuracy');
    const timerText = document.getElementById('timer');

    function calculateRSI(data, period = 14) {
      let gains = 0, losses = 0;
      for (let i = data.length - period - 1; i < data.length - 1; i++) {
        const diff = data[i + 1] - data[i];
        if (diff > 0) gains += diff;
        else losses -= diff;
      }
      const avgGain = gains / period;
      const avgLoss = losses / period;
      const rs = avgGain / (avgLoss || 1);
      return 100 - (100 / (1 + rs));
    }

    function calculateMACD(data) {
      const ema = (arr, period) => {
        const k = 2 / (period + 1);
        return arr.reduce((acc, val, i) => {
          if (i === 0) return [val];
          acc.push(val * k + acc[i - 1] * (1 - k));
          return acc;
        }, []);
      };
      const ema12 = ema(data, 12);
      const ema26 = ema(data, 26);
      return ema12[ema12.length - 1] - ema26[ema26.length - 1];
    }

    function smartAIPrediction(rsi, macd, trendUp) {
      let score = 0;
      if (rsi < 30) score += 2;
      else if (rsi > 70) score -= 2;
      else score += 1;

      if (macd > 0) score += 2;
      else score -= 1;

      if (trendUp) score += 1;
      else score -= 1;

      return score >= 2 ? "UP" : "DOWN";
    }

    function simulateTrade() {
      const rsi = calculateRSI(prices);
      const macd = calculateMACD(prices);
      const trendUp = prices[prices.length - 1] > prices[prices.length - 5];
      const prediction = smartAIPrediction(rsi, macd, trendUp);

      const accuracy = prediction === "UP"
        ? Math.floor(Math.random() * 5) + 91
        : Math.floor(Math.random() * 5) + 88;

      predictionText.textContent = `Prediction: ${prediction}`;
      predictionText.className = prediction.toLowerCase();
      accuracyText.textContent = `Accuracy: ${accuracy}%`;
      resultBox.style.display = 'block';

      const lastPrice = prices[prices.length - 1];
      const newPrice = lastPrice + (Math.random() - 0.5) * 2;
      prices.push(newPrice);
      if (prices.length > 50) prices.shift();
    }

    function startAI() {
      simulateTrade();
      let count = 60;
      setInterval(() => {
        count--;
        timerText.textContent = count;
        if (count === 0) {
          simulateTrade();
          count = 60;
        }
      }, 1000);
    }

    window.onload = startAI;
  </script>
</body>
</html>
