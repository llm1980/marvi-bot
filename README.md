[webapp_test (1).html](https://github.com/user-attachments/files/29435656/webapp_test.1.html)
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>تست Web App — حوزه علمیه مروی</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --green:   #2D6A4F;
    --green2:  #40916C;
    --gold:    #B7950B;
    --bg:      #F8F6F0;
    --card:    #FFFFFF;
    --text:    #1A1A1A;
    --muted:   #6B7280;
    --border:  #E5E0D5;
    --radius:  12px;
  }

  body {
    font-family: 'Segoe UI', Tahoma, sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    padding: 16px;
    direction: rtl;
  }

  /* هدر */
  .header {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 16px;
    background: var(--green);
    border-radius: var(--radius);
    margin-bottom: 20px;
    color: white;
  }

  .header-logo {
    width: 48px;
    height: 48px;
    background: rgba(255,255,255,0.2);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    flex-shrink: 0;
  }

  .header-text h1 {
    font-size: 16px;
    font-weight: 700;
  }

  .header-text p {
    font-size: 12px;
    opacity: 0.8;
    margin-top: 2px;
  }

  /* کارت */
  .card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 16px;
    margin-bottom: 14px;
  }

  .card-title {
    font-size: 13px;
    color: var(--muted);
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  /* انتخاب نوع سوال */
  .type-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .type-btn {
    border: 2px solid var(--border);
    border-radius: 10px;
    padding: 14px 10px;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s;
    background: white;
    font-size: 13px;
    color: var(--text);
  }

  .type-btn .icon { font-size: 24px; display: block; margin-bottom: 6px; }
  .type-btn.selected {
    border-color: var(--green);
    background: #F0F9F4;
    color: var(--green);
    font-weight: 600;
  }

  /* مرجع تقلید */
  .marja-list { display: flex; flex-direction: column; gap: 8px; }

  .marja-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px;
    border: 2px solid var(--border);
    border-radius: 10px;
    cursor: pointer;
    transition: all 0.2s;
  }

  .marja-item.selected {
    border-color: var(--green);
    background: #F0F9F4;
  }

  .marja-radio {
    width: 20px; height: 20px;
    border: 2px solid var(--border);
    border-radius: 50%;
    flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
  }

  .marja-item.selected .marja-radio {
    border-color: var(--green);
    background: var(--green);
  }

  .marja-item.selected .marja-radio::after {
    content: '';
    width: 8px; height: 8px;
    background: white;
    border-radius: 50%;
  }

  .marja-name { font-size: 14px; }

  /* textarea */
  textarea {
    width: 100%;
    border: 2px solid var(--border);
    border-radius: 10px;
    padding: 12px;
    font-size: 14px;
    font-family: inherit;
    resize: none;
    height: 110px;
    direction: rtl;
    transition: border-color 0.2s;
    background: white;
    color: var(--text);
  }

  textarea:focus {
    outline: none;
    border-color: var(--green);
  }

  .char-count {
    text-align: left;
    font-size: 11px;
    color: var(--muted);
    margin-top: 6px;
  }

  /* دکمه ارسال */
  .submit-btn {
    width: 100%;
    padding: 16px;
    background: var(--green);
    color: white;
    border: none;
    border-radius: var(--radius);
    font-size: 15px;
    font-weight: 700;
    cursor: pointer;
    transition: background 0.2s;
    font-family: inherit;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 6px;
  }

  .submit-btn:hover { background: var(--green2); }
  .submit-btn:disabled { background: var(--muted); cursor: not-allowed; }

  /* toast */
  .toast {
    position: fixed;
    bottom: 20px;
    right: 16px; left: 16px;
    background: var(--green);
    color: white;
    padding: 14px 16px;
    border-radius: var(--radius);
    font-size: 14px;
    text-align: center;
    transform: translateY(80px);
    opacity: 0;
    transition: all 0.3s ease;
    z-index: 999;
  }

  .toast.show { transform: translateY(0); opacity: 1; }

  /* web app info */
  .info-box {
    background: #FFF8E1;
    border: 1px solid #F9C74F;
    border-radius: 10px;
    padding: 12px;
    font-size: 12px;
    color: #7D5A00;
    margin-bottom: 14px;
    line-height: 1.6;
  }
</style>
</head>
<body>

<div class="header">
  <div class="header-logo">🕌</div>
  <div class="header-text">
    <h1>حوزه علمیه مروی</h1>
    <p>سامانه پاسخگویی شرعی</p>
  </div>
</div>

<div class="info-box">
  🧪 این یک صفحه تست است — بررسی سازگاری Web App با بله
</div>

<!-- نوع سوال -->
<div class="card">
  <div class="card-title">📂 نوع درخواست را انتخاب کنید</div>
  <div class="type-grid">
    <div class="type-btn" onclick="selectType(this, 'religious')">
      <span class="icon">📖</span>سوال شرعی
    </div>
    <div class="type-btn" onclick="selectType(this, 'ladies')">
      <span class="icon">🧕</span>احکام بانوان
    </div>
    <div class="type-btn" onclick="selectType(this, 'wujuhat')">
      <span class="icon">💰</span>وجوهات شرعی
    </div>
    <div class="type-btn" onclick="selectType(this, 'istikharah')">
      <span class="icon">📿</span>استخاره
    </div>
  </div>
</div>

<!-- مرجع تقلید -->
<div class="card" id="marja-card" style="display:none">
  <div class="card-title">👤 مرجع تقلید</div>
  <div class="marja-list">
    <div class="marja-item" onclick="selectMarja(this, 'خامنه‌ای')">
      <div class="marja-radio"></div>
      <span class="marja-name">آیت‌الله خامنه‌ای</span>
    </div>
    <div class="marja-item" onclick="selectMarja(this, 'سیستانی')">
      <div class="marja-radio"></div>
      <span class="marja-name">آیت‌الله سیستانی</span>
    </div>
    <div class="marja-item" onclick="selectMarja(this, 'مکارم شیرازی')">
      <div class="marja-radio"></div>
      <span class="marja-name">آیت‌الله مکارم شیرازی</span>
    </div>
    <div class="marja-item" onclick="selectMarja(this, 'وحید خراسانی')">
      <div class="marja-radio"></div>
      <span class="marja-name">آیت‌الله وحید خراسانی</span>
    </div>
  </div>
</div>

<!-- متن سوال -->
<div class="card" id="question-card" style="display:none">
  <div class="card-title">✍️ سوال خود را بنویسید</div>
  <textarea id="question-text"
    placeholder="سوال خود را با جزئیات کامل بنویسید..."
    maxlength="2000"
    oninput="updateCount(this)"></textarea>
  <div class="char-count"><span id="char-num">0</span> / 2000</div>
</div>

<button class="submit-btn" id="submit-btn" onclick="submitForm()" disabled>
  ارسال درخواست
</button>

<div class="toast" id="toast">✅ درخواست شما با موفقیت ثبت شد</div>

<script>
  let selectedType = null;
  let selectedMarja = null;

  // اتصال به Bale WebApp API
  const tg = window.Telegram?.WebApp || window.Bale?.WebApp || null;
  if (tg) {
    tg.ready();
    tg.expand();
  }

  function selectType(el, type) {
    document.querySelectorAll('.type-btn').forEach(b => b.classList.remove('selected'));
    el.classList.add('selected');
    selectedType = type;

    const needsMarja = ['religious', 'ladies'].includes(type);
    document.getElementById('marja-card').style.display = needsMarja ? 'block' : 'none';
    document.getElementById('question-card').style.display = 'block';
    checkReady();
  }

  function selectMarja(el, marja) {
    document.querySelectorAll('.marja-item').forEach(b => b.classList.remove('selected'));
    el.classList.add('selected');
    selectedMarja = marja;
    checkReady();
  }

  function updateCount(el) {
    document.getElementById('char-num').textContent = el.value.length;
    checkReady();
  }

  function checkReady() {
    const q = document.getElementById('question-text').value.trim();
    const needsMarja = ['religious', 'ladies'].includes(selectedType);
    const ok = selectedType && q.length >= 10 && (!needsMarja || selectedMarja);
    document.getElementById('submit-btn').disabled = !ok;
  }

  function submitForm() {
    const q = document.getElementById('question-text').value.trim();
    const data = {
      type:      selectedType,
      reference: selectedMarja,
      question:  q
    };

    // ارسال به ربات
    if (tg) {
      tg.sendData(JSON.stringify(data));
    } else {
      // حالت تست بدون ربات
      const toast = document.getElementById('toast');
      toast.classList.add('show');
      setTimeout(() => toast.classList.remove('show'), 3000);
      console.log('data:', data);
    }
  }
</script>
</body>
</html>
