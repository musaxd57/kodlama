<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ödeme Sayfası - 600 TL Temel Paket</title>
    <link rel="stylesheet" href="style.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .payment-container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
            width: 350px;
        }

        h2 {
            text-align: center;
        }

        .package-info {
            text-align: center;
            font-weight: bold;
            margin: 10px 0;
            color: #333;
        }

        form {
            display: flex;
            flex-direction: column;
        }

        label {
            margin-top: 10px;
            font-weight: bold;
        }

        input, select {
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .error {
            color: red;
            font-size: 14px;
            display: none;
        }

        .alert {
            display: none;
            color: white;
            background: red;
            padding: 10px;
            text-align: center;
            margin-bottom: 10px;
            border-radius: 5px;
        }

        button {
            margin-top: 15px;
            padding: 12px;
            background-color: #FF9800;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            cursor: pointer;
        }

        button:hover {
            background-color: #E68900;
        }
    </style>
</head>
<body>
    <div class="payment-container">
        <div class="alert" id="alertBox">Lütfen geçerli bilgiler girin!</div>
        <h2>Ödeme Bilgilerinizi Girin</h2>
        <div class="package-info">800 TL Standart Paket</div>
        <form id="paymentForm" onsubmit="return validateForm()">
            <input type="hidden" id="package" value="800">

            <label>E-Posta</label>
            <input type="email" id="email" placeholder="example@mail.com" required>
            <span class="error" id="emailError">Geçerli bir e-posta girin.</span>
            
            <label>Telefon Numarası</label>
            <input type="tel" id="phone" placeholder="05XX XXX XX XX" required>
            <span class="error" id="phoneError">Geçerli bir telefon numarası girin.</span>

            <label>Kart Numarası</label>
            <input type="text" id="card" placeholder="1234 5678 9101 1121" maxlength="16" required>
            <span class="error" id="cardError">Geçerli bir 16 haneli kart numarası girin.</span>

            <label>Son Kullanma Tarihi</label>
            <input type="text" id="expiry" placeholder="MM/YY" maxlength="5" required>
            <span class="error" id="expiryError">Geçerli bir son kullanma tarihi girin.</span>

            <label>CVV</label>
            <input type="password" id="cvv" placeholder="123" maxlength="3" required>
            <span class="error" id="cvvError">Geçerli bir 3 haneli CVV girin.</span>

            <label>Ad Soyad</label>
            <input type="text" id="name" placeholder="Kart Üzerindeki Ad Soyad" required>

            <button type="submit">Ödemeyi Tamamla</button>
        </form>
    </div>
</body>
</html>

