<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ödeme Sayfası</title>
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
            background: green;
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
    <h2>Ödeme Sayfası - Temel Paket</h2>
    <form onsubmit="return validateForm()">
        <label for="package">Paket Seçimi</label>
        <input type="text" id="package" name="package" value="Temel Paket - 600 TL" disabled>

        <label for="expiry">Son Kullanma Tarihi (MM/YY)</label>
        <input type="text" id="expiry" name="expiry" placeholder="MM/YY">

        <div id="expiryError" class="error"></div>

        <div id="successAlert" class="alert">Ödeme Başarılı! Onaylandı ✅</div>
        
        <button type="submit">Ödemeyi Tamamla</button>
    </form>
</div>

<script>
    function validateForm() {
        let isValid = true;
        const expiry = document.getElementById("expiry").value.trim();
        const expiryPattern = /^(0[1-9]|1[0-2])\/(\d{2})$/;
        const [month, year] = expiry.split('/');
        const currentDate = new Date();
        const currentMonth = currentDate.getMonth() + 1;
        const currentYear = currentDate.getFullYear();
        
        if (expiryPattern.test(expiry)) {
            if (parseInt(month) < 1 || parseInt(month) > 12) {
                document.getElementById("expiryError").innerText = "Ay, 01 ile 12 arasında olmalı.";
                document.getElementById("expiryError").style.display = "block";
                document.getElementById("successAlert").style.display = "none";
                isValid = false;
            } else if (parseInt(year) < currentYear % 100 || parseInt(year) > currentYear % 100 + 35) {
                document.getElementById("expiryError").innerText = "Yıl, mevcut yıldan 35 yıl daha ileri olmalı.";
                document.getElementById("expiryError").style.display = "block";
                document.getElementById("successAlert").style.display = "none";
                isValid = false;
            } else if (parseInt(year) == currentYear % 100 && parseInt(month) < currentMonth) {
                document.getElementById("expiryError").innerText = "Son kullanma tarihi geçerli değil.";
                document.getElementById("expiryError").style.display = "block";
                document.getElementById("successAlert").style.display = "none";
                isValid = false;
            } else {
                document.getElementById("expiryError").style.display = "none";
            }
        } else {
            document.getElementById("expiryError").innerText = "Geçerli bir tarih girin (MM/YY).";
            document.getElementById("expiryError").style.display = "block";
            document.getElementById("successAlert").style.display = "none";
            isValid = false;
        }

        if (isValid) {
            document.getElementById("successAlert").style.display = "block";
        }

        return isValid;
    }
</script>

</body>
</html>
