<!DOCTYPE html>
<html>
<head>
  <title>Farming Cost Calculator<br> Deborah Farm </title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
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
      margin-top: 10px;
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
    <button onclick="exportPDF()">Export as PDF</button>
  </div>

  <script>
    let lastTotal = 0;

    function calculateTotal() {
      const seeds = parseFloat(document.getElementById('seeds').value) || 0;
      const fertilizer = parseFloat(document.getElementById('fertilizer').value) || 0;
      const labor = parseFloat(document.getElementById('labor').value) || 0;
      const transport = parseFloat(document.getElementById('transport').value) || 0;
      const other = parseFloat(document.getElementById('other').value) || 0;

      const total = seeds + fertilizer + labor + transport + other;
      lastTotal = total;

      document.getElementById('total').innerText = `Total: KES ${total.toLocaleString()}`;
    }

    async function exportPDF() {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();

      const seeds = document.getElementById('seeds').value || 0;
      const fertilizer = document.getElementById('fertilizer').value || 0;
      const labor = document.getElementById('labor').value || 0;
      const transport = document.getElementById('transport').value || 0;
      const other = document.getElementById('other').value || 0;

      doc.text("Farming Cost Summary", 20, 20);
      doc.text(`Seeds: KES ${seeds}`, 20, 40);
      doc.text(`Fertilizer: KES ${fertilizer}`, 20, 50);
      doc.text(`Labor: KES ${labor}`, 20, 60);
      doc.text(`Transport: KES ${transport}`, 20, 70);
      doc.text(`Other: KES ${other}`, 20, 80);
      doc.text(`Total Cost: KES ${lastTotal.toLocaleString()}`, 20, 100);

      doc.save("Farming_Cost_Summary.pdf");
    }
  </script>
</body>
</html>
