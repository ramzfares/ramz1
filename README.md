<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>الباحث في رموز القبائل</title>
  <!-- خط IBM Plex Sans Arabic -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Arabic:wght@400;700&display=swap" rel="stylesheet" />
  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.4.0/css/all.min.css" />
  <style>
    /* تأثيرات الانتقال (Fade) */
    body {
      opacity: 1;
      transition: opacity 0.5s ease;
    }
    body.fade-out {
      opacity: 0;
    }
    /* القواعد العامة */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: "IBM Plex Sans Arabic", sans-serif;
    }
    body {
      background: linear-gradient(135deg, #FAF3E0, #F2E8D5);
      color: #5C4033;
      direction: rtl;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      line-height: 1.6;
      text-align: center;
    }
    a {
      text-decoration: none;
      color: inherit;
    }
    h1, h2, h3, h4, h5, h6 {
      color: #3E2723;
    }
    /* الهيدر */
    header {
      background-color: #8B4513;
      color: #fff;
      padding: 15px 20px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-direction: row-reverse;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
      position: relative;
      z-index: 10;
    }
    .logo {
      height: 50px;
      filter: brightness(0) invert(1);
    }
    .hamburger {
      font-size: 24px;
      cursor: pointer;
      color: #fff;
      padding: 8px;
      border-radius: 6px;
      transition: background-color 0.3s;
    }
    .hamburger.active {
      background-color: rgba(255, 255, 255, 0.2);
    }
    /* القائمة الجانبية */
    #sidebar {
      position: fixed;
      top: 0;
      left: 0;
      transform: translateX(-100%);
      width: 250px;
      height: 100%;
      background-color: #fff;
      color: #5C4033;
      box-shadow: 2px 0 10px rgba(0, 0, 0, 0.2);
      transition: transform 0.3s ease;
      padding: 20px;
      z-index: 20;
    }
    #sidebar.active {
      transform: translateX(0);
    }
    #sidebar .close-btn {
      font-size: 22px;
      cursor: pointer;
      text-align: right;
      margin-bottom: 15px;
      color: #5C4033;
    }
    #sidebar .sidebar-logo {
      margin-bottom: 15px;
    }
    #sidebar .sidebar-logo img {
      height: 45px;
      width: auto;
      filter: brightness(0);
    }
    #sidebar ul {
      list-style: none;
      padding: 0;
      margin: 0;
      font-size: 16px;
      text-align: center;
    }
    #sidebar ul li {
      margin: 12px 0;
      border-bottom: 1px solid #EFE8DC;
      padding-bottom: 8px;
    }
    #sidebar ul li:last-child {
      border-bottom: none;
    }
    #sidebar ul li a {
      color: #5C4033;
      font-weight: bold;
      cursor: pointer;
    }
    /* صندوق الأيقونات داخل القائمة الجانبية تحت "تواصل معنا" */
    #socialContainer {
      max-height: 0;
      opacity: 0;
      overflow: hidden;
      transition: max-height 0.5s ease, opacity 0.5s ease;
    }
    #socialContainer.active {
      max-height: 50px;
      opacity: 1;
    }
    #socialContainer a {
      margin: 0 8px;
      font-size: 20px;
      color: #D2B48C;
      transition: color 0.3s;
    }
    #socialContainer a:hover {
      color: #CD853F;
    }
    /* الحاوية الرئيسية */
    .container {
      background-color: #fff;
      margin: 30px auto;
      max-width: 800px;
      width: 90%;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
    h2 {
      margin-bottom: 25px;
      font-size: 26px;
      color: #3E2723;
    }
    /* خانة الإدخال مع الأيقونات */
    .input-container {
      position: relative;
      margin-bottom: 20px;
      width: 100%;
    }
    .input-container input[type="text"] {
      width: 100%;
      padding: 14px 45px 14px 45px;
      border: 2px solid #D2B48C;
      border-radius: 30px;
      font-size: 16px;
      text-align: center;
      outline: none;
      transition: border-color 0.3s, box-shadow 0.3s;
      background-color: #fff;
      color: #3E2723;
    }
    .input-container input[type="text"]:focus {
      border-color: #CD853F;
      box-shadow: 0 0 8px rgba(205, 133, 63, 0.3);
    }
    .input-container .input-icon {
      position: absolute;
      top: 50%;
      right: 18px;
      transform: translateY(-50%);
      font-size: 20px;
      pointer-events: none;
      color: #D2B48C;
    }
    .input-container .clear-icon {
      position: absolute;
      top: 50%;
      left: 18px;
      transform: translateY(-50%);
      font-size: 20px;
      color: #D2B48C;
      cursor: pointer;
      display: none;
    }
    /* زر البحث */
    .search-button {
      width: 100%;
      padding: 14px;
      border: none;
      border-radius: 30px;
      background: linear-gradient(90deg, #CD853F, #D2B48C);
      color: #fff;
      font-size: 18px;
      cursor: pointer;
      transition: background 0.3s;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      margin-bottom: 20px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
    }
    .search-button:hover {
      background: linear-gradient(90deg, #D2B48C, #CD853F);
    }
    /* عرض النتائج */
    .result {
      margin-top: 20px;
      opacity: 0;
      transition: opacity 0.5s ease-in-out;
      font-size: 18px;
      white-space: pre-wrap;
      text-align: center;
      color: #3E2723;
    }
    .result.show {
      opacity: 1;
    }
    .result .tribe-box {
      background-color: #FDF8F0;
      border: 1px solid #D2B48C;
      padding: 12px;
      border-radius: 8px;
      margin-bottom: 12px;
      color: #3E2723;
    }
    /* جدول الرموز المشتركة بتصميم صحراوي أنيق */
    .result-table {
      width: 100%;
      border-collapse: separate;
      border-spacing: 0;
      margin-top: 20px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    }
    .result-table thead {
      background-color: #EAD7C0;
    }
    .result-table thead th {
      padding: 12px;
      border: none;
      color: #3E2723;
      font-weight: bold;
    }
    .result-table tbody tr {
      background-color: #fff;
    }
    .result-table tbody tr:nth-child(even) {
      background-color: #F7F1E1;
    }
    .result-table tbody td {
      padding: 10px;
      border: none;
      color: #5C4033;
      border-bottom: 1px solid #EFE8DC;
    }
    .result-table tbody tr:last-child td {
      border-bottom: none;
    }
    /* حاوية الأسئلة الشائعة */
    .faq-container {
      max-width: 800px;
      width: 90%;
      background-color: #fff;
      margin: 30px auto;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
    .faq-container h3 {
      font-size: 22px;
      margin-bottom: 20px;
      color: #3E2723;
      text-align: center;
    }
    .faq-item {
      border: 1px solid #EDE7E3;
      border-radius: 8px;
      margin-bottom: 10px;
      overflow: hidden;
    }
    .faq-question {
      background-color: #F9F3EE;
      padding: 12px 18px;
      font-weight: bold;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: space-between;
      transition: background-color 0.3s;
      color: #5C4033;
      font-size: 16px;
      text-align: right;
    }
    .faq-question:hover,
    .faq-question.active {
      background-color: #F3EDE7;
    }
    .faq-question .faq-icon {
      font-size: 18px;
      margin-left: 10px;
      transition: transform 0.3s;
    }
    .faq-question.active .faq-icon {
      transform: rotate(180deg);
    }
    .faq-answer {
      padding: 12px 18px;
      display: none;
      background-color: #fff;
      text-align: right;
      color: #3E2723;
      font-size: 15px;
    }
    /* حاوية "تابعنا على" الخارجية */
    .contact-container {
      max-width: 800px;
      width: 90%;
      background-color: #fff;
      margin: 30px auto;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      text-align: center;
    }
    .contact-container h3 {
      font-size: 20px;
      margin-bottom: 12px;
      color: #3E2723;
    }
    .contact-container .social-icons a {
      margin: 0 8px;
      font-size: 20px;
      color: #D2B48C;
      transition: color 0.3s;
    }
    .contact-container .social-icons a:hover {
      color: #CD853F;
    }
    /* شاشة التحميل */
    .loading {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 20px 0;
    }
    .loading-circle {
      border: 4px solid #D2B48C;
      border-top: 4px solid #CD853F;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
    }
    .loading-text {
      margin-top: 10px;
      font-size: 16px;
      color: #5C4033;
    }
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    /* الفوتر */
    footer {
      background-color: #8B4513;
      color: #F5F5DC;
      padding: 15px;
      text-align: center;
      font-size: 14px;
      margin-top: auto;
      box-shadow: 0 -2px 8px rgba(0, 0, 0, 0.2);
    }
    footer p {
      margin-bottom: 5px;
    }
    footer .extra {
      font-size: 12px;
      color: #F5F5DC;
    }
    /* الشاشات الصغيرة */
    @media (max-width: 600px) {
      .container,
      .faq-container,
      .contact-container {
        margin: 20px auto;
        padding: 20px;
      }
      .input-container input[type="text"] {
        padding: 12px 35px 12px 35px;
      }
      .search-button {
        font-size: 16px;
        padding: 12px;
      }
      .faq-container h3, h2 {
        font-size: 20px;
      }
    }
    /* تنسيق نافذة الرسالة المنبثقة */
    .popup-modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 30;
    }
    .popup-content {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      text-align: center;
      max-width: 90%;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      animation: popupAnimation 0.5s ease;
    }
    @keyframes popupAnimation {
      from { transform: scale(0.8); opacity: 0; }
      to { transform: scale(1); opacity: 1; }
    }
    .popup-buttons {
      margin-top: 15px;
      display: flex;
      justify-content: center;
      gap: 10px;
    }
    .popup-btn {
      padding: 10px 20px;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      background: linear-gradient(90deg, #CD853F, #D2B48C);
      color: #fff;
      font-size: 16px;
      transition: background 0.3s;
    }
    .popup-btn:hover {
      background: linear-gradient(90deg, #D2B48C, #CD853F);
    }
  </style>
</head>
<body>
  <!-- الهيدر -->
  <header>
    <div class="hamburger" id="openSidebar">
      <i class="fa-solid fa-bars"></i>
    </div>
    <img src="https://www2.0zz0.com/2025/04/03/00/209652548.png" alt="الشعار" class="logo" />
  </header>

  <!-- القائمة الجانبية -->
  <nav id="sidebar">
    <div class="close-btn" id="closeSidebar">
      <i class="fa-solid fa-xmark"></i>
    </div>
    <div class="sidebar-logo">
      <img src="https://www2.0zz0.com/2025/04/03/00/209652548.png" alt="الشعار" />
    </div>
    <ul>
      <li><a id="homeLink" href="#">الصفحة الرئيسية</a></li>
      <li>
        <a id="contactLink" href="#">تواصل معنا</a>
        <!-- ظهور الأيقونات تحت نص تواصل معنا مباشرة -->
        <div id="socialContainer">
          <a href="https://www.tiktok.com/@ramzfares?_t=ZS-8vEnJdcIf4x&_r=1" target="_blank"><i class="fa-brands fa-tiktok"></i></a>
          <a href="https://t.me/ramzfares"><i class="fa-brands fa-telegram"></i></a>
        </div>
      </li>
      <li><a id="aboutLink" href="about.html">حول</a></li>
    </ul>
  </nav>

  <!-- الحاوية الرئيسية -->
  <div class="container">
    <h2>الباحث في رموز القبائل</h2>
    <div class="input-container">
      <input type="text" id="searchInput" placeholder="أدخل رمز القبيلة أو اسمها" enterkeyhint="go" />
      <i class="fa-solid fa-magnifying-glass input-icon"></i>
      <i class="fa-solid fa-xmark clear-icon" id="clearBtn"></i>
    </div>
    <button id="searchBtn" class="search-button">
      <i class="fa-solid fa-magnifying-glass"></i>
      بحث
    </button>
    <div id="result" class="result"></div>
    <div id="loading" class="loading" style="display: none;">
      <div class="loading-circle"></div>
      <div class="loading-text">جارٍ البحث…</div>
    </div>
  </div>

  <!-- حاوية الأسئلة الشائعة -->
  <div class="faq-container">
    <h3>الأسئلة الشائعة</h3>
    <div class="faq-item">
      <div class="faq-question">
        <span>1. وش المقصود برموز القبائل؟</span>
        <i class="faq-icon fa-solid fa-chevron-down"></i>
      </div>
      <div class="faq-answer">
        رموز القبائل هي أرقام يختارها أفراد القبيلة لتمثيلها بشكل رمزي، غالبًا في مواقع التواصل، وتستخدم كنوع من الفخر بالانتماء.
      </div>
    </div>
    <div class="faq-item">
      <div class="faq-question">
        <span>2. هل رموز القبائل رسمية؟</span>
        <i class="faq-icon fa-solid fa-chevron-down"></i>
      </div>
      <div class="faq-answer">
        لا. الرموز غير رسمية ولا معتمدة من أي جهة حكومية. هي رموز اجتهادية وشعبية يستخدمها الشباب بشكل غير رسمي.
      </div>
    </div>
    <div class="faq-item">
      <div class="faq-question">
        <span>3. من اللي يحدد رمز القبيلة؟</span>
        <i class="faq-icon fa-solid fa-chevron-down"></i>
      </div>
      <div class="faq-answer">
        عادةً يتم تداول الرمز بين أفراد القبيلة حتى ينتشر ويصبح معروف، ولا توجد جهة رسمية تحدده.
      </div>
    </div>
    <div class="faq-item">
      <div class="faq-question">
        <span>4. هل ممكن أكثر من قبيلة تستخدم نفس الرقم؟</span>
        <i class="faq-icon fa-solid fa-chevron-down"></i>
      </div>
      <div class="faq-answer">
        نعم، أحيانًا أكثر من قبيلة تستخدم نفس الرمز خاصةً إذا كان الرقم مميزًا أو ذو شعبية.
      </div>
    </div>
    <div class="faq-item">
      <div class="faq-question">
        <span>5. هل كل القبائل لها رموز؟</span>
        <i class="faq-icon fa-solid fa-chevron-down"></i>
      </div>
      <div class="faq-answer">
        لا، بعض القبائل لها رموز متداولة بينما لا تهتم البعض الآخر بتلك الرموز.
      </div>
    </div>
  </div>

  <!-- حاوية "تابعنا على" الخارجية -->
  <div class="contact-container">
    <h3>تابعنا على</h3>
    <div class="social-icons">
      <a href="https://www.tiktok.com/@ramzfares?_t=ZS-8vEnRkpwuDY&_r=1" target="_blank"><i class="fa-brands fa-tiktok"></i></a>
      <a href="https://t.me/ramzfares"><i class="fa-brands fa-telegram"></i></a>
    </div>
  </div>

  <!-- نافذة الرسالة المنبثقة -->
  <div id="popupModal" class="popup-modal">
    <div class="popup-content">
      <p id="popupMessage"></p>
      <div class="popup-buttons">
        <button id="contactBtn" class="popup-btn">تواصل</button>
        <button id="cancelBtn" class="popup-btn">الغاء</button>
      </div>
    </div>
  </div>

  <!-- الفوتر -->
  <footer>
    <p>&copy; حقوق النشر محفوظة</p>
    <p class="extra">برمجة فارس القميشي</p>
  </footer>

  <script>
    // دالة الانتقال الناعم مع تأثير الفيد أوت
    function fadeOutAndRedirect(url) {
      document.body.classList.add('fade-out');
      setTimeout(function() {
        window.location.href = url;
      }, 500);
    }

    // تفعيل القائمة الجانبية
    const openSidebar = document.getElementById("openSidebar");
    const closeSidebar = document.getElementById("closeSidebar");
    const sidebar = document.getElementById("sidebar");
    const hamburger = document.querySelector(".hamburger");
    const homeLink = document.getElementById("homeLink");
    const contactLink = document.getElementById("contactLink");
    const socialContainer = document.getElementById("socialContainer");
    const aboutLink = document.getElementById("aboutLink");

    openSidebar.addEventListener("click", () => {
      sidebar.classList.toggle("active");
      hamburger.classList.toggle("active");
    });

    closeSidebar.addEventListener("click", () => {
      sidebar.classList.remove("active");
      hamburger.classList.remove("active");
    });

    homeLink.addEventListener("click", () => {
      sidebar.classList.remove("active");
      hamburger.classList.remove("active");
      document.querySelector(".container").scrollIntoView({ behavior: "smooth" });
    });

    contactLink.addEventListener("click", () => {
      socialContainer.classList.toggle("active");
    });

    // عند الضغط على "حول" يتم الانتقال مع تأثير الفيد
    if (aboutLink) {
      aboutLink.addEventListener("click", function(event) {
         event.preventDefault();
         fadeOutAndRedirect(this.href);
      });
    }

    /* باقي كود البحث والوظائف كما هو موجود */
    function normalizeArabic(text) {
      return text
        .toLowerCase()
        .replace(/[إأآا]/g, "ا")
        .replace(/ة/g, "ه")
        .replace(/[ىئ]/g, "ي")
        .replace(/[\u064B-\u0652]/g, "")
        .trim();
    }

    // تعريف بيانات القبائل مع القبائل المضافة
    const tribes = {
      "715": [{ name: "لقموش" }],
      "917": [{ name: "العوالق" }],
      "711": [
        { name: "الصيعر" },
        { name: "وادعه" },
        { name: "بني مالك" },
        { name: "وائله" },
        { name: "قيفة" },
        { name: "دهم" },
        { name: "مراد" }
      ],
      "505": [{ name: "قحطان" }],
      "454": [{ name: "بلسمر" }],
      "509": [
        { name: "بلقرن" },
        { name: "الشرارات" }
      ],
      "511": [{ name: "عتيبه" }],
      "507": [
        { name: "شهران" },
        { name: "بني شهر" }
      ],
      "606": [
        { name: "اكلب" },
        { name: "بني غامد" }
      ],
      "911": [
        { name: "البقوم" },
        { name: "بني خالد" },
        { name: "يام" }
      ],
      "903": [{ name: "بارق" }],
      "309": [{ name: "بني حمد" }],
      "601": [{ name: "بني الحلف" }],
      "811": [{ name: "نهد" }],
      "101": [{ name: "العجمان" }],
      "504": [
        { name: "آل غريّبني" },
        { name: "همام" }
      ],
      "516": [
        { name: "الجدادله" },
        { name: "خولان" }
      ],
      "909": [{ name: "بلحمر" }],
      "305": [{ name: "مطير" }],
      "518": [{ name: "جهينه" }],
      "607": [
        { name: "عليان" },
        { name: "خثعم" }
      ],
      "717": [{ name: "السهول" }],
      "404": [{ name: "عبس" }],
      "311": [
        { name: "رجال الحجر" },
        { name: "بني مسروح" }
      ],
      "907": [{ name: "بني الحكم" }],
      "515": [
        { name: "سليم" },
        { name: "هذيل" },
        { name: "الاشراف" },
        { name: "الهواشم" }
      ],
      "405": [{ name: "ال مره" }],
      "808": [{ name: "تليد" }],
      "205": [{ name: "الظفير" }],
      "503": [{ name: "سبيع" }],
      "707": [
        { name: "عسير" },
        { name: "غامد" }
      ],
      "612": [{ name: "بني زيد" }],
      "818": [{ name: "بلي" }],
      "708": [{ name: "بني مروان" }],
      "902": [{ name: "بني شبيب" }],
      "912": [{ name: "العوامر" }],
      "411": [{ name: "بني هاجر" }],
      "906": [{ name: "العوازم" }],
      "905": [{ name: "فيفاء" }],
      "107": [{ name: "المهره" }],
      "701": [{ name: "بني عمرو" }],
      "702": [{ name: "زهران" }],
      "502": [{ name: "الــدواسـر" }],
      "525": [{ name: "شمران" }],
      "901": [
        { name: "ثقيف" },
        { name: "الفضول" }
      ],
      "506": [{ name: "بني تميم" }],
      "B-52": [{ name: "عنزه" }],
      "F-15": [{ name: "حرب" }],
      "F-16": [{ name: "شمر" }],
      "B-79": [{ name: "بني عطية" }],
      "111": [{ name: "الحوطات" }],
      /* القبائل الجديدة */
      "Y-10": [{ name: "يافع" }],
      "716": [{ name: "نعمان" }],
      "719": [{ name: "بنير" }],
      "501": [
        { name: "بلحارث" },
        { name: "ال حميقان" }
      ],
      "611": [
        { name: "العوابثه" },
        { name: "باوزير" }
      ],
      "705": [{ name: "بني هلال" }],
      "110": [
        { name: "الرصاص" },
        { name: "المناهيل" }
      ],
      "809": [{ name: "سيبان" }],
      "512": [{ name: "ال كثير" }],
      "919": [{ name: "ال بريك" }],
      "714": [{ name: "حمّير" }],
      "517": [{ name: "المشاجر" }],
      "S300": [{ name: "ال كثير" }],
      "604": [{ name: "المصعبين" }],
      "910": [{ name: "ال بريك" }],
      "F-14": [{ name: "الكرب" }],
      "712": [{ name: "نوح" }]
    };

    const searchBtn = document.getElementById("searchBtn");
    const searchInput = document.getElementById("searchInput");
    const resultDiv = document.getElementById("result");
    const loadingDiv = document.getElementById("loading");
    const inputIcon = document.querySelector(".input-icon");
    const clearIcon = document.getElementById("clearBtn");

    searchInput.addEventListener("input", function () {
      if (searchInput.value.trim().length > 0) {
        inputIcon.style.display = "none";
        clearIcon.style.display = "block";
      } else {
        inputIcon.style.display = "block";
        clearIcon.style.display = "none";
      }
    });

    clearIcon.addEventListener("click", function () {
      searchInput.value = "";
      inputIcon.style.display = "block";
      clearIcon.style.display = "none";
      searchInput.focus();
      resultDiv.innerHTML = "";
      resultDiv.classList.remove("show");
    });

    searchBtn.addEventListener("click", performSearch);
    searchInput.addEventListener("keydown", function (e) {
      if (e.key === "Enter") performSearch();
    });

    function performSearch() {
      const query = searchInput.value.trim();
      if (!query) {
        resultDiv.textContent = "يرجى ملء خانة البحث";
        resultDiv.classList.add("show");
        return;
      }
      resultDiv.classList.remove("show");
      resultDiv.innerHTML = "";
      loadingDiv.style.display = "flex";

      const delay = Math.floor(Math.random() * 2000) + 3000;
      setTimeout(function () {
        loadingDiv.style.display = "none";
        // التحقق من إدخال رمز (رقمي أو نمط B-/F-)
        if (/^\d+$|^(B-\d+|F-\d+)$/i.test(query)) {
          if (tribes[query]) {
            if (tribes[query].length > 1) {
              const table = document.createElement("table");
              table.className = "result-table";
              const thead = document.createElement("thead");
              const headerRow = document.createElement("tr");
              const thCode = document.createElement("th");
              thCode.textContent = "الرمز";
              const thTribes = document.createElement("th");
              thTribes.textContent = "القبائل المشتركة";
              headerRow.appendChild(thCode);
              headerRow.appendChild(thTribes);
              thead.appendChild(headerRow);
              table.appendChild(thead);

              const tbody = document.createElement("tbody");
              const row = document.createElement("tr");
              const tdCode = document.createElement("td");
              tdCode.textContent = query;
              const tdTribes = document.createElement("td");
              const tribesNames = tribes[query]
                .map((entry) => entry.name)
                .join("، ");
              tdTribes.textContent = tribesNames;
              row.appendChild(tdCode);
              row.appendChild(tdTribes);
              tbody.appendChild(row);
              table.appendChild(tbody);

              resultDiv.appendChild(table);
            } else {
              tribes[query].forEach(function (entry) {
                const box = document.createElement("div");
                box.className = "tribe-box";
                box.textContent = `هذا الرمز ${query} يعود لقبيلة ${entry.name}`;
                resultDiv.appendChild(box);
              });
            }
          } else {
            resultDiv.textContent = "عفواً لم يتم العثور على قبيلة بهذا الرمز";
            // عرض الرسالة المنبثقة الجديدة بعد ثانيتين في حال الرمز غير موجود
            setTimeout(function(){
              showPopupCode(query);
            }, 2000);
          }
        } else {
          const normalizedQuery = normalizeArabic(query);
          let found = false;
          for (const code in tribes) {
            tribes[code].forEach(function (entry) {
              if (normalizeArabic(entry.name).includes(normalizedQuery)) {
                found = true;
                const box = document.createElement("div");
                box.className = "tribe-box";
                box.textContent = `${entry.name} رمز القبيلة هو ${code}`;
                resultDiv.appendChild(box);
              }
            });
          }
          if (!found) {
            resultDiv.textContent = "عفواً لم يتم العثور على رمز لهذه القبيلة";
            // عرض الرسالة المنبثقة القديمة بعد ثانيتين في حال الاسم غير موجود
            if (!/^\d+$|^(B-\d+|F-\d+)$/i.test(query)) {
              setTimeout(function() {
                showPopup(query);
              }, 2000);
            }
          }
        }
        resultDiv.classList.add("show");
      }, delay);
    }

    // دالة عرض الرسالة المنبثقة للقبائل غير الموجودة عند البحث بالاسم (السابقة)
    function showPopup(query) {
      const popupModal = document.getElementById("popupModal");
      const popupMessage = document.getElementById("popupMessage");
      popupMessage.innerHTML = `قد يكون الرمز لقبيلة (<strong>${query}</strong>) غير مضاف حالياً قم بالتواصل معنا لتعريفه وإضافته في المنصة`;
      popupModal.style.display = "flex";
      // تعيين رابط التواصل القديم لهذه الحالة
      document.getElementById("contactBtn").onclick = function() {
        window.location.href = "https://www.tiktok.com/@6adio?_t=ZS-8vEWJHq02o4&_r=1";
      };
    }

    // دالة عرض الرسالة المنبثقة الجديدة عند إدخال رمز لقبيلة غير موجودة
    function showPopupCode(query) {
      const popupModal = document.getElementById("popupModal");
      const popupMessage = document.getElementById("popupMessage");
      popupMessage.innerHTML = `قد يكون رمز (<strong>${query}</strong>) يتبع لقبيلة غير مسجلة في المنصة، يمكنك التواصل معنا في حال أردت إضافته`;
      popupModal.style.display = "flex";
      // تعيين رابط التواصل الجديد لهذه الحالة
      document.getElementById("contactBtn").onclick = function() {
        window.location.href = "https://www.tiktok.com/@ramzfares?_t=ZS-8vEmO5wJ6pj&_r=1";
      };
    }

    // التعامل مع زر إلغاء النافذة المنبثقة
    document.getElementById("cancelBtn").addEventListener("click", function() {
      document.getElementById("popupModal").style.display = "none";
    });

    const faqQuestions = document.querySelectorAll(".faq-question");
    faqQuestions.forEach((question) => {
      question.addEventListener("click", function () {
        const answer = this.nextElementSibling;
        const icon = this.querySelector(".faq-icon");
        if (answer.style.display === "block") {
          answer.style.display = "none";
          this.classList.remove("active");
          icon.classList.replace("fa-chevron-up", "fa-chevron-down");
        } else {
          answer.style.display = "block";
          this.classList.add("active");
          icon.classList.replace("fa-chevron-down", "fa-chevron-up");
        }
      });
    });
  </script>
</body>
</html>