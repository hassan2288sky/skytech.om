<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>نظام التوظيف - سماء التقنية</title>
    <style>
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
    </style>
</head>
<body>

<header>
    <div class="logo-text"> شركة سماء التقنية | Sky Tech</div>
    <h1>إنضم إلى فريقنا في سماء التقنية</h1>
</header>

<div class="nav-tabs">
    <div class="nav-tab active" data-page="home">الصفحة الرئيسية</div>
    <div class="nav-tab" data-page="apply">تقديم طلب توظيف</div>
    <div class="nav-tab" data-page="contract">إنشاء عقد عمل</div>
    <div class="nav-tab" data-page="admin">لوحة الإدارة</div>
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
                أشخاص موهوبون في تركيب الدوائر الإلكترونية، برمجة المتحكمات (Arduino/ESP32/Raspberry Pi)، التصميم ثلاثيّ الأبعاد،
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
                <button class="button outline" onclick="showPage('admin')">لوحة الإدارة</button>
            </div>
        </section>
    </div>

    <!-- صفحة تقديم الطلب -->
    <div id="apply" class="page">
        <section class="card">
            <h2>نموذج بيانات المتقدم - سماء التقنية</h2>
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
                        <option>ضعيف</option>
                        <option>متوسط</option>
                        <option>ممتاز</option>
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
                            <option>ضعيف</option>
                            <option>متوسط</option>
                            <option>ممتاز</option>
                        </select>
                    </div>
                    
                    <div class="skill-item">
                        <label>ESP32</label>
                        <select name="skill_esp32">
                            <option value="">اختر</option>
                            <option>ضعيف</option>
                            <option>متوسط</option>
                            <option>ممتاز</option>
                        </select>
                    </div>
                    
                    <div class="skill-item">
                        <label>Raspberry Pi</label>
                        <select name="skill_rpi">
                            <option value="">اختر</option>
                            <option>ضعيف</option>
                            <option>متوسط</option>
                            <option>ممتاز</option>
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
                                    <option>ضعيف</option>
                                    <option>متوسط</option>
                                    <option>ممتاز</option>
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
                                <option>ضعيف</option>
                                <option>متوسط</option>
                                <option>ممتاز</option>
                            </select>
                        </div>
                        <div class="col">
                            <label>التشغيل على طابعات 3D</label>
                            <select name="skill_3d_printing">
                                <option value="">اختر</option>
                                <option>ضعيف</option>
                                <option>متوسط</option>
                                <option>ممتاز</option>
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
                    <input type="file" name="cv_file" accept=".pdf">
                    <p class="note">يرجى رفع ملف PDF فقط (حجم أقصى 5MB)</p>
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
        </section>
    </div>

    <!-- صفحة العقد -->
    <div id="contract" class="page">
        <section class="card">
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
            </div>

            <p class="note">يمكنك تعديل أي حقل قبل الطباعة. سيولد رقم وعنوان تلقائيًا عند فتح الصفحة عبر لوحة الإدارة.</p>
        </section>

        <section class="card saved-contracts" id="savedListCard" style="display:none">
            <h3>العقود المحفوظة (محليًا)</h3>
            <div id="savedList"></div>
        </section>
    </div>

    <!-- لوحة الإدارة -->
    <div id="admin" class="page">
        <section class="card">
            <h2>لوحة إدارة طلبات التوظيف</h2>
            
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
            </div>

            <div class="actions">
                <button class="button outline" onclick="exportData()">📥 تصدير البيانات</button>
                <button class="button danger" onclick="clearAllData()">🗑️ حذف جميع البيانات</button>
            </div>

            <h3>الطلبات المقدمة</h3>
            <div id="applicationsList">
                <p>جاري تحميل البيانات...</p>
            </div>
        </section>
    </div>
</div>

<footer>
    © جميع الحقوق محفوظة لشركة سماء التقنية ش.م.م | Sky Tech
</footer>

<script>
    // الثوابت والمتغيرات العامة
    const STORAGE_KEY = 'skytech_responses';
    const STORAGE_CONTRACTS = 'skytech_contracts';
    
    // وظائف التنقل بين الصفحات
    function showPage(pageId) {
        // إخفاء جميع الصفحات
        document.querySelectorAll('.page').forEach(page => {
            page.classList.remove('active');
        });
        
        // إظهار الصفحة المطلوبة
        document.getElementById(pageId).classList.add('active');
        
        // تحديث التبويبات النشطة
        document.querySelectorAll('.nav-tab').forEach(tab => {
            tab.classList.remove('active');
            if (tab.getAttribute('data-page') === pageId) {
                tab.classList.add('active');
            }
        });
        
        // إذا كانت صفحة الإدارة، قم بتحديث القائمة
        if (pageId === 'admin') {
            loadApplications();
            updateStats();
        }
        
        // إذا كانت صفحة العقد، قم بتحديث العقود المحفوظة
        if (pageId === 'contract') {
            renderSavedContracts();
        }
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
    document.getElementById('applyForm').addEventListener('submit', function(e){
        e.preventDefault();
        const form = e.target;
        const fd = new FormData(form);
        const obj = {};
        fd.forEach((v,k) => obj[k]=v);
        
        // إضافة بيانات ووقت الإرسال
        obj._submittedAt = new Date().toISOString();
        obj._id = Date.now().toString(); // معرف فريد
        
        // تحميل الطلبات الحالية وإضافة الجديد
        const arr = loadResponses();
        arr.push(obj);
        saveResponses(arr);
        
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
    function loadApplications() {
        const applications = loadResponses();
        const container = document.getElementById('applicationsList');
        
        if (applications.length === 0) {
            container.innerHTML = '<p>لا توجد طلبات مقدمه حتى الآن.</p>';
            return;
        }
        
        let html = `
            <table class="applications-table">
                <thead>
                    <tr>
                        <th>الاسم</th>
                        <th>الهاتف</th>
                        <th>البريد</th>
                        <th>التخصص</th>
                        <th>تاريخ التقديم</th>
                        <th>الإجراءات</th>
                    </tr>
                </thead>
                <tbody>
        `;
        
        applications.forEach(app => {
            const date = new Date(app._submittedAt).toLocaleDateString('ar-EG');
            html += `
                <tr>
                    <td>${app.fullName || 'غير مذكور'}</td>
                    <td>${app.phone || 'غير مذكور'}</td>
                    <td>${app.email || 'غير مذكور'}</td>
                    <td>${app.specialty || 'غير مذكور'}</td>
                    <td>${date}</td>
                    <td>
                        <div class="action-buttons">
                            <button class="button" onclick="viewApplication('${app._id}')">عرض</button>
                            <button class="button outline" onclick="generateContract('${app._id}')">عقد</button>
                            <button class="button danger" onclick="deleteApplication('${app._id}')">حذف</button>
                        </div>
                    </td>
                </tr>
            `;
        });
        
        html += '</tbody></table>';
        container.innerHTML = html;
    }
    
    function viewApplication(id) {
        const applications = loadResponses();
        const app = applications.find(a => a._id === id);
        
        if (!app) {
            alert('لم يتم العثور على الطلب');
            return;
        }
        
        let details = `الاسم: ${app.fullName}\n`;
        details += `الجنس: ${app.gender}\n`;
        details += `الهاتف: ${app.phone}\n`;
        details += `البريد: ${app.email}\n`;
        details += `العنوان: ${app.address}\n`;
        details += `المؤهل: ${app.education}\n`;
        details += `التخصص: ${app.specialty}\n`;
        details += `وسيلة نقل: ${app.hasTransport}\n`;
        details += `متفرغ: ${app.isAvailable}\n`;
        details += `سبب عدم التفرغ: ${app.availabilityReason || 'لا ينطبق'}\n`;
        details += `التعرف على القطع الإلكترونية: ${app.skill_electronics}\n`;
        details += `برامج رسم الدوائر: ${app.circuit_design_software}\n`;
        details += `تفاصيل برامج رسم الدوائر: ${app.circuit_software_details || 'لا ينطبق'}\n`;
        details += `برمجة Arduino: ${app.skill_arduino}\n`;
        details += `برمجة ESP32: ${app.skill_esp32}\n`;
        details += `برمجة Raspberry Pi: ${app.skill_rpi}\n`;
        details += `متحكمات أخرى: ${app.other_controllers}\n`;
        details += `نوع المتحكمات الأخرى: ${app.other_controllers_type || 'لا ينطبق'}\n`;
        details += `مستوى المتحكمات الأخرى: ${app.other_controllers_level || 'لا ينطبق'}\n`;
        details += `تصميم 3D: ${app.skill_3d_design}\n`;
        details += `طباعة 3D: ${app.skill_3d_printing}\n`;
        details += `برامج التصميم: ${app.design_software || 'لا ينطبق'}\n`;
        details += `الطابعات المستخدمة: ${app.printers_used || 'لا ينطبق'}\n`;
        details += `أدوات ورشة الإلكترونيات: ${app.workshop_tools}\n`;
        details += `تفاصيل أدوات الورشة: ${app.workshop_tools_details || 'لا ينطبق'}\n`;
        details += `الكهرباء ذات الفولتية العالية: ${app.high_voltage}\n`;
        details += `أدوات ومعدات الورش: ${app.workshop_equipment}\n`;
        details += `الخبرات: ${app.experience}\n`;
        
        alert(details);
    }
    
    function generateContract(id) {
        const applications = loadResponses();
        const app = applications.find(a => a._id === id);
        
        if (!app) {
            alert('لم يتم العثور على الطلب');
            return;
        }
        
        // تعبئة بيانات العقد
        document.getElementById('c_name').value = app.fullName || '';
        document.getElementById('c_id').value = app.idNumber || '';
        document.getElementById('c_address').value = app.address || '';
        document.getElementById('c_skill').value = (app.specialty || '') + (app.other_programming ? ' - ' + app.other_programming : '');
        document.getElementById('c_start').value = new Date().toISOString().slice(0,10);
        
        // الانتقال إلى صفحة العقد
        showPage('contract');
    }
    
    function deleteApplication(id) {
        if (!confirm('هل أنت متأكد من حذف هذا الطلب؟')) return;
        
        const applications = loadResponses();
        const filtered = applications.filter(a => a._id !== id);
        saveResponses(filtered);
        loadApplications();
        updateStats();
    }
    
    function updateStats() {
        const applications = loadResponses();
        const contracts = loadContracts();
        
        document.getElementById('totalApplications').textContent = applications.length;
        document.getElementById('totalContracts').textContent = contracts.length;
        
        // حساب الطلبات الجديدة (آخر 7 أيام)
        const weekAgo = new Date();
        weekAgo.setDate(weekAgo.getDate() - 7);
        const newApps = applications.filter(app => new Date(app._submittedAt) > weekAgo);
        document.getElementById('newApplications').textContent = newApps.length;
    }
    
    function exportData() {
        const applications = loadResponses();
        const dataStr = JSON.stringify(applications, null, 2);
        const dataBlob = new Blob([dataStr], {type: 'application/json'});
        
        const link = document.createElement('a');
        link.href = URL.createObjectURL(dataBlob);
        link.download = `skytech_applications_${new Date().toISOString().slice(0,10)}.json`;
        link.click();
    }
    
    function clearAllData() {
        if (!confirm('هل أنت متأكد من حذف جميع البيانات؟ لا يمكن التراجع عن هذا الإجراء.')) return;
        
        localStorage.removeItem(STORAGE_KEY);
        localStorage.removeItem(STORAGE_CONTRACTS);
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
    
    document.getElementById('fillFromData').addEventListener('click', function() {
        const applications = loadResponses();
        if (applications.length === 0) {
            alert('لا توجد طلبات مقدمه حتى الآن.');
            return;
        }
        
        // استخدام أحدث طلب
        const latest = applications[applications.length - 1];
        document.getElementById('c_name').value = latest.fullName || '';
        document.getElementById('c_id').value = latest.idNumber || '';
        document.getElementById('c_address').value = latest.address || '';
        document.getElementById('c_skill').value = (latest.specialty || '') + (latest.other_programming ? ' - ' + latest.other_programming : '');
        document.getElementById('c_start').value = new Date().toISOString().slice(0,10);
        
        alert('تم تعبئة البيانات من أحدث طلب مقدم');
    });
    
    document.getElementById('printBtn').addEventListener('click', function() {
        window.print();
    });
    
    document.getElementById('saveLocal').addEventListener('click', function() {
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
        
        const arr = loadContracts();
        arr.push(obj);
        saveContracts(arr);
        alert('تم حفظ العقد محليًا');
        renderSavedContracts();
    });
    
    function renderSavedContracts() {
        const arr = loadContracts();
        const wrap = document.getElementById('savedList');
        const card = document.getElementById('savedListCard');
        
        if (!arr.length) { 
            card.style.display = 'none'; 
            return; 
        }
        
        card.style.display = 'block';
        wrap.innerHTML = arr.map((c, i) => {
            return `<div class="contract-item">
                <strong>${c.contractNumber}</strong> - ${c.name} - ${new Date(c.savedAt).toLocaleString('ar-EG')}
                <div style="margin-top: 10px;">
                    <button class="button" onclick="loadSavedContract(${i})">تحميل</button>
                    <button class="button danger" onclick="deleteSavedContract(${i})">حذف</button>
                </div>
            </div>`;
        }).join('');
    }
    
    function loadSavedContract(i) {
        const arr = loadContracts();
        const c = arr[i];
        if (!c) return;
        
        document.getElementById('contractNumber').textContent = 'رقم العقد: ' + c.contractNumber;
        document.getElementById('contractDate').textContent = 'تاريخ العقد: ' + c.contractDate;
        document.getElementById('c_name').value = c.name;
        document.getElementById('c_id').value = c.id;
        document.getElementById('c_address').value = c.address;
        document.getElementById('c_skill').value = c.skill;
        document.getElementById('c_rate').value = c.rate;
        document.getElementById('c_start').value = c.start;
        document.getElementById('sig_emp').value = c.empSig;
        document.getElementById('sig_comp').value = c.compSig;
        
        window.scrollTo({top: 0, behavior: 'smooth'});
        alert('تم تحميل العقد المحفوظ');
    }
    
    function deleteSavedContract(i) {
        if (!confirm('حذف العقد المحفوظ؟')) return;
        
        const arr = loadContracts();
        arr.splice(i, 1);
        saveContracts(arr);
        renderSavedContracts();
        alert('تم حذف العقد');
    }
    
    // التهيئة الأولية عند تحميل الصفحة
    document.addEventListener('DOMContentLoaded', function() {
        updateStats();
        renderSavedContracts();
    });
</script>

</body>
</html>
