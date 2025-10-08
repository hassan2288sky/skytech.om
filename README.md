<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>نظام التوظيف - سماء التقنية</title>
    <!-- إضافة مكتبة Supabase -->
    <script src="https://unpkg.com/@supabase/supabase-js@2"></script>
    <style>
        /* الأنماط الأصلية تبقى كما هي */
        :root {
            --blue1: #003366;
            --blue2: #007ba7;
            --teal: #00b39f;
            --bg: #f6fbfc;
            --card-bg: #fff;
            --success: #28a745;
            --warning: #ffc107;
            --danger: #dc3545;
        }
        
        * {
            box-sizing: border-box;
        }
        
        body {
            font-family: "Tahoma", sans-serif;
            background: var(--bg);
            margin: 0;
            color: #222;
            line-height: 1.6;
        }
        
        header {
            background: linear-gradient(90deg, var(--blue1), var(--blue2));
            color: #fff;
            padding: 22px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: relative;
        }
        
        .logo-text {
            margin-top: 10px;
            font-size: 24px;
            font-weight: bold;
        }
        
        header h1 {
            margin: 8px 0 0;
            font-size: 20px;
        }
        
        .nav-tabs {
            display: flex;
            background: #fff;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            overflow-x: auto;
        }
        
        .nav-tab {
            padding: 15px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            white-space: nowrap;
            transition: all 0.3s;
        }
        
        .nav-tab.active {
            border-bottom-color: var(--teal);
            color: var(--teal);
            font-weight: bold;
        }
        
        .nav-tab:hover {
            background: #f5f5f5;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .page {
            display: none;
        }
        
        .page.active {
            display: block;
            animation: fadeIn 0.5s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .card {
            background: var(--card-bg);
            padding: 22px;
            border-radius: 10px;
            box-shadow: 0 4px 18px rgba(0,0,0,0.06);
            margin-bottom: 20px;
            border-top: 4px solid var(--blue1);
        }
        
        h2 {
            color: var(--blue1);
            border-right: 4px solid var(--blue1);
            padding-right: 8px;
            display: inline-block;
            margin-top: 0;
        }
        
        h3 {
            color: var(--blue2);
            margin-top: 25px;
        }
        
        p {
            line-height: 1.7;
        }
        
        .actions {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
            margin-top: 20px;
        }
        
        .button {
            display: inline-block;
            padding: 12px 18px;
            border-radius: 8px;
            background: var(--blue1);
            color: #fff;
            text-decoration: none;
            transition: background 0.3s;
            font-weight: bold;
            border: none;
            cursor: pointer;
            text-align: center;
        }
        
        .button:hover {
            background: var(--blue2);
        }
        
        .button.outline {
            background: #fff;
            border: 1px solid var(--blue1);
            color: var(--blue1);
        }
        
        .button.outline:hover {
            background: var(--bg);
        }
        
        .button.success {
            background: var(--success);
        }
        
        .button.warning {
            background: var(--warning);
            color: #333;
        }
        
        .button.danger {
            background: var(--danger);
        }
        
        footer {
            text-align: center;
            color: #666;
            padding: 18px;
            margin-top: 30px;
            border-top: 1px solid #ddd;
        }
        
        /* نمط النموذج */
        label {
            font-weight: bold;
            display: block;
            margin-top: 15px;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 10px;
            border-radius: 6px;
            border: 1px solid #ccc;
            margin-top: 6px;
            font-size: 15px;
            font-family: "Tahoma", sans-serif;
        }
        
        .row {
            display: flex;
            gap: 12px;
        }
        
        .col {
            flex: 1;
        }
        
        .conf {
            background: #e8f8ef;
            border: 1px solid #c8f0df;
            padding: 12px;
            margin-top: 12px;
            border-radius: 8px;
            display: none;
        }
        
        .note {
            color: #666;
            font-size: 14px;
            margin-top: 10px;
        }
        
        /* نمط لوحة الإدارة */
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .stat-card {
            background: #fff;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            text-align: center;
        }
        
        .stat-value {
            font-size: 24px;
            font-weight: bold;
            color: var(--blue1);
            margin: 10px 0;
        }
        
        .applications-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .applications-table th, .applications-table td {
            padding: 12px;
            text-align: right;
            border-bottom: 1px solid #ddd;
        }
        
        .applications-table th {
            background: var(--blue1);
            color: white;
        }
        
        .applications-table tr:hover {
            background: #f5f5f5;
        }
        
        .action-buttons {
            display: flex;
            gap: 5px;
        }
        
        /* نمط صفحة العقد */
        .contract-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #ddd;
        }
        
        .contract-section {
            margin-bottom: 25px;
        }
        
        .clauses {
            background: #f9f9f9;
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
        }
        
        .saved-contracts {
            margin-top: 30px;
        }
        
        .contract-item {
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            background: #fff;
        }
        
        /* طباعة العقد */
        @media print {
            .nav-tabs, .actions, #adminNotice, .saved-contracts {
                display: none !important;
            }
            
            body {
                background: white;
            }
            
            .card {
                box-shadow: none;
                border: 1px solid #ddd;
            }
        }
        
        /* التجاوب مع الشاشات الصغيرة */
        @media (max-width: 768px) {
            .row {
                flex-direction: column;
            }
            
            .nav-tabs {
                flex-direction: column;
            }
            
            .nav-tab {
                text-align: center;
            }
            
            .applications-table {
                display: block;
                overflow-x: auto;
            }
            
            .action-buttons {
                flex-direction: column;
            }
            
            .logo-text {
                font-size: 20px;
            }
        }

        /* أنماط جديدة للموافقة على الشروط */
        .terms-agreement {
            background: #f0f8ff;
            border: 1px solid #cce5ff;
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
        }
        
        .terms-agreement label {
            display: flex;
            align-items: flex-start;
            gap: 10px;
            font-weight: normal;
            margin-top: 0;
            cursor: pointer;
        }
        
        .terms-agreement input[type="checkbox"] {
            width: auto;
            margin-top: 3px;
            cursor: pointer;
        }
        
        .button:disabled {
            background: #ccc;
            cursor: not-allowed;
        }
        
        .error-message {
            color: var(--danger);
            font-size: 14px;
            margin-top: 5px;
            display: none;
        }
        
        /* أنماط الحقول المشروطة */
        .conditional-field {
            display: none;
        }
        
        .skills-group {
            background: #f9f9f9;
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
        }
        
        .skill-item {
            margin-bottom: 15px;
        }
        
        .file-upload {
            border: 2px dashed #ccc;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            margin-top: 10px;
            background: #f8f9fa;
        }
        
        .file-upload:hover {
            border-color: var(--blue2);
        }
        
        /* أنماط الحماية */
        .password-protection {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            padding: 20px;
            border-radius: 8px;
            margin: 20px 0;
            text-align: center;
        }
        
        .password-form {
            max-width: 400px;
            margin: 0 auto;
        }
        
        .admin-only {
            display: none;
        }
        
        .admin-access .admin-only {
            display: block;
        }
        
        .admin-access-section {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
        }

        /* أنماط جديدة لتسجيل الخروج - إظهار دائم في صفحات الإدارة والعقد */
        .logout-section {
            text-align: left;
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }

        /* أنماط جديدة لإظهار/إخفاء كلمة المرور */
        .password-container {
            position: relative;
        }
        
        .toggle-password {
            position: absolute;
            left: 10px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            cursor: pointer;
            font-size: 14px;
            color: #666;
        }
        
        .toggle-password:hover {
            color: var(--blue2);
        }

        /* أنماط جديدة للترقيم التلقائي */
        .serial-number {
            width: 50px;
            text-align: center;
        }

        /* أنماط جديدة لعرض تفاصيل الطلب */
        .application-detail {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
        }
        
        .application-detail h4 {
            color: var(--blue1);
            margin-top: 0;
            margin-bottom: 10px;
        }
        
        .detail-row {
            display: flex;
            margin-bottom: 8px;
        }
        
        .detail-label {
            font-weight: bold;
            width: 200px;
            flex-shrink: 0;
        }
        
        .detail-value {
            flex: 1;
        }

        /* أنماط جديدة لخانات الاختيار */
        .select-all-container {
            margin-bottom: 15px;
            padding: 10px;
            background: #f8f9fa;
            border-radius: 8px;
        }
        
        .export-selected {
            margin-left: 10px;
        }

        /* أنماط جديدة لعرض الملفات */
        .file-info {
            background: #e8f4ff;
            border: 1px solid #b6d7ff;
            border-radius: 6px;
            padding: 10px;
            margin-top: 10px;
        }
        
        .file-name {
            font-weight: bold;
            color: var(--blue1);
        }
        
        .file-size {
            color: #666;
            font-size: 14px;
        }
        
        .no-file {
            color: #999;
            font-style: italic;
        }
        
        /* أنماط جديدة للمزامنة */
        .sync-status {
            padding: 12px;
            margin: 15px 0;
            border-radius: 8px;
            text-align: center;
            display: none;
        }
        
        .sync-success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .sync-error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .sync-loading {
            background: #d1ecf1;
            color: #0c5460;
            border: 1px solid #bee5eb;
        }
    </style>
</head>
<body>

<header>
    <div class="logo-text"> شركة سماء التقنية | Sky Tech</div>
    <h1>إنضم إلى فريقنا في سماء التقنية</h1>
</header>

<div class="nav-tabs">
    <div class="nav-tab active" data-page="home">الصفحة الرئيسية</div>
    <div class="nav-tab admin-only" data-page="admin">لوحة الإدارة</div>
    <div class="nav-tab admin-only" data-page="contract">إنشاء عقد عمل</div>
</div>

<div class="container">
    <!-- الصفحة الرئيسية -->
    <div id="home" class="page active">
        <section class="card">
            <h2>نبذة عن الشركة</h2>
            <p>
                نحن شركة <strong>سماء التقنية ش.م.م</strong> مختصّة في مجال الإلكترونيات وبرمجياتها وتنفيذ المشاريع الهندسية المرتبطة بها،
                كما نوفر القطع الإلكترونية ونقدّم الدورات التدريبية وخدمات الطباعة الثلاثية الأبعاد والـCNC. نبحث عن كفاءات شغوفة بالتقنية.
            </p>
        </section>

        <section class="card">
            <h2>من نبحث عنهم</h2>
            <p>
                أشخاص موهوبون في تركيب الدوائر الإلكترونية، برمجة المتحكمات (Arduino/ESP/Raspberry Pi)، التصميم ثلاثيّ الأبعاد،
                والتعامل العملي مع طابعات 3D. كما نرحّب بذوي الخبرة التدريبية أو مهارات هندسية مشابهة.
            </p>
        </section>

        <section class="card">
            <h2>الشروط والأحكام</h2>
            <ul>
                <li> نظام العمل: عقد جزئي مؤقت مناسب للمهتمين والذين يبحثون عن دخل إضافي .</li>
                <li> يتطلب الحضور لإتمام المهام الموكلة في كثير من الأحيان (شبة يوميا ً خاصة في أوقات الذروة).</li>
                <li> القيام بمهام متعددة.</li>
                <li> لا يوجد راتب ثابت؛ يتم احتساب الأجر بنظام النسبة أو  لكل مهمة متفق عليها.</li>
                <li> السرية وعدم إفشاء مشاريع الشركة أمر ملزم.</li>
                <li> جميع التصاميم والمنتجات الناتجة ملك للشركة.</li>
                <li> في حالة الإنضمام إلى الفريق ، سنقوم بتدريبك و هذا يتطلب الإلتزام بالوقت والحضور، كما يتطلب الإلتزام بالمدة المتفق عليها عند إبرام العقد.</li>
                <li> قادر على تحمل الضغط والإلتزام بأوقات تسليم المشاريع على التواريخ المتفقة.</li>
                <li> خصوصية العملاء و بياناتهم و مشاريعهم أولويتنا القصوى.</li>
                <li> القدرة على التعامل مع العملاء بمختلف الفئات من أفراد و شركات.</li>
                <li> الأولوية لسكان مسقط - المناطق القريبة من الموالح الجنوبية.</li>
                <li> تعبئة النموذج لا تعني القبول النهائي.</li>
            </ul>

            <!-- مربع الموافقة على الشروط والأحكام في الصفحة الرئيسية -->
            <div class="terms-agreement">
                <label>
                    <input type="checkbox" id="agreeTermsHome">
                    <span>أقر بأنني قد قرأت الشروط والأحكام كاملة وأوافق عليها</span>
                </label>
                <div class="error-message" id="termsError">يجب الموافقة على الشروط والأحكام للمتابعة</div>
            </div>

            <div class="actions">
                <button class="button" id="applyButton">تقديم الآن</button>
            </div>

            <!-- قسم الدخول كمسؤول -->
            <div class="admin-access-section">
                <h3>الدخول كمسؤول</h3>
                <div class="password-form">
                    <label>كلمة المرور:</label>
                    <div class="password-container">
                        <input type="password" id="adminAccessPassword" placeholder="أدخل كلمة المرور">
                        <button type="button" class="toggle-password" onclick="togglePasswordVisibility('adminAccessPassword', this)">👁️</button>
                    </div>
                    <button class="button outline" onclick="checkAdminAccessPassword()" style="margin-top: 10px;">الدخول كمسؤول</button>
                    <div class="error-message" id="adminAccessPasswordError">كلمة المرور غير صحيحة</div>
                </div>
            </div>
        </section>
    </div>

    <!-- صفحة تقديم الطلب -->
    <div id="apply" class="page">
        <section class="card">
            <h2>نموذج بيانات المتقدم - سماء التقنية</h2>
            
            <div class="sync-status" id="syncStatus"></div>
            
            <form id="applyForm">
                <h3>معلومات أساسية</h3>
                <label>الاسم الكامل *</label>
                <input type="text" name="fullName" required>

                <div class="row">
                    <div class="col">
                        <label>الجنس</label>
                        <select name="gender" required>
                            <option value="">اختر</option>
                            <option>ذكر</option>
                            <option>أنثى</option>
                        </select>
                    </div>
                </div>

                <label>تاريخ الميلاد</label>
                <input type="date" name="dob">

                <label>رقم البطاقة/الهوية</label>
                <input type="text" name="idNumber">

                <label>رقم الهاتف</label>
                <input type="tel" name="phone">

                <label>البريد الإلكتروني</label>
                <input type="email" name="email">

                <label>عنوان السكن</label>
                <input type="text" name="address">

                <div class="row">
                    <div class="col">
                        <label>هل تملك وسيلة نقل؟</label>
                        <select name="hasTransport">
                            <option value="">اختر</option>
                            <option>نعم</option>
                            <option>لا</option>
                        </select>
                    </div>
                    <div class="col">
                        <label>هل أنت متفرغ؟ *</label>
                        <select name="isAvailable" id="isAvailable" required>
                            <option value="">اختر</option>
                            <option>نعم</option>
                            <option>لا</option>
                        </select>
                    </div>
                </div>

                <!-- حقل توضيح عدم التفرغ -->
                <div class="conditional-field" id="availabilityReasonField">
                    <label>سبب عدم التفرغ *</label>
                    <textarea name="availabilityReason" rows="3" placeholder="يرجى توضيح سبب عدم التفرغ"></textarea>
                </div>

                <h3>المؤهل و الخبرات</h3>
                <label>أعلى مؤهل</label>
                <input type="text" name="education">

                <label>التخصص</label>
                <input type="text" name="specialty">

                <label>الخبرات السابقة (جهة العمل - المدة - المهام)</label>
                <textarea name="experience" rows="3" placeholder="مثال: شركة التقنية - سنتين - برمجة المتحكمات وتصميم الدوائر"></textarea>

                <h3>المهارات</h3>
                <div class="skills-group">
                    <label>التعرف على القطع الإلكترونية المختلفة</label>
                    <select name="skill_electronics">
                        <option value="">اختر</option>
                        <option>مبتدئ</option>
                        <option>متقدم</option>
                        <option>ماهر</option>
                    </select>
                    
                    <label>هل تتعامل مع برامج رسم الدوائر الإلكترونية ومحاكاتها؟</label>
                    <select name="circuit_design_software" id="circuitDesignSoftware">
                        <option value="">اختر</option>
                        <option>نعم</option>
                        <option>لا</option>
                    </select>
                    
                    <div class="conditional-field" id="circuitSoftwareDetailsField">
                        <label>يرجى توضيح برامج رسم الدوائر الإلكترونية التي تتعامل معها</label>
                        <textarea name="circuit_software_details" rows="2" placeholder="مثال: Eagle, KiCad, Proteus..."></textarea>
                    </div>
                </div>
                
                <div class="skills-group">
                    <h4>برمجة المتحكمات</h4>
                    <div class="skill-item">
                        <label>Arduino</label>
                        <select name="skill_arduino">
                            <option value="">اختر</option>
                            <option>مبتدئ</option>
                            <option>متقدم</option>
                            <option>ماهر</option>
                        </select>
                    </div>
                    
                    <div class="skill-item">
                        <label>ESP</label>
                        <select name="skill_ESP">
                            <option value="">اختر</option>
                            <option>مبتدئ</option>
                            <option>متقدم</option>
                            <option>ماهر</option>
                        </select>
                    </div>
                    
                    <div class="skill-item">
                        <label>Raspberry Pi</label>
                        <select name="skill_rpi">
                            <option value="">اختر</option>
                            <option>مبتدئ</option>
                            <option>متقدم</option>
                            <option>ماهر</option>
                        </select>
                    </div>
                    
                    <label>هل لديك خبرة ببرمجة أو تعاملت مع أنواع أخرى من المتحكمات؟</label>
                    <select name="other_controllers" id="otherControllers">
                        <option value="">اختر</option>
                        <option>نعم</option>
                        <option>لا</option>
                    </select>
                    
                    <div class="conditional-field" id="otherControllersField">
                        <div class="row">
                            <div class="col">
                                <label>نوع المتحكمات الأخرى</label>
                                <input type="text" name="other_controllers_type" placeholder="مثال: STM32, PIC, AVR...">
                            </div>
                            <div class="col">
                                <label>مستوى الخبرة</label>
                                <select name="other_controllers_level">
                                    <option value="">اختر</option>
                                    <option>مبتدئ</option>
                                    <option>متقدم</option>
                                    <option>ماهر</option>
                                </select>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="skills-group">
                    <h4>التصميم ثلاثي الأبعاد / التشغيل على طابعات 3D</h4>
                    <div class="row">
                        <div class="col">
                            <label>التصميم ثلاثي الأبعاد</label>
                            <select name="skill_3d_design">
                                <option value="">اختر</option>
                                <option>مبتدئ</option>
                                <option>متقدم</option>
                                <option>ماهر</option>
                            </select>
                        </div>
                        <div class="col">
                            <label>التشغيل على طابعات 3D</label>
                            <select name="skill_3d_printing">
                                <option value="">اختر</option>
                                <option>مبتدئ</option>
                                <option>متقدم</option>
                                <option>ماهر</option>
                            </select>
                        </div>
                    </div>
                    
                    <label>البرامج التي تعاملت معها في تصميم 3D أو CNC</label>
                    <textarea name="design_software" rows="2" placeholder="مثال: Fusion 360, SolidWorks, AutoCAD..."></textarea>
                    
                    <label>الطابعات التي تعاملت معها في 3D أو CNC</label>
                    <textarea name="printers_used" rows="2" placeholder="مثال: Creality Ender 3, Prusa i3, CNC Router..."></textarea>
                </div>

                <h3>خبرات عملية إضافية</h3>
                <label>هل تعاملت مع أي من أجهزة أو أدوات الورشة في مجال الإلكترونيات؟</label>
                <select name="workshop_tools" id="workshopTools">
                    <option value="">اختر</option>
                    <option>نعم</option>
                    <option>لا</option>
                </select>
                
                <div class="conditional-field" id="workshopToolsDetailsField">
                    <label>يرجى توضيح الأدوات التي تعاملت معها</label>
                    <textarea name="workshop_tools_details" rows="2" placeholder="مثال: اللحام، القياس، القطع..."></textarea>
                </div>
                
                <div class="row">
                    <div class="col">
                        <label>هل سبق وتعاملت مع الكهرباء ذات الفولتية العالية؟</label>
                        <select name="high_voltage">
                            <option value="">اختر</option>
                            <option>نعم</option>
                            <option>لا</option>
                        </select>
                    </div>
                    <div class="col">
                        <label>هل سبق وتعاملت مع أدوات ومعدات الورش (النجارة، الحدادة، إلخ)؟</label>
                        <select name="workshop_equipment">
                            <option value="">اختر</option>
                            <option>نعم</option>
                            <option>لا</option>
                        </select>
                    </div>
                </div>

                <h3>ملف السيرة الذاتية</h3>
                <label>إرفاق ملف السيرة الذاتية (PDF) - اختياري</label>
                <div class="file-upload">
                    <input type="file" name="cv_file" id="cv_file" accept=".pdf">
                    <p class="note">يرجى رفع ملف PDF فقط (حجم أقصى 5MB)</p>
                    <button type="button" class="button outline" onclick="confirmPDFUpload()" style="margin-top: 10px;">تأكيد رفع ملف PDF</button>
                </div>

                <h3>تأكيد</h3>
                <label><input type="checkbox" name="agree" required> أقر بأن جميع البيانات صحيحة وأتحمل مسؤولية أي خطأ فيها.</label>

                <button type="submit" class="button" id="submitBtn">إرسال الطلب</button>
            </form>

            <div class="conf" id="confirmation">
                <strong>تم استلام طلبك بنجاح ✅</strong>
                <p>شكراً لتقديمك. سنقوم بالتواصل مع المرشحين المناسبين قريبًا.</p>
            </div>

            <p class="note">ملاحظة: تعبئة النموذج لا تعني قبولًا نهائيًا، وهو خطوة أولية للتقييم.</p>
            
            <div class="actions">
                <button class="button outline" onclick="showPage('home')">العودة للصفحة الرئيسية</button>
            </div>
        </section>
    </div>

    <!-- صفحة العقد -->
    <div id="contract" class="page">
        <section class="card">
            <div class="logout-section">
                <button class="button outline" onclick="logout()">تسجيل الخروج</button>
            </div>
            
            <div class="password-protection" id="contractPasswordProtection">
                <h3>الدخول إلى صفحة إنشاء العقود</h3>
                <p>هذه الصفحة محمية بكلمة مرور للمسؤولين فقط</p>
                <div class="password-form">
                    <label>كلمة المرور:</label>
                    <div class="password-container">
                        <input type="password" id="contractPassword" placeholder="أدخل كلمة المرور">
                        <button type="button" class="toggle-password" onclick="togglePasswordVisibility('contractPassword', this)">👁️</button>
                    </div>
                    <button class="button" onclick="checkContractPassword()" style="margin-top: 10px;">الدخول</button>
                    <div class="error-message" id="contractPasswordError">كلمة المرور غير صحيحة</div>
                </div>
            </div>
            
            <div id="contractContent" class="admin-only">
                <div id="adminNotice">
                    <label>ملاحظة أمنيّة:</label>
                    <p>هذه الصفحة تُفتح عبر لوحة الإدارة. احفظ الرابط في مكان آمن ولا تشاركه.</p>
                    <p class="note">لملء العقد تلقائيًا: استخدم زر "عقد" في لوحة الإدارة، أو ضع المعطيات يدوياً أدناه.</p>
                </div>

                <div class="contract-header">
                    <div><strong id="contractNumber">رقم العقد: SKY-XXXX-XXX</strong></div>
                    <div id="contractDate">تاريخ العقد: --/--/----</div>
                </div>

                <h2>عقد عمل جزئي - سماء التقنية</h2>

                <div class="contract-section">
                    <h3>بيانات الموظف</h3>
                    <label>الاسم الكامل</label><input id="c_name" type="text">
                    <label>رقم الهوية / الإقامة</label><input id="c_id" type="text">
                    <label>العنوان</label><input id="c_address" type="text">
                    <div class="row">
                        <div class="col">
                            <label>المجال / المهارة</label><input id="c_skill" type="text">
                        </div>
                        <div class="col">
                            <label>النسبة المتفق عليها (%)</label><input id="c_rate" type="number">
                        </div>
                    </div>
                    <label>تاريخ البدء</label><input id="c_start" type="date">
                </div>

                <div class="contract-section">
                    <h3>بيانات الشركة</h3>
                    <p><strong>الاسم التجاري:</strong> شركة سماء التقنية ش.م.م (Sky Tech)</p>
                    <p><strong>العنوان:</strong> سلطنة عمان</p>
                    <p><strong>السجل التجاري:</strong> 0000000</p>
                    <p><strong>ممثل الشركة:</strong> الإدارة العامة</p>
                </div>

                <div class="contract-section">
                    <h3>بنود العقد</h3>
                    <div class="clauses" id="clauses">
                        <p>1. هذا عقد عمل جزئي بموجب مهمة محددة بين شركة سماء التقنية والطرف الثاني (الموظف).</p>
                        <p>2. لا يوجد راتب ثابت، ويُحتسب الأجر حسب النسبة المتفق عليها لكل مهمة.</p>
                        <p>3. يلتزم الموظف بالحضور إلى مقر الشركة لتنفيذ المهام المتفق عليها.</p>
                        <p>4. على الموظف الحفاظ على سرية المعلومات وعدم إفشاء البيانات.</p>
                        <p>5. يحق للطرفين إنهاء العقد بعد إشعار مسبق.</p>
                    </div>
                </div>

                <div class="contract-section">
                    <h3>التوقيعات</h3>
                    <div class="row">
                        <div class="col">
                            <label>توقيع الموظف (اكتب الاسم أو توقيع إلكتروني)</label>
                            <input id="sig_emp" type="text">
                        </div>
                        <div class="col">
                            <label>توقيع ممثل الشركة</label>
                            <input id="sig_comp" type="text" value="الإدارة العامة">
                        </div>
                    </div>
                </div>

                <div class="actions">
                    <button class="button" id="fillFromData">ملء تلقائي من بيانات (إن وجدت)</button>
                    <button class="button warning" id="printBtn">🖨️ طباعة / حفظ كـ PDF</button>
                    <button class="button success" id="saveLocal">💾 حفظ بالعقدات المحفوظة</button>
                    <button class="button outline" onclick="showPage('home')">العودة للرئيسية</button>
                </div>

                <p class="note">يمكنك تعديل أي حقل قبل الطباعة. سيولد رقم وعنوان تلقائيًا عند فتح الصفحة عبر لوحة الإدارة.</p>
            </div>

            <section class="card saved-contracts admin-only" id="savedListCard" style="display:none">
                <h3>العقود المحفوظة (محليًا)</h3>
                <div id="savedList"></div>
            </section>
        </section>
    </div>

    <!-- لوحة الإدارة -->
    <div id="admin" class="page">
        <section class="card">
            <div class="logout-section">
                <button class="button outline" onclick="logout()">تسجيل الخروج</button>
            </div>
            
            <div class="password-protection" id="adminPasswordProtection">
                <h3>الدخول إلى لوحة الإدارة</h3>
                <p>هذه الصفحة محمية بكلمة مرور للمسؤولين فقط</p>
                <div class="password-form">
                    <label>كلمة المرور:</label>
                    <div class="password-container">
                        <input type="password" id="adminPassword" placeholder="أدخل كلمة المرور">
                        <button type="button" class="toggle-password" onclick="togglePasswordVisibility('adminPassword', this)">👁️</button>
                    </div>
                    <button class="button" onclick="checkAdminPassword()" style="margin-top: 10px;">الدخول</button>
                    <div class="error-message" id="adminPasswordError">كلمة المرور غير صحيحة</div>
                </div>
            </div>
            
            <div id="adminContent" class="admin-only">
                <h2>لوحة إدارة طلبات التوظيف</h2>
                
                <div class="sync-status" id="adminSyncStatus"></div>
                
                <div class="stats">
                    <div class="stat-card">
                        <div>إجمالي الطلبات</div>
                        <div class="stat-value" id="totalApplications">0</div>
                    </div>
                    <div class="stat-card">
                        <div>المتقدمين الجدد</div>
                        <div class="stat-value" id="newApplications">0</div>
                    </div>
                    <div class="stat-card">
                        <div>العقود المحفوظة</div>
                        <div class="stat-value" id="totalContracts">0</div>
                    </div>
                    <div class="stat-card">
                        <div>عدد الزوار</div>
                        <div class="stat-value" id="totalVisitors">0</div>
                    </div>
                </div>

                <div class="actions">
                    <button class="button outline" onclick="exportAllData()">📥 تصدير جميع البيانات (Excel)</button>
                    <button class="button success export-selected" onclick="exportSelectedData()">📥 تصدير المحدد (Excel)</button>
                    <button class="button danger" onclick="clearAllData()">🗑️ حذف جميع البيانات</button>
                    <button class="button" onclick="showPage('contract')">إنشاء عقد</button>
                    <button class="button outline" onclick="showPage('home')">العودة للرئيسية</button>
                </div>

                <div class="select-all-container">
                    <label>
                        <input type="checkbox" id="selectAllApplications" onchange="toggleSelectAll(this.checked)">
                        تحديد/إلغاء تحديد جميع الطلبات
                    </label>
                </div>

                <h3>الطلبات المقدمة</h3>
                <div id="applicationsList">
                    <p>جاري تحميل البيانات...</p>
                </div>
            </div>
        </section>
    </div>

    <!-- صفحة عرض تفاصيل الطلب -->
    <div id="applicationDetail" class="page">
        <section class="card">
            <div class="logout-section admin-only">
                <button class="button outline" onclick="showPage('admin')">العودة إلى لوحة الإدارة</button>
            </div>
            
            <h2>تفاصيل الطلب</h2>
            <div id="applicationDetailContent">
                <p>جاري تحميل البيانات...</p>
            </div>
        </section>
    </div>
</div>

<footer>
    © جميع الحقوق محفوظة لشركة سماء التقنية ش.م.م | Sky Tech
</footer>

<script>
    // =============================================
    // الإعدادات الأساسية
    // =============================================
    
    // الثوابت والمتغيرات العامة
    const STORAGE_KEY = 'skytech_responses';
    const STORAGE_CONTRACTS = 'skytech_contracts';
    const STORAGE_FILES = 'skytech_uploaded_files';
    const VISITOR_COUNT_KEY = 'skytech_visitor_count';
    const ADMIN_PASSWORD = 'sky222025';
    const LOGIN_STATUS_KEY = 'skytech_admin_logged_in';
    
    // =============================================
    // إعدادات Supabase - استبدل هذه القيم بمعلومات مشروعك
    // =============================================
    const SUPABASE_URL = 'https://wmtfeavgzrotcjjfmsxk.supabase.co'; // استبدل بـ URL مشروعك
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6IndtdGZlYXZnenJvdGNqamZtc3hrIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTk5MTA1OTYsImV4cCI6MjA3NTQ4NjU5Nn0.T7EguSI_idH8BbnEdDbgSHKcySpomHsWq98_GODs5V0'; // استبدل بـ Anon Key مشروعك
    
    // تهيئة Supabase
    const supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
    
    // =============================================
    // دوال إدارة الحالة
    // =============================================
    
    // إظهار رسالة حالة المزامنة
    function showSyncStatus(message, type, elementId = 'syncStatus') {
        const statusEl = document.getElementById(elementId);
        statusEl.textContent = message;
        statusEl.className = 'sync-status';
        statusEl.classList.add(`sync-${type}`);
        statusEl.style.display = 'block';
        
        if (type !== 'loading') {
            setTimeout(() => {
                statusEl.style.display = 'none';
            }, 5000);
        }
    }
    
    // =============================================
    // دوال Supabase
    // =============================================
    
    // مزامنة البيانات المحلية مع Supabase
    async function syncWithSupabase() {
        try {
            showSyncStatus('جاري مزامنة البيانات مع السحابة...', 'loading');
            
            // مزامنة الطلبات
            const localApplications = loadResponses();
            if (localApplications.length > 0) {
                for (const app of localApplications) {
                    await saveApplicationToSupabase(app);
                }
            }

            // مزامنة العقود
            const localContracts = loadContracts();
            if (localContracts.length > 0) {
                for (const contract of localContracts) {
                    await saveContractToSupabase(contract);
                }
            }

            showSyncStatus('✅ تمت مزامنة البيانات مع السحابة بنجاح', 'success');
        } catch (error) {
            console.error('خطأ في المزامنة:', error);
            showSyncStatus('❌ فشل في مزامنة البيانات مع السحابة', 'error');
        }
    }

    // حفظ طلب في Supabase
    async function saveApplicationToSupabase(application) {
        try {
            const { data, error } = await supabase
                .from('applications')
                .upsert({
                    local_id: application._id,
                    full_name: application.fullName,
                    gender: application.gender,
                    dob: application.dob,
                    id_number: application.idNumber,
                    phone: application.phone,
                    email: application.email,
                    address: application.address,
                    has_transport: application.hasTransport,
                    is_available: application.isAvailable,
                    availability_reason: application.availabilityReason,
                    education: application.education,
                    specialty: application.specialty,
                    experience: application.experience,
                    skill_electronics: application.skill_electronics,
                    circuit_design_software: application.circuit_design_software,
                    circuit_software_details: application.circuit_software_details,
                    skill_arduino: application.skill_arduino,
                    skill_esp: application.skill_ESP,
                    skill_rpi: application.skill_rpi,
                    other_controllers: application.other_controllers,
                    other_controllers_type: application.other_controllers_type,
                    other_controllers_level: application.other_controllers_level,
                    skill_3d_design: application.skill_3d_design,
                    skill_3d_printing: application.skill_3d_printing,
                    design_software: application.design_software,
                    printers_used: application.printers_used,
                    workshop_tools: application.workshop_tools,
                    workshop_tools_details: application.workshop_tools_details,
                    high_voltage: application.high_voltage,
                    workshop_equipment: application.workshop_equipment,
                    has_file: application._hasFile,
                    file_name: application._fileName,
                    file_size: application._fileSize,
                    submitted_at: application._submittedAt,
                    created_at: new Date().toISOString()
                }, {
                    onConflict: 'local_id'
                });

            if (error) throw error;
            return data;
        } catch (error) {
            console.error('خطأ في حفظ الطلب:', error);
            throw error;
        }
    }

    // حفظ عقد في Supabase
    async function saveContractToSupabase(contract) {
        try {
            const { data, error } = await supabase
                .from('contracts')
                .upsert({
                    contract_number: contract.contractNumber,
                    contract_date: contract.contractDate,
                    employee_name: contract.name,
                    employee_id: contract.id,
                    employee_address: contract.address,
                    employee_skill: contract.skill,
                    rate_percentage: contract.rate,
                    start_date: contract.start,
                    employee_signature: contract.empSig,
                    company_signature: contract.compSig,
                    saved_at: contract.savedAt,
                    created_at: new Date().toISOString()
                }, {
                    onConflict: 'contract_number'
                });

            if (error) throw error;
            return data;
        } catch (error) {
            console.error('خطأ في حفظ العقد:', error);
            throw error;
        }
    }

    // جلب جميع الطلبات من Supabase
    async function loadApplicationsFromSupabase() {
        try {
            const { data, error } = await supabase
                .from('applications')
                .select('*')
                .order('created_at', { ascending: false });

            if (error) throw error;
            return data || [];
        } catch (error) {
            console.error('خطأ في جلب الطلبات:', error);
            return [];
        }
    }

    // جلب جميع العقود من Supabase
    async function loadContractsFromSupabase() {
        try {
            const { data, error } = await supabase
                .from('contracts')
                .select('*')
                .order('created_at', { ascending: false });

            if (error) throw error;
            return data || [];
        } catch (error) {
            console.error('خطأ في جلب العقود:', error);
            return [];
        }
    }

    // دالة محسنة لتحميل الطلبات (تدمج البيانات المحلية والسحابية)
    async function enhancedLoadApplications() {
        try {
            showSyncStatus('جاري تحميل البيانات من السحابة...', 'loading', 'adminSyncStatus');
            
            // جلب البيانات من السحابة
            const cloudApplications = await loadApplicationsFromSupabase();
            
            // جلب البيانات المحلية
            const localApplications = loadResponses();
            
            // دمج البيانات (إعطاء الأولوية للسحابة)
            const allApplications = [...cloudApplications, ...localApplications];
            
            // إزالة التكرارات بناءً على local_id
            const uniqueApplications = allApplications.filter((app, index, self) =>
                index === self.findIndex(a => 
                    (a.local_id && a.local_id === app.local_id) || 
                    (a._id && a._id === app._id)
                )
            );
            
            showSyncStatus('✅ تم تحميل البيانات بنجاح', 'success', 'adminSyncStatus');
            return uniqueApplications;
        } catch (error) {
            console.error('خطأ في تحميل البيانات:', error);
            showSyncStatus('❌ فشل في تحميل البيانات من السحابة', 'error', 'adminSyncStatus');
            return loadResponses(); // العودة للبيانات المحلية في حالة الخطأ
        }
    }

    // دالة محسنة لحفظ الطلبات (تحفظ في كلا المكانين)
    async function enhancedSaveApplication(application) {
        // الحفظ المحلي (كما كان)
        const arr = loadResponses();
        arr.push(application);
        saveResponses(arr);
        
        // الحفظ في السحابة
        try {
            await saveApplicationToSupabase(application);
        } catch (error) {
            console.warn('تعذر الحفظ في السحابة، سيتم الاعتماد على التخزين المحلي');
        }
    }

    // =============================================
    // الدوال الأصلية (مع تعديلات طفيفة لدعم Supabase)
    // =============================================
    
    // إضافة دالة للتحقق من رفع ملف PDF
    function confirmPDFUpload() {
        const fileInput = document.getElementById('cv_file');
        if (fileInput && fileInput.files.length > 0) {
            const file = fileInput.files[0];
            if (file.type === 'application/pdf') {
                if (file.size <= 5 * 1024 * 1024) { // 5MB
                    alert('✓ تم تأكيد رفع ملف PDF بنجاح: ' + file.name);
                    return true;
                } else {
                    alert('❌ حجم الملف كبير جداً. الحد الأقصى 5MB');
                    return false;
                }
            } else {
                alert('❌ يرجى اختيار ملف PDF فقط');
                return false;
            }
        } else {
            alert('⚠️ لم يتم اختيار أي ملف لرفعه');
            return false;
        }
    }
    
    // وظيفة لتحويل الملف إلى Base64
    function fileToBase64(file) {
        return new Promise((resolve, reject) => {
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = () => resolve(reader.result);
            reader.onerror = error => reject(error);
        });
    }
    
    // وظائف إدارة الملفات
    function loadFiles() {
        try {
            const raw = localStorage.getItem(STORAGE_FILES);
            if (!raw) return {};
            return JSON.parse(raw);
        } catch (e) {
            return {};
        }
    }
    
    function saveFiles(filesObj) {
        localStorage.setItem(STORAGE_FILES, JSON.stringify(filesObj));
    }
    
    // وظائف التنقل بين الصفحات
    function showPage(pageId) {
        document.querySelectorAll('.page').forEach(page => {
            page.classList.remove('active');
        });
        
        document.getElementById(pageId).classList.add('active');
        
        document.querySelectorAll('.nav-tab').forEach(tab => {
            tab.classList.remove('active');
            if (tab.getAttribute('data-page') === pageId) {
                tab.classList.add('active');
            }
        });
        
        if (pageId === 'admin') {
            loadApplications();
            updateStats();
        }
    }
    
    // التحقق من حالة تسجيل الدخول
    function checkLoginStatus() {
        return localStorage.getItem(LOGIN_STATUS_KEY) === 'true';
    }
    
    // حفظ حالة تسجيل الدخول
    function setLoginStatus(loggedIn) {
        localStorage.setItem(LOGIN_STATUS_KEY, loggedIn.toString());
    }
    
    // تسجيل الدخول العام
    function login() {
        document.body.classList.add('admin-access');
        setLoginStatus(true);
        
        document.querySelectorAll('.nav-tab.admin-only').forEach(tab => {
            tab.style.display = 'block';
        });
        
        document.getElementById('adminPasswordProtection').style.display = 'none';
        document.getElementById('contractPasswordProtection').style.display = 'none';
        
        document.getElementById('adminContent').style.display = 'block';
        document.getElementById('contractContent').style.display = 'block';
    }
    
    // تسجيل الخروج
    function logout() {
        document.body.classList.remove('admin-access');
        setLoginStatus(false);
        
        document.querySelectorAll('.nav-tab.admin-only').forEach(tab => {
            tab.style.display = 'none';
        });
        
        document.getElementById('adminPasswordProtection').style.display = 'block';
        document.getElementById('contractPasswordProtection').style.display = 'block';
        
        document.getElementById('adminContent').style.display = 'none';
        document.getElementById('contractContent').style.display = 'none';
        
        showPage('home');
        
        document.getElementById('adminPassword').value = '';
        document.getElementById('contractPassword').value = '';
        document.getElementById('adminAccessPassword').value = '';
        
        document.getElementById('adminPasswordError').style.display = 'none';
        document.getElementById('contractPasswordError').style.display = 'none';
        document.getElementById('adminAccessPasswordError').style.display = 'none';
    }
    
    // التحقق من كلمة مرور الإدارة
    function checkAdminPassword() {
        const password = document.getElementById('adminPassword').value;
        const errorElement = document.getElementById('adminPasswordError');
        
        if (password === ADMIN_PASSWORD) {
            login();
            loadApplications();
            updateStats();
        } else {
            errorElement.style.display = 'block';
        }
    }
    
    // التحقق من كلمة مرور العقد
    function checkContractPassword() {
        const password = document.getElementById('contractPassword').value;
        const errorElement = document.getElementById('contractPasswordError');
        
        if (password === ADMIN_PASSWORD) {
            login();
            renderSavedContracts();
        } else {
            errorElement.style.display = 'block';
        }
    }
    
    // التحقق من كلمة مرور الوصول كمسؤول من الصفحة الرئيسية
    function checkAdminAccessPassword() {
        const password = document.getElementById('adminAccessPassword').value;
        const errorElement = document.getElementById('adminAccessPasswordError');
        
        if (password === ADMIN_PASSWORD) {
            login();
            showPage('admin');
        } else {
            errorElement.style.display = 'block';
        }
    }
    
    // إظهار/إخفاء كلمة المرور
    function togglePasswordVisibility(passwordFieldId, button) {
        const passwordField = document.getElementById(passwordFieldId);
        if (passwordField.type === 'password') {
            passwordField.type = 'text';
        } else {
            passwordField.type = 'password';
        }
    }
    
    // زيادة عدد الزوار
    function incrementVisitorCount() {
        let count = localStorage.getItem(VISITOR_COUNT_KEY);
        if (!count) {
            count = 0;
        }
        count = parseInt(count) + 1;
        localStorage.setItem(VISITOR_COUNT_KEY, count.toString());
        return count;
    }
    
    // الحصول على عدد الزوار
    function getVisitorCount() {
        let count = localStorage.getItem(VISITOR_COUNT_KEY);
        if (!count) {
            count = 0;
            localStorage.setItem(VISITOR_COUNT_KEY, count.toString());
        }
        return parseInt(count);
    }
    
    // التحقق من الموافقة على الشروط قبل الانتقال لصفحة التقديم
    document.getElementById('applyButton').addEventListener('click', function() {
        const agreeCheckbox = document.getElementById('agreeTermsHome');
        const errorMessage = document.getElementById('termsError');
        
        if (!agreeCheckbox.checked) {
            errorMessage.style.display = 'block';
            agreeCheckbox.focus();
        } else {
            errorMessage.style.display = 'none';
            showPage('apply');
        }
    });
    
    // إخفاء رسالة الخطأ عند تحديد المربع
    document.getElementById('agreeTermsHome').addEventListener('change', function() {
        if (this.checked) {
            document.getElementById('termsError').style.display = 'none';
        }
    });
    
    // إضافة مستمعي الأحداث للتبويبات
    document.querySelectorAll('.nav-tab').forEach(tab => {
        tab.addEventListener('click', function() {
            showPage(this.getAttribute('data-page'));
        });
    });
    
    // التحكم في الحقول المشروطة
    document.getElementById('isAvailable').addEventListener('change', function() {
        const reasonField = document.getElementById('availabilityReasonField');
        if (this.value === 'لا') {
            reasonField.style.display = 'block';
            reasonField.querySelector('textarea').required = true;
        } else {
            reasonField.style.display = 'none';
            reasonField.querySelector('textarea').required = false;
        }
    });
    
    document.getElementById('circuitDesignSoftware').addEventListener('change', function() {
        const detailsField = document.getElementById('circuitSoftwareDetailsField');
        if (this.value === 'نعم') {
            detailsField.style.display = 'block';
        } else {
            detailsField.style.display = 'none';
        }
    });
    
    document.getElementById('otherControllers').addEventListener('change', function() {
        const otherField = document.getElementById('otherControllersField');
        if (this.value === 'نعم') {
            otherField.style.display = 'block';
        } else {
            otherField.style.display = 'none';
        }
    });
    
    document.getElementById('workshopTools').addEventListener('change', function() {
        const detailsField = document.getElementById('workshopToolsDetailsField');
        if (this.value === 'نعم') {
            detailsField.style.display = 'block';
        } else {
            detailsField.style.display = 'none';
        }
    });
    
    // وظائف إدارة التخزين المحلي
    function loadResponses() {
        try {
            const raw = localStorage.getItem(STORAGE_KEY);
            if (!raw) return [];
            return JSON.parse(raw);
        } catch (e) {
            return [];
        }
    }
    
    function saveResponses(arr) {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(arr));
    }
    
    function loadContracts() {
        try {
            const raw = localStorage.getItem(STORAGE_CONTRACTS);
            if (!raw) return [];
            return JSON.parse(raw);
        } catch (e) {
            return [];
        }
    }
    
    function saveContracts(arr) {
        localStorage.setItem(STORAGE_CONTRACTS, JSON.stringify(arr));
    }
    
    // معالجة نموذج التقديم
    document.getElementById('applyForm').addEventListener('submit', async function(e){
        e.preventDefault();
        const form = e.target;
        const fd = new FormData(form);
        const obj = {};
        fd.forEach((v,k) => obj[k]=v);
        
        // إضافة بيانات ووقت الإرسال
        obj._submittedAt = new Date().toISOString();
        obj._id = Date.now().toString();
        
        // معالجة ملف PDF إذا تم رفعه
        const fileInput = document.getElementById('cv_file');
        if (fileInput && fileInput.files.length > 0) {
            const file = fileInput.files[0];
            if (file.type === 'application/pdf' && file.size <= 5 * 1024 * 1024) {
                try {
                    const fileData = await fileToBase64(file);
                    const fileInfo = {
                        name: file.name,
                        size: file.size,
                        type: file.type,
                        data: fileData,
                        uploadedAt: new Date().toISOString()
                    };
                    
                    // حفظ الملف في التخزين المنفصل
                    const files = loadFiles();
                    files[obj._id] = fileInfo;
                    saveFiles(files);
                    
                    obj._hasFile = true;
                    obj._fileName = file.name;
                    obj._fileSize = file.size;
                } catch (error) {
                    console.error('Error processing file:', error);
                    obj._hasFile = false;
                }
            }
        } else {
            obj._hasFile = false;
        }
        
        // الحفظ المحلي وفي السحابة
        await enhancedSaveApplication(obj);
        
        // إعادة تعيين النموذج وإظهار رسالة التأكيد
        form.reset();
        document.getElementById('confirmation').style.display='block';
        document.getElementById('confirmation').scrollIntoView({behavior:'smooth'});
        
        // إعادة تعيين الحقول المشروطة
        document.querySelectorAll('.conditional-field').forEach(field => {
            field.style.display = 'none';
        });
        
        // تحديث الإحصائيات إذا كنا في صفحة الإدارة
        if (document.getElementById('admin').classList.contains('active')) {
            loadApplications();
            updateStats();
        }
    });
    
    // وظائف لوحة الإدارة
    async function loadApplications() {
        const applications = await enhancedLoadApplications();
        const container = document.getElementById('applicationsList');
        
        if (applications.length === 0) {
            container.innerHTML = '<p>لا توجد طلبات مقدمه حتى الآن.</p>';
            return;
        }
        
        let html = `
            <table class="applications-table">
                <thead>
                    <tr>
                        <th class="serial-number">#</th>
                        <th><input type="checkbox" id="selectAllHeader" onchange="toggleSelectAll(this.checked)"></th>
                        <th>الاسم</th>
                        <th>الهاتف</th>
                        <th>البريد</th>
                        <th>ملف PDF</th>
                        <th>تاريخ التقديم</th>
                        <th>الإجراءات</th>
                    </tr>
                </thead>
                <tbody>
        `;
        
        applications.forEach((app, index) => {
            const submittedAt = app._submittedAt || app.submitted_at;
            const date = new Date(submittedAt).toLocaleDateString('ar-EG');
            const hasFile = app._hasFile || app.has_file;
            const fileName = app._fileName || app.file_name;
            const fileSize = app._fileSize || app.file_size;
            
            const fileInfo = hasFile ? 
                `<span class="file-name">${fileName}</span><br><span class="file-size">(${(fileSize / 1024).toFixed(2)} KB)</span>` : 
                '<span class="no-file">لا يوجد ملف</span>';
            
            const appId = app._id || app.local_id;
            
            html += `
                <tr>
                    <td class="serial-number">${index + 1}</td>
                    <td><input type="checkbox" class="application-checkbox" value="${appId}"></td>
                    <td>${app.fullName || app.full_name || 'غير مذكور'}</td>
                    <td>${app.phone || 'غير مذكور'}</td>
                    <td>${app.email || 'غير مذكور'}</td>
                    <td>${fileInfo}</td>
                    <td>${date}</td>
                    <td>
                        <div class="action-buttons">
                            <button class="button" onclick="viewApplicationDetail('${appId}')">عرض</button>
                            <button class="button outline" onclick="generateContract('${appId}')">عقد</button>
                            <button class="button danger" onclick="deleteApplication('${appId}')">حذف</button>
                            ${hasFile ? `<button class="button success" onclick="downloadFile('${appId}')">📥 تحميل PDF</button>` : ''}
                        </div>
                    </td>
                </tr>
            `;
        });
        
        html += '</tbody></table>';
        container.innerHTML = html;
    }
    
    // تحميل ملف PDF
    function downloadFile(applicationId) {
        const files = loadFiles();
        const fileInfo = files[applicationId];
        
        if (fileInfo && fileInfo.data) {
            const link = document.createElement('a');
            link.href = fileInfo.data;
            link.download = fileInfo.name || 'السيرة_الذاتية.pdf';
            link.click();
        } else {
            alert('❌ الملف غير موجود أو تم حذفه');
        }
    }
    
    // تحديد/إلغاء تحديد جميع الطلبات
    function toggleSelectAll(checked) {
        const checkboxes = document.querySelectorAll('.application-checkbox');
        checkboxes.forEach(checkbox => {
            checkbox.checked = checked;
        });
        document.getElementById('selectAllHeader').checked = checked;
        document.getElementById('selectAllApplications').checked = checked;
    }
    
    // عرض تفاصيل الطلب في صفحة جديدة
    async function viewApplicationDetail(id) {
        const applications = await enhancedLoadApplications();
        const app = applications.find(a => (a._id === id) || (a.local_id === id));
        
        if (!app) {
            alert('لم يتم العثور على الطلب');
            return;
        }
        
        let details = `
            <div class="application-detail">
                <h4>المعلومات الأساسية</h4>
                <div class="detail-row">
                    <div class="detail-label">الاسم الكامل:</div>
                    <div class="detail-value">${app.fullName || app.full_name || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">الجنس:</div>
                    <div class="detail-value">${app.gender || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">تاريخ الميلاد:</div>
                    <div class="detail-value">${app.dob || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">رقم البطاقة/الهوية:</div>
                    <div class="detail-value">${app.idNumber || app.id_number || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">رقم الهاتف:</div>
                    <div class="detail-value">${app.phone || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">البريد الإلكتروني:</div>
                    <div class="detail-value">${app.email || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">عنوان السكن:</div>
                    <div class="detail-value">${app.address || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">وسيلة نقل:</div>
                    <div class="detail-value">${app.hasTransport || app.has_transport || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">التفرغ:</div>
                    <div class="detail-value">${app.isAvailable || app.is_available || 'غير مذكور'}</div>
                </div>
                ${(app.availabilityReason || app.availability_reason) ? `
                <div class="detail-row">
                    <div class="detail-label">سبب عدم التفرغ:</div>
                    <div class="detail-value">${app.availabilityReason || app.availability_reason}</div>
                </div>
                ` : ''}
            </div>
            
            <div class="application-detail">
                <h4>المؤهل والخبرات</h4>
                <div class="detail-row">
                    <div class="detail-label">أعلى مؤهل:</div>
                    <div class="detail-value">${app.education || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">التخصص:</div>
                    <div class="detail-value">${app.specialty || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">الخبرات السابقة:</div>
                    <div class="detail-value">${app.experience || 'غير مذكور'}</div>
                </div>
            </div>
            
            <div class="application-detail">
                <h4>المهارات التقنية</h4>
                <div class="detail-row">
                    <div class="detail-label">التعرف على القطع الإلكترونية:</div>
                    <div class="detail-value">${app.skill_electronics || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">برامج رسم الدوائر:</div>
                    <div class="detail-value">${app.circuit_design_software || 'غير مذكور'}</div>
                </div>
                ${(app.circuit_software_details) ? `
                <div class="detail-row">
                    <div class="detail-label">تفاصيل برامج رسم الدوائر:</div>
                    <div class="detail-value">${app.circuit_software_details}</div>
                </div>
                ` : ''}
                <div class="detail-row">
                    <div class="detail-label">برمجة Arduino:</div>
                    <div class="detail-value">${app.skill_arduino || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">برمجة ESP:</div>
                    <div class="detail-value">${app.skill_ESP || app.skill_esp || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">برمجة Raspberry Pi:</div>
                    <div class="detail-value">${app.skill_rpi || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">متحكمات أخرى:</div>
                    <div class="detail-value">${app.other_controllers || 'غير مذكور'}</div>
                </div>
                ${(app.other_controllers_type) ? `
                <div class="detail-row">
                    <div class="detail-label">نوع المتحكمات الأخرى:</div>
                    <div class="detail-value">${app.other_controllers_type}</div>
                </div>
                ` : ''}
                ${(app.other_controllers_level) ? `
                <div class="detail-row">
                    <div class="detail-label">مستوى المتحكمات الأخرى:</div>
                    <div class="detail-value">${app.other_controllers_level}</div>
                </div>
                ` : ''}
            </div>
            
            <div class="application-detail">
                <h4>التصميم ثلاثي الأبعاد والطباعة</h4>
                <div class="detail-row">
                    <div class="detail-label">التصميم ثلاثي الأبعاد:</div>
                    <div class="detail-value">${app.skill_3d_design || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">التشغيل على طابعات 3D:</div>
                    <div class="detail-value">${app.skill_3d_printing || 'غير مذكور'}</div>
                </div>
                ${(app.design_software) ? `
                <div class="detail-row">
                    <div class="detail-label">برامج التصميم:</div>
                    <div class="detail-value">${app.design_software}</div>
                </div>
                ` : ''}
                ${(app.printers_used) ? `
                <div class="detail-row">
                    <div class="detail-label">الطابعات المستخدمة:</div>
                    <div class="detail-value">${app.printers_used}</div>
                </div>
                ` : ''}
            </div>
            
            <div class="application-detail">
                <h4>خبرات عملية إضافية</h4>
                <div class="detail-row">
                    <div class="detail-label">أدوات الورشة:</div>
                    <div class="detail-value">${app.workshop_tools || 'غير مذكور'}</div>
                </div>
                ${(app.workshop_tools_details) ? `
                <div class="detail-row">
                    <div class="detail-label">تفاصيل أدوات الورشة:</div>
                    <div class="detail-value">${app.workshop_tools_details}</div>
                </div>
                ` : ''}
                <div class="detail-row">
                    <div class="detail-label">الكهرباء ذات الفولتية العالية:</div>
                    <div class="detail-value">${app.high_voltage || 'غير مذكور'}</div>
                </div>
                <div class="detail-row">
                    <div class="detail-label">أدوات ومعدات الورش:</div>
                    <div class="detail-value">${app.workshop_equipment || 'غير مذكور'}</div>
                </div>
            </div>
        `;
        
        // إضافة قسم ملف السيرة الذاتية إذا كان موجوداً
        const hasFile = app._hasFile || app.has_file;
        if (hasFile) {
            const fileName = app._fileName || app.file_name;
            const fileSize = app._fileSize || app.file_size;
            
            details += `
                <div class="application-detail">
                    <h4>ملف السيرة الذاتية</h4>
                    <div class="file-info">
                        <div class="detail-row">
                            <div class="detail-label">اسم الملف:</div>
                            <div class="detail-value file-name">${fileName}</div>
                        </div>
                        <div class="detail-row">
                            <div class="detail-label">حجم الملف:</div>
                            <div class="detail-value file-size">${(fileSize / 1024).toFixed(2)} KB</div>
                        </div>
                        <div class="actions">
                            <button class="button success" onclick="downloadFile('${app._id || app.local_id}')">📥 تحميل ملف PDF</button>
                        </div>
                    </div>
                </div>
            `;
        }
        
        // إضافة معلومات إضافية
        const submittedAt = app._submittedAt || app.submitted_at;
        details += `
            <div class="application-detail">
                <h4>معلومات إضافية</h4>
                <div class="detail-row">
                    <div class="detail-label">تاريخ التقديم:</div>
                    <div class="detail-value">${new Date(submittedAt).toLocaleString('ar-EG')}</div>
                </div>
            </div>
        `;
        
        document.getElementById('applicationDetailContent').innerHTML = details;
        showPage('applicationDetail');
    }
    
    async function generateContract(id) {
        const applications = await enhancedLoadApplications();
        const app = applications.find(a => (a._id === id) || (a.local_id === id));
        
        if (!app) {
            alert('لم يتم العثور على الطلب');
            return;
        }
        
        // تعبئة بيانات العقد
        document.getElementById('c_name').value = app.fullName || app.full_name || '';
        document.getElementById('c_id').value = app.idNumber || app.id_number || '';
        document.getElementById('c_address').value = app.address || '';
        document.getElementById('c_skill').value = (app.specialty || '') + (app.other_programming ? ' - ' + app.other_programming : '');
        document.getElementById('c_start').value = new Date().toISOString().slice(0,10);
        
        // الانتقال إلى صفحة العقد
        showPage('contract');
    }
    
    async function deleteApplication(id) {
        if (!confirm('هل أنت متأكد من حذف هذا الطلب؟ سيتم حذف جميع البيانات المرتبطة به بما في ذلك ملف PDF.')) return;
        
        try {
            // حذف من السحابة
            const { error } = await supabase
                .from('applications')
                .delete()
                .eq('local_id', id);
            
            if (error) console.warn('لم يتم الحذف من السحابة:', error);
        } catch (error) {
            console.warn('تعذر الحذف من السحابة:', error);
        }
        
        // حذف محلي (كما كان)
        const applications = loadResponses();
        const filtered = applications.filter(a => a._id !== id);
        saveResponses(filtered);
        
        // حذف الملف المرتبط إن وجد
        const files = loadFiles();
        if (files[id]) {
            delete files[id];
            saveFiles(files);
        }
        
        loadApplications();
        updateStats();
    }
    
    async function updateStats() {
        const applications = await enhancedLoadApplications();
        const contracts = await loadContractsFromSupabase();
        const localContracts = loadContracts();
        
        // دمج العقود من السحابة والمحلية
        const allContracts = [...contracts, ...localContracts];
        
        document.getElementById('totalApplications').textContent = applications.length;
        document.getElementById('totalContracts').textContent = allContracts.length;
        
        // حساب الطلبات الجديدة (آخر 7 أيام)
        const weekAgo = new Date();
        weekAgo.setDate(weekAgo.getDate() - 7);
        const newApps = applications.filter(app => {
            const submittedAt = app._submittedAt || app.submitted_at;
            return new Date(submittedAt) > weekAgo;
        });
        document.getElementById('newApplications').textContent = newApps.length;
        
        // تحديث عدد الزوار
        document.getElementById('totalVisitors').textContent = getVisitorCount();
    }
    
    // تصدير جميع البيانات إلى Excel
    async function exportAllData() {
        const applications = await enhancedLoadApplications();
        exportToExcel(applications, 'جميع_الطلبات');
    }
    
    // تصدير البيانات المحددة إلى Excel
    async function exportSelectedData() {
        const selectedCheckboxes = document.querySelectorAll('.application-checkbox:checked');
        if (selectedCheckboxes.length === 0) {
            alert('يرجى تحديد طلب واحد على الأقل');
            return;
        }
        
        const applications = await enhancedLoadApplications();
        const selectedIds = Array.from(selectedCheckboxes).map(cb => cb.value);
        const selectedApplications = applications.filter(app => 
            selectedIds.includes(app._id) || selectedIds.includes(app.local_id)
        );
        
        exportToExcel(selectedApplications, 'الطلبات_المحددة');
    }
    
    // تصدير البيانات إلى Excel
    function exportToExcel(data, filename) {
        if (data.length === 0) {
            alert('لا توجد بيانات للتصدير');
            return;
        }
        
        // إنشاء رأس جدول Excel
        let csvContent = "data:text/csv;charset=utf-8,\ufeff";
        
        // إضافة رأس الجدول
        const headers = [
            "الرقم التسلسلي",
            "الاسم الكامل",
            "الجنس",
            "تاريخ الميلاد",
            "رقم البطاقة/الهوية",
            "رقم الهاتف",
            "البريد الإلكتروني",
            "عنوان السكن",
            "وسيلة نقل",
            "التفرغ",
            "سبب عدم التفرغ",
            "أعلى مؤهل",
            "التخصص",
            "الخبرات السابقة",
            "التعرف على القطع الإلكترونية",
            "برامج رسم الدوائر",
            "تفاصيل برامج رسم الدوائر",
            "برمجة Arduino",
            "برمجة ESP",
            "برمجة Raspberry Pi",
            "متحكمات أخرى",
            "نوع المتحكمات الأخرى",
            "مستوى المتحكمات الأخرى",
            "التصميم ثلاثي الأبعاد",
            "التشغيل على طابعات 3D",
            "برامج التصميم",
            "الطابعات المستخدمة",
            "أدوات الورشة",
            "تفاصيل أدوات الورشة",
            "الكهرباء ذات الفولتية العالية",
            "أدوات ومعدات الورش",
            "ملف السيرة الذاتية",
            "تاريخ التقديم"
        ];
        
        csvContent += headers.join(",") + "\r\n";
        
        // إضافة البيانات
        data.forEach((app, index) => {
            const submittedAt = app._submittedAt || app.submitted_at;
            const row = [
                index + 1,
                app.fullName || app.full_name || '',
                app.gender || '',
                app.dob || '',
                app.idNumber || app.id_number || '',
                app.phone || '',
                app.email || '',
                app.address || '',
                app.hasTransport || app.has_transport || '',
                app.isAvailable || app.is_available || '',
                app.availabilityReason || app.availability_reason || '',
                app.education || '',
                app.specialty || '',
                app.experience || '',
                app.skill_electronics || '',
                app.circuit_design_software || '',
                app.circuit_software_details || '',
                app.skill_arduino || '',
                app.skill_ESP || app.skill_esp || '',
                app.skill_rpi || '',
                app.other_controllers || '',
                app.other_controllers_type || '',
                app.other_controllers_level || '',
                app.skill_3d_design || '',
                app.skill_3d_printing || '',
                app.design_software || '',
                app.printers_used || '',
                app.workshop_tools || '',
                app.workshop_tools_details || '',
                app.high_voltage || '',
                app.workshop_equipment || '',
                (app._hasFile || app.has_file) ? 'نعم - ' + (app._fileName || app.file_name || '') : 'لا',
                new Date(submittedAt).toLocaleDateString('ar-EG')
            ].map(field => `"${field}"`).join(",");
            
            csvContent += row + "\r\n";
        });
        
        // إنشاء رابط التحميل
        const encodedUri = encodeURI(csvContent);
        const link = document.createElement("a");
        link.setAttribute("href", encodedUri);
        link.setAttribute("download", `${filename}_${new Date().toISOString().slice(0,10)}.csv`);
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
    }
    
    async function clearAllData() {
        if (!confirm('هل أنت متأكد من حذف جميع البيانات؟ لا يمكن التراجع عن هذا الإجراء.')) return;
        
        try {
            // حذف من السحابة
            const { error: appError } = await supabase
                .from('applications')
                .delete()
                .neq('id', 0); // حذف جميع السجلات
            
            const { error: contractError } = await supabase
                .from('contracts')
                .delete()
                .neq('id', 0); // حذف جميع السجلات
            
            if (appError) console.warn('لم يتم حذف الطلبات من السحابة:', appError);
            if (contractError) console.warn('لم يتم حذف العقود من السحابة:', contractError);
        } catch (error) {
            console.warn('تعذر الحذف من السحابة:', error);
        }
        
        // حذف محلي
        localStorage.removeItem(STORAGE_KEY);
        localStorage.removeItem(STORAGE_CONTRACTS);
        localStorage.removeItem(STORAGE_FILES);
        
        loadApplications();
        updateStats();
        alert('تم حذف جميع البيانات');
    }
    
    // وظائف صفحة العقد
    function genContractNumber() {
        const d = new Date();
        const rnd = Math.floor(100 + Math.random() * 900);
        return `SKY-${d.getFullYear()}-${rnd}`;
    }
    
    function genDateStr() {
        const d = new Date();
        return d.toLocaleDateString('ar-EG');
    }
    
    // تهيئة صفحة العقد
    document.getElementById('contractNumber').textContent = 'رقم العقد: ' + genContractNumber();
    document.getElementById('contractDate').textContent = 'تاريخ العقد: ' + genDateStr();
    
    document.getElementById('fillFromData').addEventListener('click', async function() {
        const applications = await enhancedLoadApplications();
        if (applications.length === 0) {
            alert('لا توجد طلبات مقدمه حتى الآن.');
            return;
        }
        
        // استخدام أحدث طلب
        const latest = applications[0]; // الأول هو الأحدث
        document.getElementById('c_name').value = latest.fullName || latest.full_name || '';
        document.getElementById('c_id').value = latest.idNumber || latest.id_number || '';
        document.getElementById('c_address').value = latest.address || '';
        document.getElementById('c_skill').value = (latest.specialty || '') + (latest.other_programming ? ' - ' + latest.other_programming : '');
        document.getElementById('c_start').value = new Date().toISOString().slice(0,10);
        
        alert('تم تعبئة البيانات من أحدث طلب مقدم');
    });
    
    document.getElementById('printBtn').addEventListener('click', function() {
        window.print();
    });
    
    document.getElementById('saveLocal').addEventListener('click', async function() {
        const obj = {
            contractNumber: document.getElementById('contractNumber').textContent.replace('رقم العقد: ', ''),
            contractDate: document.getElementById('contractDate').textContent.replace('تاريخ العقد: ', ''),
            name: document.getElementById('c_name').value,
            id: document.getElementById('c_id').value,
            address: document.getElementById('c_address').value,
            skill: document.getElementById('c_skill').value,
            rate: document.getElementById('c_rate').value,
            start: document.getElementById('c_start').value,
            empSig: document.getElementById('sig_emp').value,
            compSig: document.getElementById('sig_comp').value,
            savedAt: new Date().toISOString()
        };
        
        // الحفظ المحلي
        const arr = loadContracts();
        arr.push(obj);
        saveContracts(arr);
        
        // الحفظ في السحابة
        try {
            await saveContractToSupabase(obj);
        } catch (error) {
            console.warn('تعذر الحفظ في السحابة:', error);
        }
        
        alert('تم حفظ العقد محليًا وفي السحابة');
        renderSavedContracts();
    });
    
    async function renderSavedContracts() {
        const cloudContracts = await loadContractsFromSupabase();
        const localContracts = loadContracts();
        
        // دمج العقود
        const allContracts = [...cloudContracts, ...localContracts];
        
        const wrap = document.getElementById('savedList');
        const card = document.getElementById('savedListCard');
        
        if (allContracts.length === 0) { 
            card.style.display = 'none'; 
            return; 
        }
        
        card.style.display = 'block';
        wrap.innerHTML = allContracts.map((c, i) => {
            const contractNumber = c.contractNumber || c.contract_number;
            const name = c.name || c.employee_name;
            const savedAt = c.savedAt || c.saved_at;
            
            return `<div class="contract-item">
                <strong>${contractNumber}</strong> - ${name} - ${new Date(savedAt).toLocaleString('ar-EG')}
                <div style="margin-top: 10px;">
                    <button class="button" onclick="loadSavedContract(${i})">تحميل</button>
                    <button class="button danger" onclick="deleteSavedContract(${i})">حذف</button>
                </div>
            </div>`;
        }).join('');
    }
    
    async function loadSavedContract(i) {
        const cloudContracts = await loadContractsFromSupabase();
        const localContracts = loadContracts();
        const allContracts = [...cloudContracts, ...localContracts];
        
        const c = allContracts[i];
        if (!c) return;
        
        const contractNumber = c.contractNumber || c.contract_number;
        const contractDate = c.contractDate || c.contract_date;
        const name = c.name || c.employee_name;
        const id = c.id || c.employee_id;
        const address = c.address || c.employee_address;
        const skill = c.skill || c.employee_skill;
        const rate = c.rate || c.rate_percentage;
        const start = c.start || c.start_date;
        const empSig = c.empSig || c.employee_signature;
        const compSig = c.compSig || c.company_signature;
        
        document.getElementById('contractNumber').textContent = 'رقم العقد: ' + contractNumber;
        document.getElementById('contractDate').textContent = 'تاريخ العقد: ' + contractDate;
        document.getElementById('c_name').value = name;
        document.getElementById('c_id').value = id;
        document.getElementById('c_address').value = address;
        document.getElementById('c_skill').value = skill;
        document.getElementById('c_rate').value = rate;
        document.getElementById('c_start').value = start;
        document.getElementById('sig_emp').value = empSig;
        document.getElementById('sig_comp').value = compSig;
        
        window.scrollTo({top: 0, behavior: 'smooth'});
        alert('تم تحميل العقد المحفوظ');
    }
    
    async function deleteSavedContract(i) {
        if (!confirm('حذف العقد المحفوظ؟')) return;
        
        const cloudContracts = await loadContractsFromSupabase();
        const localContracts = loadContracts();
        const allContracts = [...cloudContracts, ...localContracts];
        
        const contractToDelete = allContracts[i];
        if (!contractToDelete) return;
        
        // حذف من السحابة إذا كان عقد سحابي
        if (contractToDelete.id) { // إذا كان له id فهو من السحابة
            try {
                const { error } = await supabase
                    .from('contracts')
                    .delete()
                    .eq('id', contractToDelete.id);
                
                if (error) throw error;
            } catch (error) {
                console.warn('تعذر الحذف من السحابة:', error);
            }
        }
        
        // حذف محلي
        const updatedLocalContracts = localContracts.filter((c, index) => {
            // حذف العقد المحلي الذي يتوافق مع الفهرس
            if (index === i && !contractToDelete.id) {
                return false; // حذفه
            }
            return true;
        });
        saveContracts(updatedLocalContracts);
        
        renderSavedContracts();
        alert('تم حذف العقد');
    }
    
    // التهيئة الأولية عند تحميل الصفحة
    document.addEventListener('DOMContentLoaded', function() {
        // زيادة عدد الزوار عند تحميل الصفحة
        incrementVisitorCount();
        
        // التحقق من حالة تسجيل الدخول
        if (checkLoginStatus()) {
            login();
        } else {
            // إخفاء محتوى الإدارة والعقد عن العامة
            document.querySelectorAll('.admin-only').forEach(el => {
                el.style.display = 'none';
            });
        }
        
        updateStats();
        renderSavedContracts();
        
        // مزامنة البيانات مع السحابة (في الخلفية)
        setTimeout(() => {
            syncWithSupabase();
        }, 2000);
    });
</script>

</body>
</html>
