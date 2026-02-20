<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fresh & Blend Juice Bar</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #e8f5e9; display: flex; justify-content: center; padding: 20px; }
        .card { background: white; padding: 25px; border-radius: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); width: 100%; max-width: 400px; text-align: center; }
        h2 { color: #2e7d32; margin-bottom: 5px; }
        .tagline { color: #666; font-size: 0.9em; margin-bottom: 20px; }
        .menu-item { display: flex; justify-content: space-between; align-items: center; padding: 15px; margin: 10px 0; border: 1px solid #eee; border-radius: 10px; cursor: pointer; transition: 0.3s; }
        .menu-item:hover { border-color: #4caf50; background: #f9fff9; transform: scale(1.02); }
        .active { border: 2px solid #2e7d32; background: #f0fff0; }
        .total-box { margin-top: 20px; padding: 15px; background: #2e7d32; color: white; border-radius: 10px; font-size: 1.2em; }
        .qr-section { margin-top: 20px; display: none; border-top: 1px solid #eee; pt: 15px; }
        .qr-section img { width: 150px; height: 150px; margin-top: 10px; }
        .btn { width: 100%; padding: 15px; background: #1b5e20; color: white; border: none; border-radius: 10px; font-weight: bold; margin-top: 15px; cursor: pointer; font-size: 1em; }
    </style>
</head>
<body>

<div class="card">
    <h2>🥤 Fresh & Blend</h2>
    <p class="tagline">Select your flavor to start order</p>
    
    <div onclick="updateOrder(this, 'Avocado 🥑', 100)" class="menu-item"><span>Avocado 🥑</span> <b>100/-</b></div>
    <div onclick="updateOrder(this, 'Watermelon 🍉', 100)" class="menu-item"><span>Watermelon 🍉</span> <b>100/-</b></div>
    <div onclick="updateOrder(this, 'VimSprite 🍓', 100)" class="menu-item"><span>VimSprite 🍓</span> <b>100/-</b></div>
    <div onclick="updateOrder(this, 'Avo-Melon 🥑🍉', 150)" class="menu-item"><span>Avo-Melon 🥑🍉</span> <b>150/-</b></div>

    <div class="total-box">
        Total: <span id="display-price">0</span> Ksh
    </div>

    <button class="btn" onclick="initiateSTK()">PAY VIA M-PESA STK</button>

    <div id="qr-area" class="qr-section">
        <p style="font-size: 0.8em; color: #555;">Or Scan Till Number to Pay:</p>
        <img id="qr-code" src="" alt="M-Pesa QR">
        <p><strong>Till: 555 444</strong></p>
    </div>
</div>

<script>
    let selectedPrice = 0;
    let selectedItem = "";
    const tillNumber = "555444"; // Replace with your actual Till

    function updateOrder(element, name, price) {
        // Reset styles
        document.querySelectorAll('.menu-item').forEach(item => item.classList.remove('active'));
        // Highlight selection
        element.classList.add('active');
        
        selectedPrice = price;
        selectedItem = name;
        document.getElementById('display-price').innerText = price;
        
        // Update QR Code dynamically with the price
        const qrUrl = `https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl=MPESA|BUYGOODS|${tillNumber}|${price}`;
        document.getElementById('qr-code').src = qrUrl;
        document.getElementById('qr-area').style.display = "block";
    }

    function initiateSTK() {
        if(selectedPrice === 0) {
            alert("Please pick a juice first!");
            return;
        }
        const phone = prompt("Enter phone (2547...):", "254");
        if(phone) {
            alert("Sending STK Push for " + selectedPrice + " Ksh to " + phone + "...");
            // Here you would call your Python backend /pay route
        }
    }
</script>

</body>
</html>
