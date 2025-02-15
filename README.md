<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>HEX BOT 10 PRO 5G</title>
  <style>
    /* RESET بسيط */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: sans-serif;
    }

    body {
      min-height: 100vh;
      background: linear-gradient(90deg, #ff0000, #00ffd0);
      display: flex;
      justify-content: center;
      align-items: center;
    }

    /* حاوية الصفحة بالكامل */
    .container {
      width: 100%;
      max-width: 400px;
      background-color: #222;
      border-radius: 10px;
      padding: 20px;
      color: #fff;
      text-align: center;
    }

    /* عنوان الموقع */
    .container h1 {
      margin-bottom: 20px;
      color: #fff;
    }

    /* قسم تسجيل الدخول */
    #login-section input {
      width: 80%;
      padding: 10px;
      margin-bottom: 15px;
      border: none;
      border-radius: 5px;
      outline: none;
      text-align: center;
    }

    #login-section button {
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      background-color: #e60000;
      color: #fff;
      cursor: pointer;
    }

    #login-section button:hover {
      background-color: #c00000;
    }

    /* قسم لوحة التحكم */
    #dashboard-section {
      display: none; /* مخفي افتراضياً إلى أن يتم التحقق من الكود */
    }

    .grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-top: 20px;
    }

    .grid-item {
      background-color: #333;
      border-radius: 5px;
      padding: 10px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      align-items: center;
      min-height: 80px;
    }

    .grid-item span {
      margin-bottom: 10px;
    }

    .grid-item button {
      border: none;
      border-radius: 5px;
      padding: 6px 10px;
      cursor: pointer;
      background-color: #009900;
      color: #fff;
    }

    .grid-item button:hover {
      background-color: #007700;
    }

    /* رسائل الخطأ */
    .error {
      color: #ff5555;
      margin-bottom: 15px;
    }
  </style>
</head>
<body>

<div class="container">
  <!-- عنوان الموقع -->
  <h1>HEX BOT 10 PRO 5G</h1>

  <!-- قسم تسجيل الدخول -->
  <div id="login-section">
    <p>أدخل كود التفعيل:</p>
    <input type="text" id="activationCode" placeholder="مثال: HEX-1A2B3C" />
    <div id="errorMessage" class="error"></div>
    <button onclick="checkCode()">دخول</button>
  </div>

  <!-- قسم لوحة التحكم بعد تسجيل الدخول -->
  <div id="dashboard-section">
    <h2>لوحة التحكم</h2>
    <div class="grid">
      <div class="grid-item">
        <span>رياكشن النور</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>مشروع تخمين النور</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>دردشة فقر لعب</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>معلومات لعب</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>حماية لفك حظر</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>تحديث السريبات</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>مطور تعليم النور</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>تلقف النشر سبام</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>مطور تعليم البو</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>نشر استيكرات ضحك</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>إرسال رسالة لعب</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>إنشاء حساب لعب</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>بوت ربط الصفحة بلعب</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>الحصول على حساب</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>تفعيل بوت فيسبوك</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>البث في 5 ثواني</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>غلق باب الثغرات</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>مشاركة مع صفحة ثانية</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>تسجيل خروج من الحساب</span>
        <button>تشغيل</button>
      </div>
      <div class="grid-item">
        <span>حذف البوت من التلي</span>
        <button>تشغيل</button>
      </div>
    </div>
  </div>
</div>

<script>
  // قائمة الأكواد الصحيحة
  const validCodes = [
    "HEX-1A2B3C",
    "HEX-4D5E6F",
    "HEX-7G8H9I",
    "HEX-J1K2L3",
    "HEX-M4N5O6",
    "HEX-P7Q8R9",
    "HEX-ABC123",
    "HEX-DEF456",
    "HEX-789XYZ",
    "HEX-654MNO",
    "HEX-X1Y2Z3",
    "HEX-9B8C7D",
    "HEX-3F2E1D",
    "HEX-6H5G4F",
    "HEX-J9K8L7",
    "HEX-M3N2O1",
    "HEX-Q4R5S6",
    "HEX-T7U8V9",
    "HEX-WX1Y2Z",
    "HEX-987ABC"
  ];

  function checkCode() {
    const inputCode = document.getElementById("activationCode").value.trim();
    const errorMessage = document.getElementById("errorMessage");
    if (validCodes.includes(inputCode)) {
      // إخفاء قسم تسجيل الدخول وإظهار لوحة التحكم
      document.getElementById("login-section").style.display = "none";
      document.getElementById("dashboard-section").style.display = "block";
    } else {
      // رسالة خطأ إذا كان الكود غير صحيح
      errorMessage.textContent = "الكود غير صحيح! حاول مرة أخرى.";
    }
  }
</script>

</body>
</html>
