Powered by Abicheru Technologies 
<html>
<head>
  <title>Deborah farm Farming Cost Calculator</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: #f4f4f4;
    }
    .container {
      max-width: 500px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    input, button {
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      box-sizing: border-box;
    }
    button {
      background: green;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background: darkgreen;
    }
    #categories input {
      margin-top: 5px;
    }
    .row {
      display: flex;
      gap: 10px;
    }
    .row input {
      flex: 1;
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

    <div class="row">
      <input type="text" id="newCategoryName" placeholder="Enter category name (e.g. Seeds)">
      <button onclick="addCategory()">Add Category</button>
    </div>

    <div id="categories"></div>

    <button onclick="calculateTotal()">Calculate Total Cost</button>
    <div id="total">Total: KES 0</div>
    <button onclick="exportPDF()">Export as PDF</button>
  </div>

  <script>
    let lastTotal = 0;

    function addCategory() {
      const name = document.getElementById('newCategoryName').value.trim();
      if (!name) return;

      const container = document.createElement('div');
      container.className = 'row';
      container.innerHTML = `
        <input type="text" value="${name}" disabled>
        <input type="number" placeholder="KES 0" data-name="${name}" class="amount">
      `;
      document.getElementById('categories').appendChild(container);

      document.getElementById('newCategoryName').value = '';
    }

    function calculateTotal() {
      const amountFields = document.querySelectorAll('.amount');
      let total = 0;

      amountFields.forEach(field => {
        total += parseFloat(field.value) || 0;
      });

      lastTotal = total;
      document.getElementById('total').innerText = `Total: KES ${total.toLocaleString()}`;
    }

    async function exportPDF() {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();

      doc.text("Farming Cost Summary", 20, 20);
      const amountFields = document.querySelectorAll('.amount');

      let y = 40;
      amountFields.forEach(field => {
        const name = field.dataset.name;
        const value = parseFloat(field.value) || 0;
        doc.text(`${name}: KES ${value.toLocaleString()}`, 20, y);
        y += 10;
      });

      doc.text(`Total Cost: KES ${lastTotal.toLocaleString()}`, 20, y + 10);
      doc.save("Farming_Cost_Summary.pdf");
    }
  </script>
</body>
</html>
