<!-- صفحة تسجيل دخول بسيطة -->
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>تسجيل دخول المتدربين</title>
  <style>
    body {
      font-family: 'Cairo', sans-serif;
      background-color: #111;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .login-container {
      background-color: #222;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
      max-width: 400px;
      width: 100%;
    }
    h2 {
      text-align: center;
      margin-bottom: 20px;
    }
    input {
      width: 100%;
      padding: 10px;
      margin-bottom: 15px;
      border: none;
      border-radius: 8px;
      background-color: #333;
      color: #fff;
    }
    button {
      width: 100%;
      padding: 12px;
      background-color: #ffc107;
      color: #000;
      border: none;
      border-radius: 8px;
      font-weight: bold;
      cursor: pointer;
    }
    .error {
      color: red;
      margin-bottom: 10px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="login-container">
    <h2>تسجيل الدخول</h2>
    <div class="error" id="error"></div>
    <input type="text" id="username" placeholder="اسم المستخدم">
    <input type="password" id="password" placeholder="كلمة المرور">
    <button onclick="login()">دخول</button>
  </div>

  <script>
    async function login() {
      const username = document.getElementById("username").value;
      const password = document.getElementById("password").value;
      const error = document.getElementById("error");

      if (!username || !password) {
        error.textContent = "يرجى إدخال اسم المستخدم وكلمة المرور";
        return;
      }

      // Google Apps Script endpoint
      const url = "https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec?username=" + encodeURIComponent(username) + "&password=" + encodeURIComponent(password);

      try {
        const res = await fetch(url);
        const result = await res.json();

        if (result.success) {
          window.location.href = result.redirectUrl; // مثل صفحة الدورة التدريبية
        } else {
          error.textContent = "اسم المستخدم أو كلمة المرور غير صحيحة";
        }
      } catch (err) {
        error.textContent = "حدث خطأ أثناء الاتصال بالخادم";
      }
    }
  </script>
</body>
</html>
