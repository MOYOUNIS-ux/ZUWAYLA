<!DOCTYPE html>
<html lang="ar" dir="rtl" id="html-root">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZUWAYLA — Tax Position & Decision Flow Suite</title>
    <style>
        :root {
            --primary: #1e3a8a;
            --secondary: #0d9488;
            --accent: #ea580c;
            --bg: #f8fafc;
            --card: #ffffff;
            --text: #0f172a;
            --border: #e2e8f0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        .screen { display: none; padding: 20px; box-sizing: border-box; flex: 1; }
        .screen.active { display: block; }

        /* Lang Button Header */
        .lang-bar {
            padding: 10px 20px;
            background: #f1f5f9;
            display: flex;
            justify-content: flex-end;
            border-bottom: 1px solid var(--border);
        }
        .btn-lang {
            background: var(--secondary);
            color: white;
            border: none;
            padding: 6px 14px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
        }

        /* Welcome Screen Styling */
        .welcome-container {
            max-width: 600px;
            margin: 50px auto;
            text-align: center;
            background: var(--card);
            padding: 40px;
            border-radius: 12px;
            box-shadow: 0 10px 25px -5px rgba(0,0,0,0.1);
        }

        .welcome-container h1 { color: var(--primary); margin-bottom: 10px; }
        .welcome-container p { color: #64748b; margin-bottom: 30px; }

        .btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            font-size: 16px;
            width: 100%;
            margin-bottom: 12px;
            transition: background 0.2s;
        }
        .btn-secondary { background-color: var(--secondary); }
        .btn-accent { background-color: #64748b; }
        .btn:hover { opacity: 0.9; }

        /* Internal Application Layout */
        header {
            background-color: var(--primary);
            color: white;
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
        }

        .nav-tabs button {
            background: rgba(255,255,255,0.15);
            border: none;
            color: white;
            padding: 8px 16px;
            margin: 0 3px;
            cursor: pointer;
            border-radius: 4px;
        }
        .nav-tabs button.active { background: var(--secondary); font-weight: bold; }

        .container { max-width: 1200px; margin: 30px auto; flex: 1; width: 100%; px: 15px; box-sizing: border-box;}
        .card { background: var(--card); border-radius: 8px; padding: 25px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); margin-bottom: 20px; }
        
        /* Forms styling */
        .form-group { margin-bottom: 15px; }
        html[dir="rtl"] .form-group { text-align: right; }
        html[dir="ltr"] .form-group { text-align: left; }
        label { display: block; margin-bottom: 5px; font-weight: 600; }
        input, select { width: 100%; padding: 10px; border: 1px solid var(--border); border-radius: 6px; box-sizing: border-box; }

        /* Tables */
        table { width: 100%; border-collapse: collapse; margin-top: 15px; background: white; }
        th, td { border: 1px solid var(--border); padding: 12px; font-size: 14px; }
        html[dir="rtl"] th, html[dir="rtl"] td { text-align: right; }
        html[dir="ltr"] th, html[dir="ltr"] td { text-align: left; }
        th { background-color: #f1f5f9; color: var(--primary); }

        /* Badges */
        .badge { padding: 4px 8px; border-radius: 4px; font-size: 12px; font-weight: bold; }
        .badge-active { background-color: #dcfce7; color: #166534; }
        .badge-blocked { background-color: #fee2e2; color: #991b1b; }

        .result-box { background-color: #f0fdf4; border-inline-start: 5px solid #16a34a; padding: 20px; border-radius: 6px; margin-top: 20px; }
        .paywall { text-align: center; color: var(--accent); border: 2px dashed var(--accent); background: #fff7ed; padding: 30px; border-radius: 8px; }

        /* Footer styling */
        footer {
            background-color: #0f172a;
            color: #94a3b8;
            text-align: center;
            padding: 15px;
            font-size: 14px;
            margin-top: auto;
            border-top: 1px solid #1e293b;
        }
        footer a {
            color: #0d9488;
            text-decoration: none;
            font-weight: bold;
            transition: color 0.2s;
        }
        footer a:hover {
            color: #2dd4bf;
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <!-- شريط تغيير اللغة العلوي الثابت -->
    <div class="lang-bar">
        <button class="btn-lang" onclick="toggleLanguage()" id="lang-toggle-btn">English</button>
    </div>

    <!-- 1. شاشة الترحيب والمدخل الرئيسي -->
    <div id="screen-welcome" class="screen active">
        <div class="welcome-container">
            <h1 data-key="welcome-title">ZUWAYLA Tax Suite</h1>
            <p data-key="welcome-desc">اختبار</p>
            <button class="btn btn-secondary" onclick="showScreen('screen-client-login')" data-key="btn-client-login">تسجيل دخول عميل</button>
            <button class="btn" onclick="showScreen('screen-register')" data-key="btn-client-reg">إنشاء حساب عميل جديد</button>
            <button class="btn btn-accent" onclick="showScreen('screen-admin-login')" data-key="btn-admin-portal">بوابة الإدارة (Admin)</button>
        </div>
    </div>

    <!-- 2. شاشة إنشاء حساب عميل جديد -->
    <div id="screen-register" class="screen">
        <div class="welcome-container">
            <h2 data-key="reg-title">إنشاء حساب عميل جديد</h2>
            <p data-key="reg-desc">يرجى إدخال البيانات للحصول على فترة سماح 15 يوماً مجاناً</p>
            <div class="form-group">
                <label data-key="lbl-name">الاسم بالكامل:</label>
                <input type="text" id="reg-name" placeholder="مثال: شركة يونس للخدمات اللوجستية">
            </div>
            <div class="form-group">
                <label data-key="lbl-email">البريد الإلكتروني:</label>
                <input type="email" id="reg-email" placeholder="name@example.com">
            </div>
            <div class="form-group">
                <label data-key="lbl-phone">رقم الهاتف (مع رمز الدولة):</label>
                <input type="text" id="reg-phone" placeholder="971500000000+">
            </div>
            <button class="btn" onclick="handleRegistration()" data-key="btn-send-code">إرسال كود التفعيل</button>
            <button class="btn btn-accent" onclick="showScreen('screen-welcome')" data-key="btn-back">رجوع</button>
        </div>
    </div>

    <!-- 3. شاشة إدخال كود التفعيل للعميل -->
    <div id="screen-verify" class="screen">
        <div class="welcome-container">
            <h2 data-key="verify-title">تأكيد الحساب</h2>
            <p id="verify-msg">تم إرسال كود تفعيل مؤلف من 4 أرقام إلى بريدك الإلكتروني.</p>
            <div class="form-group">
                <label data-key="lbl-enter-code">أدخل كود التفعيل (الافتراضي للتجربة: 1234):</label>
                <input type="text" id="verify-code" style="text-align: center; font-size: 20px; letter-spacing: 5px;">
            </div>
            <button class="btn btn-secondary" onclick="handleVerification()" data-key="btn-verify-act">تفعيل الحساب والتشغيل</button>
        </div>
    </div>

    <!-- 4. شاشة تسجيل دخول العميل -->
    <div id="screen-client-login" class="screen">
        <div class="welcome-container">
            <h2 data-key="login-title">تسجيل دخول العميل</h2>
            <div class="form-group">
                <label data-key="lbl-login-id">البريد الإلكتروني أو رقم الهاتف:</label>
                <input type="text" id="login-client-id" placeholder="أدخل البريد الإلكتروني أو الهاتف المسجل">
            </div>
            <button class="btn btn-secondary" onclick="handleClientLogin()" data-key="btn-enter">دخول</button>
            <button class="btn btn-accent" onclick="showScreen('screen-welcome')" data-key="btn-back">رجوع</button>
        </div>
    </div>

    <!-- 5. شاشة تسجيل دخول الإدارة (Admin) -->
    <div id="screen-admin-login" class="screen">
        <div class="welcome-container">
            <h2 data-key="admin-login-title">تسجيل دخول الإدارة (Admin)</h2>
            <div class="form-group">
                <label data-key="lbl-admin-user">اسم المستخدم للآدمن:</label>
                <input type="text" id="admin-user" value="admin">
            </div>
            <div class="form-group">
                <label data-key="lbl-admin-pass">كلمة المرور:</label>
                <input type="password" id="admin-pass" placeholder="أدخل كلمة مرور الآدمن">
            </div>
            <button class="btn" onclick="handleAdminLogin()" data-key="btn-admin-enter">دخول لوحة التحكم</button>
            <button class="btn btn-accent" onclick="showScreen('screen-welcome')" data-key="btn-back">رجوع</button>
        </div>
    </div>

    <!-- 6. الشاشة الرئيسية الكبرى للتطبيق (بعد الدخول الناجح) -->
    <div id="screen-main-app" class="screen" style="padding:0;">
        <header>
            <h3>ZUWAYLA Tax Suite</h3>
            <div class="nav-tabs" id="tabs-container">
                <button id="tab-flow" class="active" onclick="switchTab('flow')">ZUWAYLA — Decision Flow</button>
                <button id="tab-position" onclick="switchTab('position')">ZUWAYLA — Tax Position</button>
                <button id="tab-admin" style="display:none; background-color:#b91c1c;" onclick="switchTab('admin')" data-key="tab-lbl-admin">لوحة تحكم الآدمن</button>
                <button style="background: #ef4444;" onclick="logout()" data-key="btn-logout">خروج</button>
            </div>
        </header>

        <div class="container">
            <!-- إشعار حالة الحساب وفترة السماح للعميل -->
            <div id="account-status-bar" class="card" style="background: #eff6ff; border-inline-start: 4px solid var(--primary); display: flex; justify-content: space-between;">
                <span id="welcome-user-text"></span>
                <span id="days-left-text" style="font-weight: bold; color: var(--accent);"></span>
            </div>

            <!-- الشاشة الموقوفة (انتهاء فترة السماح) -->
            <div id="block-paywall" class="card paywall" style="display: none;">
                <h2 data-key="paywall-title">عذراً، انتهت فترة السماح المجانية الخاصة بحسابك (15 يوماً)</h2>
                <p data-key="paywall-desc">لإعادة تمكين الحساب وفتح النطاق الكامل لعمليات الفحص الضريبية، يرجى التواصل فوراً مع مكتب الدعم الفني المعتمد بدولة الإمارات والتفعيل:</p>
                <h1 style="color: var(--primary); letter-spacing: 1px;">971-50-0000000+</h1>
                <p style="font-size: 13px; color: #64748b;" data-key="paywall-note">يرجى إعطاء موظف الخدمة بريدك الإلكتروني لتوثيق تفعيل السداد الفوري.</p>
            </div>

            <div id="app-content-body">
                <!-- شيت الـ Decision Flow -->
                <div id="sub-screen-flow" class="tab-content">
                    <div class="card">
                        <h2 data-key="flow-card-title">ZUWAYLA — Decision Flow</h2>
                        <p style="color: #64748b; font-size:14px;" data-key="flow-card-desc"><strong>دليل الاستخدام الشجري:</strong> اختر تصنيف المعاملة الرئيسي وسيتم توجيهك بالأسئلة المتتابعة بشكل ديناميكي حتى الوصول للحكم التشريعي النهائي.</p>
                        <hr style="border: 0; border-top: 1px solid var(--border); margin: 20px 0;">

                        <div class="form-group">
                            <label data-key="lbl-select-cat">1. حدد التصنيف القانوني للمعاملة (Category):</label>
                            <select id="flow-category" onchange="buildDynamicTree()">
                                <!-- الخيارات يتم بناؤها ديناميكياً لتحديث لغتها -->
                            </select>
                        </div>

                        <!-- حاوية الأسئلة الديناميكية المتفرعة بناءً على الشيت -->
                        <div id="dynamic-questions-zone"></div>

                        <button class="btn btn-secondary" style="margin-top:20px; max-width:300px;" onclick="executeEngineDecision()" data-key="btn-run-engine">تشغيل محرك الفحص القانوني</button>

                        <div id="flow-result-box" class="result-box" style="display: none;"></div>
                    </div>
                </div>

                <!-- شيت الـ Tax Position -->
                <div id="sub-screen-position" class="tab-content" style="display: none;">
                    <div class="card">
                        <h2 data-key="position-card-title">ZUWAYLA — Tax Position Register</h2>
                        <p style="color: #64748b;" data-key="position-card-desc">قاعدة البيانات التشريعية الكاملة للمواقف الضريبية المتطابقة مع الفحص الفني (40/40 Paths Pass):</p>
                        <div style="overflow-x: auto;">
                            <table id="tax-position-table">
                                <thead id="tax-position-thead">
                                    <!-- يتم بناؤها باللغة المختارة -->
                                </thead>
                                <tbody id="tax-position-tbody"></tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- شاشة تحكم الأدمن الفرعية -->
                <div id="sub-screen-admin" class="tab-content" style="display: none;">
                    <div class="card">
                        <h2 data-key="admin-card-title">لوحة تحكم الإدارة العليا</h2>
                        <p style="color: #64748b;" data-key="admin-card-desc">مراقبة العملاء الذين سجلوا أولاً بأول والتحكم الكامل في حساباتهم:</p>
                        
                        <div class="form-group">
                            <input type="text" id="user-search-input" onkeyup="filterAdminUsers()" placeholder="ابحث باسم العميل...">
                        </div>

                        <table id="admin-users-table">
                            <thead id="admin-users-thead">
                                <!-- العناوين مبنية ديناميكياً -->
                            </thead>
                            <tbody id="admin-users-tbody"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- التذييل المطلوب والمربوط بالواتساب الفوري لمحمد يونس -->
    <footer>
        Developed & Managed by <a href="https://wa.me/201146479052" target="_blank">Mohamed Younis</a> &copy; 2026
    </footer>

    <script>
        // ملف الترجمة ثنائي اللغة بالكامل
        let currentLang = "ar";
        const translations = {
            ar: {
                "lang-btn": "English",
                "welcome-title": "ZUWAYLA Tax Suite",
                "welcome-desc": "تيست",
                "btn-client-login": "تسجيل دخول عميل",
                "btn-client-reg": "إنشاء حساب عميل جديد",
                "btn-admin-portal": "بوابة الإدارة (Admin)",
                "reg-title": "إنشاء حساب عميل جديد",
                "reg-desc": "يرجى إدخال البيانات للحصول على فترة سماح 15 يوماً مجاناً",
                "lbl-name": "الاسم بالكامل:",
                "lbl-email": "البريد الإلكتروني:",
                "lbl-phone": "رقم الهاتف (مع رمز الدولة):",
                "btn-send-code": "إرسال كود التفعيل",
                "btn-back": "رجوع",
                "verify-title": "تأكيد الحساب",
                "lbl-enter-code": "أدخل كود التفعيل (الافتراضي للتجربة: 1234):",
                "btn-verify-act": "تفعيل الحساب والتشغيل",
                "login-title": "تسجيل دخول العميل",
                "lbl-login-id": "البريد الإلكتروني أو رقم الهاتف:",
                "btn-enter": "دخول",
                "admin-login-title": "تسجيل دخول الإدارة (Admin)",
                "lbl-admin-user": "اسم المستخدم للآدمن:",
                "lbl-admin-pass": "كلمة المرور:",
                "btn-admin-enter": "دخول لوحة التحكم",
                "tab-lbl-admin": "لوحة تحكم الآدمن",
                "btn-logout": "خروج",
                "paywall-title": "عذراً، انتهت فترة السماح المجانية الخاصة بحسابك (15 يوماً)",
                "paywall-desc": "لإعادة تمكين الحساب وفتح النطاق الكامل لعمليات الفحص الضريبية، يرجى التواصل فوراً مع مكتب الدعم الفني المعتمد بدولة الإمارات والتفعيل:",
                "paywall-note": "يرجى إعطاء موظف الخدمة بريدك الإلكتروني لتوثيق تفعيل السداد الفوري.",
                "flow-card-title": "ZUWAYLA — Decision Flow",
                "flow-card-desc": "دليل الاستخدام الشجري: اختر تصنيف المعاملة الرئيسي وسيتم توجيهك بالأسئلة المتتابعة بشكل ديناميكي حتى الوصول للحكم التشريعي النهائي.",
                "lbl-select-cat": "1. حدد التصنيف القانوني للمعاملة (Category):",
                "btn-run-engine": "تشغيل محرك الفحص القانوني",
                "position-card-title": "ZUWAYLA — Tax Position Register",
                "position-card-desc": "قاعدة البيانات التشريعية الكاملة للمواقف الضريبية المتطابقة مع الفحص الفني (40/40 Paths Pass):",
                "admin-card-title": "لوحة تحكم الإدارة العليا",
                "admin-card-desc": "مراقبة العملاء الذين سجلوا أولاً بأول والتحكم الكامل في حساباتهم:"
            },
            en: {
                "lang-btn": "العربية",
                "welcome-title": "ZUWAYLA Tax Suite",
                "welcome-desc": "test",
                "btn-client-login": "Client Login",
                "btn-client-reg": "Register New Client Account",
                "btn-admin-portal": "Administration Gateway (Admin)",
                "reg-title": "Create New Client Account",
                "reg-desc": "Please enter registration details to secure a 15-day free grace period",
                "lbl-name": "Full Name / Entity:",
                "lbl-email": "Email Address:",
                "lbl-phone": "Phone Number (with Country Code):",
                "btn-send-code": "Send Activation Code",
                "btn-back": "Back",
                "verify-title": "Account Verification",
                "lbl-enter-code": "Enter Activation Code (Default for testing: 1234):",
                "btn-verify-act": "Activate Account & Launch",
                "login-title": "Client Login Portal",
                "lbl-login-id": "Registered Email or Phone Number:",
                "btn-enter": "Login",
                "admin-login-title": "Admin Authentication",
                "lbl-admin-user": "Admin Username:",
                "lbl-admin-pass": "Password:",
                "btn-admin-enter": "Access Admin Dashboard",
                "tab-lbl-admin": "Admin Control Panel",
                "btn-logout": "Logout",
                "paywall-title": "Attention: Your 15-Day Free Grace Period Has Expired",
                "paywall-desc": "To unblock your account and restore access to the automated tax engine, please contact the certified support desk in the UAE immediately:",
                "paywall-note": "Please provide your registered email address to the representative to authorize instant clearance.",
                "flow-card-title": "ZUWAYLA — Decision Flow Engine",
                "flow-card-desc": "Tree Logic Guide: Select the core transaction type, and the module will populate targeted regulatory questions to isolate the statutory tax ruling.",
                "lbl-select-cat": "1. Select Legal Category of Transaction:",
                "btn-run-engine": "Execute Legislative Tax Engine",
                "position-card-title": "ZUWAYLA — Tax Position Register",
                "position-card-desc": "Complete Legislative Matrix mapping the definitive tax treatments (40/40 Analytical Paths Compliant):",
                "admin-card-title": "Executive Administration Panel",
                "admin-card-desc": "Real-time client ledger overview and manual compliance access override:"
            }
        };

        const statutoryDatabase = [
            { pos: "P-00", cat: "Decision support", trigger: "Essential facts missing or contradictory", rate: "Need info", treatment: "More information required", legal: "Validation" },
            { pos: "P-01", cat: "Transport of goods", trigger: "International transport of goods, one supplier for the whole journey", rate: "0%", treatment: "Zero-rated", legal: "Art.45(2) Decree + Art.33(1) ER" },
            { pos: "P-03", cat: "Transport of goods", trigger: "Domestic leg by the SAME supplier as the international transport", rate: "0%", treatment: "Zero-rated", legal: "Art.33(1)(d) ER + VATP040" },
            { pos: "P-04", cat: "Transport of goods", trigger: "Domestic leg by a DIFFERENT supplier / separate contract", rate: "5%", treatment: "Standard-rated", legal: "Art.33(1)(d) ER + VATP040" },
            { pos: "P-05", cat: "Transport of goods", trigger: "Purely domestic transport / local supply inside the UAE", rate: "5%", treatment: "Standard-rated", legal: "Art.2 Decree" },
            { pos: "P-15", cat: "Transport of goods", trigger: "Transport BEGINS outside the UAE", rate: "Out of scope", treatment: "Outside the scope of UAE VAT", legal: "Art.30(3) Decree" },
            { pos: "P-16", cat: "Transport of goods", trigger: "Foreign-to-foreign transport, no UAE nexus", rate: "Out of scope", treatment: "Outside the scope of UAE VAT", legal: "Art.30(3) Decree" },
            { pos: "P-06", cat: "Goods movement", trigger: "Export of goods, full evidence kept in time", rate: "0%", treatment: "Zero-rated", legal: "Art.45(1) Decree + Art.30 ER" },
            { pos: "P-EVID", cat: "Goods movement", trigger: "Qualifies for 0% but evidence missing / out of time", rate: "5%", treatment: "Standard — pending evidence", legal: "Art.30 ER" },
            { pos: "P-08", cat: "Goods movement", trigger: "Import of goods into the mainland (owner imports)", rate: "5%", treatment: "Import VAT (reverse charge)", legal: "Art.48 Decree + Art.50 ER" },
            { pos: "P-10", cat: "Designated Zone", trigger: "Move between two Designated Zones", rate: "Out of scope", treatment: "Outside the scope of UAE VAT", legal: "Art.51(3) ER" },
            { pos: "P-11", cat: "Designated Zone", trigger: "From the mainland INTO a Designated Zone", rate: "5%", treatment: "Standard-rated (local)", legal: "Art.30(3) ER" },
            { pos: "P-12", cat: "Designated Zone", trigger: "From a Designated Zone INTO the mainland (import)", rate: "5%", treatment: "Standard-rated (import)", legal: "Art.30(3)+Art.50 ER" },
            { pos: "P-13b", cat: "Designated Zone", trigger: "DZ goods DELIVERED outside the UAE (customs + commercial proof)", rate: "Out of scope", treatment: "Outside the scope of UAE VAT", legal: "Art.51(5)(b) ER + VATP027" },
            { pos: "P-22", cat: "Forwarder / agency", trigger: "Cost paid in client's name, at exact cost (disbursement)", rate: "Out of scope", treatment: "Outside the scope of UAE VAT", legal: "VATP013 + Art.1 Decree" },
            { pos: "P-24", cat: "Mixed invoice", trigger: "Several services at SEPARATE prices (multiple supplies)", rate: "Each on its own", treatment: "Multiple supplies", legal: "Art.4(4) ER + VATP040" },
            { pos: "P-26", cat: "Decision support", trigger: "Genuine legal grey area, exclusion not established", rate: "5%", treatment: "Safe Default Position", legal: "VATP027" },
            { pos: "P-PASS-01", cat: "Passengers", trigger: "International transport of passengers", rate: "0%", treatment: "Zero-rated", legal: "Art.45(2) Decree" }
        ];

        let usersDatabase = [
            { name: "شركة النقل العالمية للعبور", email: "younis@example.com", phone: "971501111111", regDate: "2026-06-15", isBlocked: false, daysLeft: 12 },
            { name: "دبي للشحن السريع", email: "dubai@cargo.ae", phone: "971502222222", regDate: "2026-06-01", isBlocked: true, daysLeft: 0 }
        ];

        let activeUser = null;
        let isAdminActive = false;
        let tempRegData = null;

        function toggleLanguage() {
            currentLang = currentLang === "ar" ? "en" : "ar";
            const root = document.getElementById('html-root');
            if(currentLang === "en") {
                root.setAttribute('dir', 'ltr');
                root.setAttribute('lang', 'en');
            } else {
                root.setAttribute('dir', 'rtl');
                root.setAttribute('lang', 'ar');
            }
            applyTranslations();
        }

        function applyTranslations() {
            // ترجمة الأزرار والنصوص الثابتة
            document.getElementById('lang-toggle-btn').innerText = translations[currentLang]["lang-btn"];
            document.querySelectorAll('[data-key]').forEach(el => {
                const key = el.getAttribute('data-key');
                if(translations[currentLang][key]) {
                    el.innerText = translations[currentLang][key];
                }
            });

            // ترجمة خيارات فئات الشجرة الـ Categories
            const catSelect = document.getElementById('flow-category');
            const savedVal = catSelect.value;
            catSelect.innerHTML = currentLang === "ar" ? `
                <option value="">-- اختر الفئة الرئيسية --</option>
                <option value="Transport">1 Transport of goods (خدمات نقل البضائع)</option>
                <option value="Goods">2 Goods movement (حركة وتوريد البضائع)</option>
                <option value="DZ">3 Designated Zone (المناطق المحددة والبيوع داخلها)</option>
                <option value="Agency">4 Forwarder and agency (الوكالة وإعادة الفوترة)</option>
                <option value="Mixed">5 Mixed invoice (الفواتير المركبة والمختلطة)</option>
                <option value="Passengers">6 Passengers and MOT (نقل الركاب ووسائل النقل)</option>
                <option value="Input">7 Needs more input (حالات تتطلب معطيات إضافية)</option>
            ` : `
                <option value="">-- Select Main Category --</option>
                <option value="Transport">1 Transport of goods</option>
                <option value="Goods">2 Goods movement</option>
                <option value="DZ">3 Designated Zone</option>
                <option value="Agency">4 Forwarder and agency</option>
                <option value="Mixed">5 Mixed invoice</option>
                <option value="Passengers">6 Passengers and MOT</option>
                <option value="Input">7 Needs more input</option>
            `;
            catSelect.value = savedVal;

            buildDynamicTree();
            renderTaxPositionRegister();
            renderAdminUsersTable();
            updateStatusBar();
        }

        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(screenId).classList.add('active');
        }

        function handleRegistration() {
            const name = document.getElementById('reg-name').value.trim();
            const email = document.getElementById('reg-email').value.trim();
            const phone = document.getElementById('reg-phone').value.trim();

            if(!name || !email || !phone) {
                alert(currentLang === "ar" ? "برجاء ملء جميع الحقول المطلوبة وافية." : "Please fill out all required fields.");
                return;
            }

            const isDuplicate = usersDatabase.some(u => u.email.toLowerCase() === email.toLowerCase() || u.phone === phone);
            if (isDuplicate) {
                alert(currentLang === "ar" ? "خطأ: هذا الحساب أو رقم الهاتف مسجل بالفعل ولا يمكن تكراره." : "Security Error: Unique profile violation, this identity exists.");
                return;
            }

            tempRegData = { name, email, phone, regDate: new Date().toISOString().split('T')[0], isBlocked: false, daysLeft: 15 };
            
            document.getElementById('verify-msg').innerHTML = currentLang === "ar" ? 
                `تم إرسال كود تفعيل مؤلف من 4 أرقام إلى بريدك الإلكتروني: <strong>${email}</strong> <br><br><span style="color:var(--accent);"></span>` :
                `A 4-digit verification code has been dispatched to: <strong>${email}</strong> <br><br><span style="color:var(--accent);">>`;
            
            showScreen('screen-verify');
        }

        function handleVerification() {
            const code = document.getElementById('verify-code').value.trim();
            if(code === "1234") {
                usersDatabase.push(tempRegData);
                activeUser = tempRegData;
                isAdminActive = false;
                alert(currentLang === "ar" ? "تم تفعيل حسابك بنجاح! فترة السماح 15 يوماً." : "Account successfully authorized! 15 days active trial deployed.");
                enterApplication();
            } else {
                alert(currentLang === "ar" ? "كود التحقق غير صحيح، أدخل 1234 للتجربة." : "Invalid code. Enter 1234 for testing.");
            }
        }

        function handleClientLogin() {
            const loginId = document.getElementById('login-client-id').value.trim().toLowerCase();
            const user = usersDatabase.find(u => u.email.toLowerCase() === loginId || u.phone === loginId);
            
            if(user) {
                activeUser = user;
                isAdminActive = false;
                enterApplication();
            } else {
                alert(currentLang === "ar" ? "لم يتم العثور على مستخدم مطابق." : "Client record not found.");
            }
        }

        function handleAdminLogin() {
            const pass = document.getElementById('admin-pass').value;
            if(pass === "admin123") {
                isAdminActive = true;
                activeUser = { name: currentLang === "ar" ? "المدير العام" : "Director " };
                enterApplication();
            } else {
                alert(currentLang === "ar" ? "كلمة مرور الإدارة خاطئة." : "Invalid administrative credentials.");
            }
        }

        function enterApplication() {
            showScreen('screen-main-app');
            document.getElementById('tab-admin').style.display = isAdminActive ? "inline-block" : "none";
            updateStatusBar();
            
            if(isAdminActive) {
                document.getElementById('account-status-bar').style.background = "#fee2e2";
                document.getElementById('block-paywall').style.display = "none";
                document.getElementById('app-content-body').style.display = "block";
                switchTab('admin');
            } else {
                document.getElementById('account-status-bar').style.background = "#eff6ff";
                if(activeUser.isBlocked || activeUser.daysLeft <= 0) {
                    document.getElementById('block-paywall').style.display = "block";
                    document.getElementById('app-content-body').style.display = "none";
                } else {
                    document.getElementById('block-paywall').style.display = "none";
                    document.getElementById('app-content-body').style.display = "block";
                    switchTab('flow');
                }
            }
            renderTaxPositionRegister();
            renderAdminUsersTable();
        }

        function updateStatusBar() {
            if(!activeUser) return;
            document.getElementById('welcome-user-text').innerText = currentLang === "ar" ? 
                `أهلاً بك: ${activeUser.name} ${isAdminActive ? '(لوحة التحكم الفنية للآدمن)' : ''}` :
                `Welcome: ${activeUser.name} ${isAdminActive ? '(Executive Admin Mode)' : ''}`;
            
            if(isAdminActive) {
                document.getElementById('days-left-text').innerText = currentLang === "ar" ? "وضع الإدارة المطلق" : "Absolute Override View";
            } else {
                document.getElementById('days-left-text').innerText = currentLang === "ar" ? 
                    `الأيام المتبقية بفترة السماح: ${activeUser.daysLeft} يوم` : 
                    `Grace Period Remaining: ${activeUser.daysLeft} Days`;
            }
        }

        function logout() {
            activeUser = null;
            isAdminActive = false;
            showScreen('screen-welcome');
        }

        function switchTab(tab) {
            document.querySelectorAll('.tab-content').forEach(c => c.style.display = 'none');
            document.querySelectorAll('.nav-tabs button').forEach(b => b.classList.remove('active'));
            
            document.getElementById(`sub-screen-${tab}`).style.display = 'block';
            document.getElementById(`tab-${tab}`).classList.add('active');
        }

        // --- بناء شجرة الأسئلة ديناميكياً لتتحول مع اللغة ---
        function buildDynamicTree() {
            const cat = document.getElementById('flow-category').value;
            const zone = document.getElementById('dynamic-questions-zone');
            zone.innerHTML = '';
            document.getElementById('flow-result-box').style.display = 'none';

            if(cat === "Transport") {
                zone.innerHTML = currentLang === "ar" ? `
                    <div class="form-group">
                        <label>س1: أين يبدأ مسار عملية النقل الجغرافي للشحنة؟</label>
                        <select id="t-q1" onchange="evaluateTransportExit()">
                            <option value="">-- اختر الإجابة --</option>
                            <option value="outside">خارج دولة الإمارات (Outside the UAE)</option>
                            <option value="inside">داخل دولة الإمارات (Inside the UAE)</option>
                        </select>
                    </div>
                    <div id="transport-next-layer"></div>
                ` : `
                    <div class="form-group">
                        <label>Q1: Where does the physical transit journey originate?</label>
                        <select id="t-q1" onchange="evaluateTransportExit()">
                            <option value="">-- Select Answer --</option>
                            <option value="outside">Outside the UAE</option>
                            <option value="inside">Inside the UAE</option>
                        </select>
                    </div>
                    <div id="transport-next-layer"></div>
                `;
            } else if(cat === "Goods") {
                zone.innerHTML = currentLang === "ar" ? `
                    <div class="form-group">
                        <label>س1: هل تقع البضاعة الحالية تحت وضع التعليق الجمركي / العبور الجمركي؟</label>
                        <select id="g-q1" onchange="evaluateGoodsExit()">
                            <option value="">-- اختر الإجابة --</option>
                            <option value="yes">نعم، تحت وضع التعليق الجمركي (Suspension / Transit)</option>
                            <option value="no">لا، بضائع حرة بالبر الرئيسي (Mainland)</option>
                        </select>
                    </div>
                    <div id="goods-next-layer"></div>
                ` : `
                    <div class="form-group">
                        <label>Q1: Are the goods under Customs Duty Suspension or Transit arrangement?</label>
                        <select id="g-q1" onchange="evaluateGoodsExit()">
                            <option value="">-- Select Answer --</option>
                            <option value="yes">Yes, Customs Suspended / Transit</option>
                            <option value="no">No, Free Circulation Mainland Goods</option>
                        </select>
                    </div>
                    <div id="goods-next-layer"></div>
                `;
            }
        }

        function evaluateTransportExit() {
            const q1 = document.getElementById('t-q1').value;
            const nextLayer = document.getElementById('transport-next-layer');
            nextLayer.innerHTML = '';

            if(q1 === "inside") {
                nextLayer.innerHTML = currentLang === "ar" ? `
                    <div class="form-group">
                        <label>س2: هل تعد الرحلة دولية عابرة للحدود أم شحنة محلية؟</label>
                        <select id="t-q2" onchange="evaluateTransportLeg()">
                            <option value="">-- اختر الإجابة --</option>
                            <option value="intl">رحلة دولية (International)</option>
                            <option value="domestic">رحلة محلية بالكامل داخل الإمارات (Domestic)</option>
                        </select>
                    </div>
                    <div id="transport-leg-layer"></div>
                ` : `
                    <div class="form-group">
                        <label>Q2: Is the specific movement part of cross-border international transit or entirely local?</label>
                        <select id="t-q2" onchange="evaluateTransportLeg()">
                            <option value="">-- Select Answer --</option>
                            <option value="intl">International Voyage</option>
                            <option value="domestic">Purely Local / Domestic Leg</option>
                        </select>
                    </div>
                    <div id="transport-leg-layer"></div>
                `;
            }
        }

        function evaluateTransportLeg() {
            const q2 = document.getElementById('t-q2').value;
            const legLayer = document.getElementById('transport-leg-layer');
            legLayer.innerHTML = '';

            if(q2 === "intl") {
                legLayer.innerHTML = currentLang === "ar" ? `
                    <div class="form-group">
                        <label>س3: هل المتعاقد على نقل المرحلة المحلية هو نفس مورد الشحن الدولي الرئيسي؟</label>
                        <select id="t-q3">
                            <option value="">-- اختر الإجابة --</option>
                            <option value="same">نعم، نفس الناقل لكامل الرحلة بعقد موحد</option>
                            <option value="different">لا، مورد محلي مختلف بعقد منفصل تماماً</option>
                        </select>
                    </div>
                ` : `
                    <div class="form-group">
                        <label>Q3: Is the domestic transit leg billed by the EXACT same international main supplier?</label>
                        <select id="t-q3">
                            <option value="">-- Select Answer --</option>
                            <option value="same">Yes, unified single supplier framework</option>
                            <option value="different">No, separate subcontractor domestic dispatch</option>
                        </select>
                    </div>
                `;
            }
        }

        function evaluateGoodsExit() {
            const q1 = document.getElementById('g-q1').value;
            const nextLayer = document.getElementById('goods-next-layer');
            nextLayer.innerHTML = '';

            if(q1 === "no") {
                nextLayer.innerHTML = currentLang === "ar" ? `
                    <div class="form-group">
                        <label>س2: ما هي طبيعة حركة البضاعة بالدائرة الجمركية؟</label>
                        <select id="g-q2">
                            <option value="">-- اختر الإجابة --</option>
                            <option value="export-evidence">عملية تصدير كاملة ومستندات الإثبات محفوظة بالوقت القانوني</option>
                            <option value="export-missing">عملية تصدير لكن مستندات الإثبات مفقودة أو متأخرة</option>
                            <option value="import-owner">عملية استيراد مباشرة لحساب المالك الفعلي</option>
                        </select>
                    </div>
                ` : `
                    <div class="form-group">
                        <label>Q2: What is the specific customs clearance category?</label>
                        <select id="g-q2">
                            <option value="">-- Select Answer --</option>
                            <option value="export-evidence">Direct Export out of UAE (Official commercial exit proofs secured)</option>
                            <option value="export-missing">Export executed but exit documentation missing/delayed</option>
                            <option value="import-owner">Direct Import on mainland for registered owner</option>
                        </select>
                    </div>
                `;
            }
        }

        function executeEngineDecision() {
            const cat = document.getElementById('flow-category').value;
            let matchedPosition = "P-26";

            if(cat === "Transport") {
                const q1 = document.getElementById('t-q1').value;
                if(q1 === "outside") matchedPosition = "P-15";
                else if(q1 === "inside") {
                    const q2 = document.getElementById('t-q2')?.value;
                    if(q2 === "domestic") matchedPosition = "P-05";
                    else if(q2 === "intl") {
                        const q3 = document.getElementById('t-q3')?.value;
                        if(q3 === "same") matchedPosition = "P-01";
                        if(q3 === "different") matchedPosition = "P-04";
                    }
                }
            } else if(cat === "Goods") {
                const q1 = document.getElementById('g-q1').value;
                if(q1 === "yes") matchedPosition = "P-09";
                else {
                    const q2 = document.getElementById('g-q2').value;
                    if(q2 === "export-evidence") matchedPosition = "P-06";
                    if(q2 === "export-missing") matchedPosition = "P-EVID";
                    if(q2 === "import-owner") matchedPosition = "P-08";
                }
            } else if(cat === "Agency") { matchedPosition = "P-22"; } 
            else if(cat === "Mixed") { matchedPosition = "P-24"; } 
            else if(cat === "Passengers") { matchedPosition = "P-PASS-01"; }

            const resultData = statutoryDatabase.find(p => p.pos === matchedPosition);
            const resBox = document.getElementById('flow-result-box');
            
            resBox.innerHTML = currentLang === "ar" ? `
                <h3>الحكم الضريبي النهائي للمحرك (${resultData.pos}):</h3>
                <p><strong>الفئة القانونية:</strong> ${resultData.cat}</p>
                <p><strong>النسبة المستحقة بالفاتورة:</strong> <span style="color:var(--accent); font-weight:bold; font-size:16px;">${resultData.rate}</span></p>
                <p><strong>المعاملة الجمركية والضريبية:</strong> ${resultData.treatment}</p>
                <p><strong>السند التشريعي:</strong> <em style="color:var(--primary);">${resultData.legal}</em></p>
            ` : `
                <h3>Definitive Engine Tax Ruling (${resultData.pos}):</h3>
                <p><strong>Legal Category:</strong> ${resultData.cat}</p>
                <p><strong>Calculated VAT Rate:</strong> <span style="color:var(--accent); font-weight:bold; font-size:16px;">${resultData.rate}</span></p>
                <p><strong>Tax & Customs Treatment:</strong> ${resultData.treatment}</p>
                <p><strong>Statutory Legal Basis:</strong> <em style="color:var(--primary);">${resultData.legal}</em></p>
            `;
            resBox.style.display = 'block';
        }

        function renderTaxPositionRegister() {
            const thead = document.getElementById('tax-position-thead');
            thead.innerHTML = currentLang === "ar" ? `
                <tr>
                    <th>الرمز (Position)</th>
                    <th>الفئة (Category)</th>
                    <th>الحالة المسببة (Trigger Situation)</th>
                    <th>النسبة (Rate)</th>
                    <th>المعاملة الضريبية</th>
                    <th>السند القانوني (Legal Basis)</th>
                </tr>
            ` : `
                <tr>
                    <th>Code (Position)</th>
                    <th>Category</th>
                    <th>Trigger Situation</th>
                    <th>Rate</th>
                    <th>Tax Treatment</th>
                    <th>Legal Basis</th>
                </tr>
            `;

            const tbody = document.getElementById('tax-position-tbody');
            tbody.innerHTML = '';
            statutoryDatabase.forEach(p => {
                tbody.innerHTML += `
                    <tr>
                        <td><strong>${p.pos}</strong></td>
                        <td>${p.cat}</td>
                        <td>${p.trigger}</td>
                        <td><span class="badge" style="background:#f1f5f9; color:var(--primary);">${p.rate}</span></td>
                        <td>${p.treatment}</td>
                        <td><code>${p.legal}</code></td>
                    </tr>
                `;
            });
        }

        function renderAdminUsersTable() {
            const thead = document.getElementById('admin-users-thead');
            thead.innerHTML = currentLang === "ar" ? `
                <tr>
                    <th>اسم العميل</th>
                    <th>البريد الإلكتروني</th>
                    <th>رقم الهاتف</th>
                    <th>تاريخ التسجيل</th>
                    <th>الحالة الحالية</th>
                    <th>الإجراء والتحكم</th>
                </tr>
            ` : `
                <tr>
                    <th>Client Name</th>
                    <th>Email</th>
                    <th>Phone</th>
                    <th>Registration Date</th>
                    <th>Status</th>
                    <th>Admin Override Action</th>
                </tr>
            `;

            const tbody = document.getElementById('admin-users-tbody');
            tbody.innerHTML = '';
            usersDatabase.forEach((user, index) => {
                const statusBadge = user.isBlocked || user.daysLeft <= 0 ? 
                    `<span class="badge badge-blocked">${currentLang === 'ar' ? 'محجوب / انتهى' : 'Blocked / Expired'}</span>` : 
                    `<span class="badge badge-active">${currentLang === 'ar' ? 'نشط (متبقي ' + user.daysLeft + ' يوم)' : 'Active (' + user.daysLeft + ' d)'}</span>`;
                
                const actionBtn = user.isBlocked ? 
                    `<button class="btn btn-secondary" style="padding:4px 8px; font-size:12px; width:auto;" onclick="toggleBlockUser(${index}, false)">${currentLang === 'ar' ? 'تفعيل وتمكين' : 'Activate User'}</button>` : 
                    `<button class="btn" style="padding:4px 8px; font-size:12px; width:auto; background-color:#ef4444;" onclick="toggleBlockUser(${index}, true)">${currentLang === 'ar' ? 'حظر الحساب' : 'Revoke / Block'}</button>`;

                tbody.innerHTML += `
                    <tr>
                        <td><strong>${user.name}</strong></td>
                        <td>${user.email}</td>
                        <td>${user.phone}</td>
                        <td>${user.regDate}</td>
                        <td>${statusBadge}</td>
                        <td>${actionBtn}</td>
                    </tr>
                `;
            });
        }

        function toggleBlockUser(index, blockStatus) {
            usersDatabase[index].isBlocked = blockStatus;
            usersDatabase[index].daysLeft = blockStatus ? 0 : 15;
            alert(currentLang === "ar" ? "تم تحديث حالة حساب العميل." : "Client compliance state updated.");
            renderAdminUsersTable();
        }

        function filterAdminUsers() {
            const input = document.getElementById('user-search-input').value.toLowerCase();
            const rows = document.getElementById('admin-users-tbody').getElementsByTagName('tr');
            for (let i = 0; i < rows.length; i++) {
                rows[i].style.display = rows[i].innerText.toLowerCase().includes(input) ? "" : "none";
            }
        }

        // تشغيل التهيئة الأولية للواجهة
        applyTranslations();
    </script>
</body>
</html>
