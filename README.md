<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ödeme Sayfası - Temel Paket</title>
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

        .loading-spinner {
            display: none;
            margin-top: 20px;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #3498db;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 2s linear infinite;
        }

        .success-check {
            display: none;
            font-size: 50px;
            color: green;
            margin: 20px 0;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="payment-container">
        <div class="alert" id="alertBox">Lütfen geçerli bilgiler girin!</div>
        <h2>Ödeme Bilgilerinizi Girin</h2>
        <div class="package-info">600 TL Temel Paket</div>
        <form id="paymentForm" onsubmit="return validateForm()">
            <input type="hidden" id="package" value="600">

            <label>Paket Dili Seçin</label>
            <select id="language">
                <option value="tr">Türkçe</option>
                <option value="en">English</option>
            </select>

            <label>Altyazı Dili Seçin</label>
            <select id="subtitleLanguage">
                <option value="tr">Türkçe</option>
                <option value="en">English</option>
            </select>

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

        <div class="loading-spinner" id="loadingSpinner"></div>
        <div class="success-check" id="successCheck">&#10004;</div>
    </div>

    <script>
        function validateForm() {
            let isValid = true;

            const email = document.getElementById("email").value;
            const phone = document.getElementById("phone").value;
            const card = document.getElementById("card").value;
            const expiry = document.getElementById("expiry").value;
            const cvv = document.getElementById("cvv").value;

            const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

            if (!emailPattern.test(email)) {
                document.getElementById("emailError").style.display = "block";
                isValid = false;
            } else {
                document.getElementById("emailError").style.display = "none";
            }

            const phonePattern = /^05\d{2} \d{3} \d{2} \d{2}$/;
            if (!phonePattern.test(phone)) {
                document.getElementById("phoneError").style.display = "block";
                isValid = false;
            } else {
                document.getElementById("phoneError").style.display = "none";
            }

            const cardPattern = /^\d{16}$/;
            if (!cardPattern.test(card)) {
                document.getElementById("cardError").style.display = "block";
                isValid = false;
            } else {
                document.getElementById("cardError").style.display = "none";
            }

            const expiryPattern = /^(0[1-9]|1[0-2])\/\d{2}$/;
            if (!expiryPattern.test(expiry)) {
                document.getElementById("expiryError").style.display = "block";
                isValid = false;
            } else {
                document.getElementById("expiryError").style.display = "none";
            }

            const cvvPattern = /^\d{3}$/;
            if (!cvvPattern.test(cvv)) {
                document.getElementById("cvvError").style.display = "block";
                isValid = false;
            } else {
                document.getElementById("cvvError").style.display = "none";
            }

            return isValid;
        }
    </script>
</body>
</html>
