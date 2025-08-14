<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>بطاقة عميل</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #f2f2f2;
    direction: rtl;
    padding: 20px;
  }
  .customer-card {
    background: white;
    padding: 20px;
    border-radius: 10px;
    max-width: 400px;
    margin: auto;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
  }
  .customer-card h3 {
    text-align: center;
    color: #333;
  }
  label {
    display: block;
    margin: 10px 0 5px;
    color: #555;
  }
  input {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  button {
    margin-top: 15px;
    width: 100%;
    padding: 10px;
    border: none;
    background: #4CAF50;
    color: white;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
  }
  button:hover {
    background: #45a049;
  }
</style>
</head>
<body>

<div class="customer-card">
  <h3>بيانات العميل</h3>
  <form id="customerForm">
    <label>الاسم</label>
    <input type="text" name="name" required>
    
    <label>العنوان</label>
    <input type="text" name="address" required>
    
    <label>رقم الهاتف</label>
    <input type="tel" name="phone" required>
    
    <label>البريد الإلكتروني</label>
    <input type="email" name="email" required>
    
    <button type="submit">إرسال</button>
  </form>
</div>

<script>
  const scriptURL = "https://script.google.com/macros/s/AKfycbxM9h_5MD7x8EbBlbSTIZhLnkrZcfReu4ITqDlx8d9CY7bx4Bt3l2A97i5aIZ3w28hPxw/exec"; // الصق الرابط هنا

  document.getElementById("customerForm").addEventListener("submit", function(e) {
    e.preventDefault();

    const formData = {
      name: this.name.value,
      address: this.address.value,
      phone: this.phone.value,
      email: this.email.value
    };

    fetch(scriptURL, {
      method: 'POST',
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(formData)
    })
    .then(res => res.json())
    .then(data => {
      if (data.status === "success") {
        alert("✅ تم إرسال البيانات بنجاح");
        this.reset();
      } else {
        alert("❌ خطأ: " + (data.message || "تعذر الإرسال"));
      }
    })
    .catch(err => {
      console.error(err);
      alert("❌ تعذر الاتصال بالسيرفر");
    });
  });
</script>

</body>
</html>
