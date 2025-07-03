
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>تسجيل الدخول - رحلة المهندس المحترف</title>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    body {
      font-family: 'Cairo', sans-serif;
      background: #111;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    form {
      background: #1e1e1e;
      padding: 30px;
      border-radius: 10px;
      width: 100%;
      max-width: 400px;
      box-shadow: 0 0 10px rgba(0,0,0,0.5);
    }

    input {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border-radius: 6px;
      border: none;
      background: #2c2c2c;
      color: #fff;
    }

    button {
      width: 100%;
      padding: 12px;
      background: #ffc107;
      color: #000;
      border: none;
      border-radius: 6px;
      font-weight: bold;
      cursor: pointer;
    }

    a {
      color: #09f;
      text-decoration: none;
    }

    a:hover {
      text-decoration: underline;
    }

    p {
      margin-top: 15px;
      text-align: center;
    }
  </style>
</head>
<body>

  <!-- ✅ مكان إدخال الكود هنا داخل البودي -->
  <form onsubmit="login(event)">
    <input type="text" id="username" placeholder="اسم المستخدم" required />
    <input type="password" id="password" placeholder="كلمة المرور" required />
    <button type="submit">دخول</button>
    <p style="text-align:center">
      <a href="reset.html">هل نسيت كلمة المرور؟</a>
    </p>
  </form>

  <script>
const scriptURL = "https://script.google.com/macros/s/AKfycbw2Ku6QKIpy8KZheZclEvg_tmaElEq-KQCcLy6_5P-vGxPx_8L5CadYGVLA3McYKcKZwQ/exec";

function login(e) {
  e.preventDefault();
  const username = document.getElementById("username").value;
  const password = document.getElementById("password").value;

  fetch(`${scriptURL}?username=${encodeURIComponent(username)}&password=${encodeURIComponent(password)}`)
    .then(res => res.json())
    .then(data => {
      if (data.success) {
        localStorage.setItem("loggedIn", "true");
  localStorage.setItem("courseStartDate", data.startDate);
  localStorage.setItem("studentEmail", data.username); // ✅ مهم جداً
  location.href = data.redirectUrl;
      } else {
        alert("❌ اسم المستخدم أو كلمة المرور غير صحيحة");
      }
    })
    .catch(err => {
      alert("⚠️ حدث خطأ أثناء الاتصال بالخادم");
      console.error(err);
    });
}

  </script>

</body>
</html>
