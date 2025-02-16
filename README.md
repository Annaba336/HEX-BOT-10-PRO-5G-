const express = require("express");
const fs = require("fs");
const session = require("express-session");

const app = express();
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(session({ secret: "adminSecret", resave: false, saveUninitialized: true }));

// الأكواد المخزنة
let codes = [
    "HEX-1A2B3C", "HEX-4D5E6F", "HEX-7G8H9I", "HEX-J1K2L3",
    "HEX-M4N5O6", "HEX-P7Q8R9", "HEX-ABC123", "HEX-DEF456",
    "HEX-789XYZ", "HEX-654MNO", "HEX-X1Y2Z3", "HEX-9B8C7D"
];

let attempts = {}; // لتتبع محاولات كل IP

// الصفحة الرئيسية (التحقق من الأكواد)
app.get("/", (req, res) => {
    res.send(`
        <html>
        <head>
            <title>التحقق من الكود</title>
            <style>
                body { text-align: center; font-family: Arial; background: #f4f4f4; }
                .container { margin: 100px auto; padding: 20px; width: 300px; background: white; border-radius: 10px; }
                input, button { width: 100%; margin: 5px 0; padding: 10px; }
                button { background: blue; color: white; border: none; }
            </style>
        </head>
        <body>
            <div class="container">
                <h2>أدخل الكود للتحقق</h2>
                <input type="text" id="codeInput" placeholder="أدخل الكود">
                <button onclick="checkCode()">تحقق</button>
                <p id="result"></p>
            </div>
            <script>
                async function checkCode() {
                    const code = document.getElementById("codeInput").value;
                    const response = await fetch("/verify?code=" + code);
                    const result = await response.text();
                    document.getElementById("result").innerText = result;
                }
            </script>
        </body>
        </html>
    `);
});

// التحقق من الأكواد
app.get("/verify", (req, res) => {
    const ip = req.ip;
    const code = req.query.code;

    if (!attempts[ip]) attempts[ip] = 0;
    if (attempts[ip] >= 5) return res.send("❌ تم حظرك بسبب المحاولات الخاطئة المتكررة!");

    if (codes.includes(code)) {
        res.send("✅ الكود صحيح!");
    } else {
        attempts[ip]++;
        fs.appendFileSync("logs.txt", `محاولة فاشلة: ${code} من IP: ${ip}\n`);
        res.send("❌ الكود غير صحيح!");
    }
});

// صفحة تسجيل الدخول للإدارة
app.get("/admin", (req, res) => {
    res.send(`
        <html>
        <head>
            <title>لوحة التحكم</title>
            <style>
                body { text-align: center; font-family: Arial; background: #222; color: white; }
                .container { margin: 100px auto; padding: 20px; width: 300px; background: #333; border-radius: 10px; }
                input, button { width: 100%; margin: 5px 0; padding: 10px; }
                button { background: green; color: white; border: none; }
            </style>
        </head>
        <body>
            <div class="container">
                <h2>تسجيل الدخول</h2>
                <form action="/login" method="POST">
                    <input type="text" name="username" placeholder="اسم المستخدم">
                    <input type="password" name="password" placeholder="كلمة المرور">
                    <button type="submit">تسجيل الدخول</button>
                </form>
            </div>
        </body>
        </html>
    `);
});

// تسجيل الدخول
app.post("/login", (req, res) => {
    if (req.body.username === "admin" && req.body.password === "1234") {
        req.session.admin = true;
        res.redirect("/dashboard");
    } else {
        res.send("❌ بيانات خاطئة!");
    }
});

// لوحة التحكم للإدارة
app.get("/dashboard", (req, res) => {
    if (!req.session.admin) return res.send("❌ غير مصرح لك!");
    
    res.send(`
        <html>
        <head>
            <title>لوحة التحكم</title>
            <style>
                body { text-align: center; font-family: Arial; background: #222; color: white; }
                .container { margin: 100px auto; padding: 20px; width: 400px; background: #333; border-radius: 10px; }
                input, button { width: 100%; margin: 5px 0; padding: 10px; }
                button { background: orange; color: white; border: none; }
            </style>
        </head>
        <body>
            <div class="container">
                <h2>إدارة الأكواد</h2>
                <input type="text" id="newCode" placeholder="أدخل كود جديد">
                <button onclick="addCode()">إضافة كود</button>
                <button onclick="deleteCode()">حذف كود</button>
                <p id="status"></p>
            </div>
            <script>
                async function addCode() {
                    const newCode = document.getElementById("newCode").value;
                    const response = await fetch("/add-code", {
                        method: "POST",
                        headers: { "Content-Type": "application/json" },
                        body: JSON.stringify({ code: newCode })
                    });
                    document.getElementById("status").innerText = await response.text();
                }
                async function deleteCode() {
                    const delCode = document.getElementById("newCode").value;
                    const response = await fetch("/delete-code", {
                        method: "POST",
                        headers: { "Content-Type": "application/json" },
                        body: JSON.stringify({ code: delCode })
                    });
                    document.getElementById("status").innerText = await response.text();
                }
            </script>
        </body>
        </html>
    `);
});

// إضافة كود جديد
app.post("/add-code", (req, res) => {
    if (!req.session.admin) return res.send("❌ غير مصرح لك!");

    const newCode = req.body.code;
    if (!codes.includes(newCode)) {
        codes.push(newCode);
        res.send("✅ تم إضافة الكود!");
    } else {
        res.send("⚠️ الكود موجود مسبقًا!");
    }
});

// حذف كود
app.post("/delete-code", (req, res) => {
    if (!req.session.admin) return res.send("❌ غير مصرح لك!");

    codes = codes.filter(c => c !== req.body.code);
    res.send("✅ تم حذف الكود!");
});

// تشغيل السيرفر
app.listen(3000, () => console.log("🚀 السيرفر يعمل على المنفذ 3000"));
