# This is a test page for a financial stock summary
<html><head><base href="https://websim.ai/finance-dashboard/" /><meta charset="utf-8"><meta name="viewport" content="width=device-width, initial-scale=1"><title>FinViz: AAPL Stock Analysis</title>
<style>
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f0f2f5;
  color: #333;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}
header {
  background-color: #1a237e;
  color: white;
  padding: 20px 0;
  text-align: center;
}
h1, h2, h3 {
  margin: 0;
  color: #1a237e;
}
.dashboard {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 20px;
  margin-top: 20px;
}
.card {
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
}
.chart-container {
  width: 100%;
  height: 400px;
}
.data-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
.data-table th, .data-table td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: left;
}
.data-table th {
  background-color: #e8eaf6;
  font-weight: bold;
}
.data-table tr:nth-child(even) {
  background-color: #f8f8f8;
}
.stock-info {
  background-color: #e8eaf6;
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.stock-price {
  font-size: 24px;
  font-weight: bold;
}
.stock-change {
  font-size: 18px;
  margin-left: 10px;
}
.positive { color: #4caf50; }
.negative { color: #f44336; }
.analysis-section {
  margin-top: 20px;
}
.analysis-section h3 {
  margin-bottom: 10px;
}
.indicator {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}
.indicator-bar {
  height: 20px;
  background-color: #e0e0e0;
  border-radius: 10px;
  overflow: hidden;
}
.indicator-value {
  height: 100%;
  background-color: #4caf50;
}
</style>
</head>
<body>
<header>
  <div class="container">
    <h1>FinViz: AAPL Stock Analysis</h1>
  </div>
</header>
<main class="container">
  <div class="stock-info">
    <h2>Apple Inc. (AAPL)</h2>
    <div>
      <span class="stock-price">$179.36</span>
      <span class="stock-change positive">+2.45 (+1.38%)</span>
    </div>
  </div>
  <div class="dashboard">
    <div class="card">
      <h3>Interactive Stock Chart</h3>
      <div class="chart-container" id="interactive-chart"></div>
    </div>
    <div class="card">
      <h3>Technical Indicators</h3>
      <div class="indicator">
        <span>RSI (14)</span>
        <span>63.24</span>
      </div>
      <div class="indicator-bar">
        <div class="indicator-value" style="width: 63.24%;"></div>
      </div>
      <div class="indicator">
        <span>MACD (12,26,9)</span>
        <span>2.15</span>
      </div>
      <div class="indicator">
        <span>Stochastic %K (14,3,3)</span>
        <span>82.56</span>
      </div>
      <div class="indicator-bar">
        <div class="indicator-value" style="width: 82.56%;"></div>
      </div>
    </div>
  </div>
  <div class="analysis-section">
    <h3>Market Analysis</h3>
    <p>Apple (AAPL) stock has shown strong performance recently, with the price currently trading at $179.36, up 1.38% for the day. The stock has been in an uptrend over the past month, supported by positive sentiment around the company's upcoming product launches and strong services revenue growth.</p>
    <p>The RSI at 63.24 indicates that the stock is approaching overbought territory but still has room for growth. The MACD is positive, suggesting bullish momentum. The high Stochastic %K reading of 82.56 confirms the stock's recent strength but also warns of potential short-term overbought conditions.</p>
    <p>Investors should watch for the upcoming iPhone 15 release and any announcements regarding Apple's AI initiatives, as these could be significant catalysts for future price movements.</p>
  </div>
  <div class="analysis-section">
    <h3>Volume Analysis</h3>
    <table class="data-table">
      <tr>
        <th>Time Frame</th>
        <th>Average Volume</th>
        <th>Current Volume</th>
        <th>Volume Trend</th>
      </tr>
      <tr>
        <td>Daily</td>
        <td>56,234,567</td>
        <td>62,145,890</td>
        <td class="positive">Increasing</td>
      </tr>
      <tr>
        <td>Weekly</td>
        <td>284,567,890</td>
        <td>310,729,450</td>
        <td class="positive">Increasing</td>
      </tr>
      <tr>
        <td>Monthly</td>
        <td>1,235,678,901</td>
        <td>1,242,917,800</td>
        <td>Stable</td>
      </tr>
    </table>
    <p>The increasing daily and weekly volume suggests growing investor interest and supports the current uptrend. This could indicate further potential for price appreciation if the trend continues.</p>
  </div>
</main>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-zoom"></script>
<script>
document.addEventListener('DOMContentLoaded', function() {
  const ctx = document.getElementById('interactive-chart').getContext('2d');
  
  // Simulated stock data for AAPL (6 months of daily data)
  const labels = Array.from({length: 180}, (_, i) => {
    const d = new Date();
    d.setDate(d.getDate() - (180 - i));
    return d.toISOString().split('T')[0];
  });
  
  const generateData = (startPrice, volatility) => {
    let price = startPrice;
    return Array.from({length: 180}, () => {
      price += volatility * (Math.random() - 0.5);
      return price;
    });
  };
  
  const data = generateData(150, 3);
  
  new Chart(ctx, {
    type: 'line',
    data: {
      labels: labels,
      datasets: [{
        label: 'AAPL Stock Price',
        data: data,
        borderColor: 'rgb(75, 192, 192)',
        backgroundColor: 'rgba(75, 192, 192, 0.1)',
        fill: true,
        pointRadius: 0,
        borderWidth: 2
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      scales: {
        x: {
          type: 'time',
          time: {
            unit: 'month'
          }
        },
        y: {
          beginAtZero: false
        }
      },
      plugins: {
        zoom: {
          zoom: {
            wheel: {
              enabled: true,
            },
            pinch: {
              enabled: true
            },
            mode: 'xy',
          },
          pan: {
            enabled: true,
            mode: 'xy',
          }
        }
      }
    }
  });
});
</script>
</body></html>
