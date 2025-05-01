<!DOCTYPE html>
<html>
<head>
  <title>Farming Cost Calculator<br>Deborah farm</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: #f4f4f4;
    }
    .container {
      max-width: 400px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    input {
      width: 100%;
      padding: 8px;
      margin: 8px 0;
    }
    button {
      padding: 10px;
      width: 100%;
      background: green;
      color: white;
      border: none;
      border-radius: 5px;
    }
    #total {
      margin-top: 15px;
      font-size: 18px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Farming Cost Calculator</h2>
    <label>Seeds (KES):</label>
    <input type="number" id="seeds" placeholder="e.g. 2000">
    
    <label>Fertilizer (KES):</label>
    <input type="number" id="fertilizer" placeholder="e.g. 1500">
    
    <label>Labor (KES):</label>
    <input type="number" id="labor" placeholder="e.g. 3000">
    
    <label>Transport (KES):</label>
    <input type="number" id="transport" placeholder="e.g. 1000">

    <label>Other (KES):</label>
    <input type="number" id="other" placeholder="e.g. 500">

    <button onclick="calculateTotal()">Calculate Total Cost</button>
    <div id="total">Total: KES 0</div>
  </div>

  <script>
    function calculateTotal() {
      const seeds = parseFloat(document.getElementById('seeds').value) || 0;
      const fertilizer = parseFloat(document.getElementById('fertilizer').value) || 0;
      const labor = parseFloat(document.getElementById('labor').value) || 0;
      const transport = parseFloat(document.getElementById('transport').value) || 0;
      const other = parseFloat(document.getElementById('other').value) || 0;

      const total = seeds + fertilizer + labor + transport + other;

      document.getElementById('total').innerText = `Total: KES ${total.toLocaleString()}`;
    }
  </script>
</body>
</html>
