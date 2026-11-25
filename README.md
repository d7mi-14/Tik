
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>TikTok Report Manager</title>
<style>
*{box-sizing:border-box}
body{
  margin:0;
  background:#090a10;
  color:#fff;
  font-family:Arial,sans-serif;
  padding:25px 15px;
}
.container{
  max-width:480px;
  margin:30px auto;
  background:#151621;
  padding:25px;
  border-radius:18px;
  border:1px solid #292a38;
}
h2{text-align:center;margin-top:0}
.sub{text-align:center;color:#888;font-size:13px}
label{display:block;margin:18px 0 8px}
input,select,textarea{
  width:100%;
  padding:13px;
  border-radius:9px;
  border:1px solid #343544;
  background:#0d0e16;
  color:white;
  outline:none;
  font-size:14px;
}
textarea{resize:vertical;min-height:100px}
button{
  width:100%;
  padding:14px;
  margin-top:15px;
  border:0;
  border-radius:9px;
  background:#fe2c55;
  color:white;
  font-size:15px;
  font-weight:bold;
  cursor:pointer;
}
button:hover{opacity:.85}
.result{
  margin-top:20px;
  padding:15px;
  border-radius:10px;
  background:#0d0e16;
  display:none;
  white-space:pre-wrap;
  line-height:1.8;
}
.footer{
  text-align:center;
  color:#666;
  font-size:11px;
  margin-top:22px;
}
</style>
</head>
<body>

<div class="container">
  <h2>🎵 TikTok Report Manager</h2>
  <p class="sub">أداة تجهيز وإدارة بلاغات TikTok</p>

  <label>رابط الحساب أو الفيديو</label>
  <input id="url" type="url"
  placeholder="https://www.tiktok.com/@username">

  <label>نوع البلاغ</label>
  <select id="type">
    <option value="Spam">إزعاج أو محتوى مزعج</option>
    <option value="Harassment">تنمر ومضايقة</option>
    <option value="Hate speech">خطاب كراهية</option>
    <option value="Violence">عنف وتهديدات</option>
    <option value="Impersonation">انتحال شخصية</option>
    <option value="Misinformation">معلومات مضللة</option>
    <option value="Other">سبب آخر</option>
  </select>

  <label>تفاصيل المخالفة</label>
  <textarea id="details"
  placeholder="اشرح سبب البلاغ وأرفق وصف الأدلة..."></textarea>

  <button onclick="generate()">تجهيز البلاغ</button>
  <button onclick="copyReport()" style="background:#292a38">
    نسخ البلاغ
  </button>

  <div class="result" id="result"></div>

  <p class="footer">
    TikTok Report Manager | Version 1.0
  </p>
</div>

<script>
let report = "";

function generate(){
  const url = document.getElementById("url").value.trim();
  const type = document.getElementById("type").value;
  const details = document.getElementById("details").value.trim();

  if(!url){
    alert("أدخل رابط الحساب أو الفيديو");
    return;
  }

  try {
    const parsed = new URL(url);
    if(!["tiktok.com","www.tiktok.com","m.tiktok.com"].includes(parsed.hostname)){
      alert("أدخل رابط TikTok صحيحاً");
      return;
    }
  } catch(e) {
    alert("الرابط غير صالح");
    return;
  }

  report =
`TikTok Report
----------------
Target: ${url}
Report Type: ${type}
Details: ${details || "No additional details"}
----------------
Prepared for manual review.`;

  document.getElementById("result").style.display="block";
  document.getElementById("result").textContent=report;
}

async function copyReport(){
  if(!report){
    alert("جهّز البلاغ أولاً");
    return;
  }
  try{
    await navigator.clipboard.writeText(report);
    alert("تم نسخ البلاغ");
  }catch(e){
    alert("تعذر النسخ، تحقق من صلاحية المتصفح");
  }
}
</script>

</body>
</html>
