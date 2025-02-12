<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ödeme Sayfası - 600 TL Paket</title>
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
            text-align: center;
        }
        h2 {
            margin-bottom: 20px;
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
        .error-alert {
            display: none;
            color: white;
            background: red;
            padding: 10px;
            text-align: center;
            margin-bottom: 10px;
            border-radius: 5px;
        }
        .success-check {
            display: none;
            font-size: 50px;
            color: green;
            margin: 20px 0;
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
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>

    <div class="payment-container">
        <h2>600 TL Temel Paket</h2>
        <form id="paymentForm" onsubmit="return validateForm()">
            <label for="expiry">Son Kullanma Tarihi (MM/YY):</label>
            <input type="text" id="expiry" name="expiry" placeholder="MM/YY" required>
            <div class="error" id="expiryError"></div>

            <div class="alert" id="successAlert">Ödeme Başarılı!</div>
            <div class="error-alert" id="errorAlert">Ödeme sırasında bir hata oluştu. Lütfen tekrar deneyin.</div>

            <button type="submit">Ödemeyi Tamamla</button>
        </form>

        <div class="loading-spinner" id="loadingSpinner"></div>

        <div class="success-check" id="successCheck">&#10004;</div>
    </div>

    <script>
        function validateForm() {
            let isValid = true;
            const expiry = document.getElementById("expiry").value.trim();
            const expiryPattern = /^(0[1-9]|1[0-2])\/(\d{2})$/; // MM/YY format
            const [month, year] = expiry.split('/');  // MM ve YY'yi ayırıyoruz
            const currentDate = new Date();
            const currentMonth = currentDate.getMonth() + 1; // Aylar 0-11 arasında, bu yüzden +1 ekliyoruz
            const currentYear = currentDate.getFullYear(); // Tam yıl alıyoruz (2025 gibi)

            // Son Kullanma Tarihi Kontrolü
            if (expiryPattern.test(expiry)) {
                if (parseInt(month) < 1 || parseInt(month) > 12) {
                    document.getElementById("expiryError").innerText = "Ay, 01 ile 12 arasında olmalı.";
                    document.getElementById("expiryError").style.display = "block";
                    isValid = false;
                } else if (parseInt(year) < currentYear % 100 || parseInt(year) > currentYear % 100 + 40) {
                    document.getElementById("expiryError").innerText = "Yıl, mevcut yıldan 40 yıl daha ileri olmalı.";
                    document.getElementById("expiryError").style.display = "block";
                    isValid = false;
                } else if (parseInt(year) == currentYear % 100 && parseInt(month) < currentMonth) {
                    document.getElementById("expiryError").innerText = "Son kullanma tarihi geçerli değil.";
                    document.getElementById("expiryError").style.display = "block";
                    isValid = false;
                } else {
                    document.getElementById("expiryError").style.display = "none";
                }
            } else {
                document.getElementById("expiryError").innerText = "Geçerli bir tarih girin (MM/YY).";
                document.getElementById("expiryError").style.display = "block";
                isValid = false;
            }

            if (isValid) {
                // Loading Spinner'ı gösteriyoruz
                document.getElementById("loadingSpinner").style.display = "block";

                // Başarı mesajı ve tik işaretini gösteriyoruz
                setTimeout(function() {
                    document.getElementById("successAlert").style.display = "block";
                    document.getElementById("successCheck").style.display = "inline-block"; // Tik işareti
                    document.getElementById("loadingSpinner").style.display = "none";
                }, 2000); // 2 saniye sonra başarı mesajı gösterilir
            } else {
                // Hata mesajı göster
                document.getElementById("errorAlert").style.display = "block";
            }

            return isValid;
        }
    </script>

</body>
</html>
