<!DOCTYPE html>
<html lang="ar" translate="yes">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الساعة المخصصة</title>
    <!-- ربط Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', Arial, sans-serif;
            text-align: center;
            background-color: #2c3e50;
            color: #ecf0f1;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 10vh;
        }

        h1 {
            font-size: 30px;
            margin-bottom: 0px;
            color: ‎#2c6e50 ;
        }

        h2 {
            font-size: 45px;
            margin-bottom: 0px;
            color: ‎#2c7e50 ;
        }

        .clock-container {
            margin-top: 16px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .digital-clock {
            font-size: 44px;
            margin: 10px 0;
            font-weight: bold;
        }

        .device-clock {
            color: #3498db;
        }

        .custom-clock {
            color: #e74c3c;
        }

        .clock-label {
            margin-top: 10px;
            font-size: 18px;
            color: #f39c12;
        }

        /* تحسين عرض النصوص القابلة للترجمة */
        [translate="yes"] {
            cursor: pointer;
            text-decoration: ;
        }
    </style>
</head>
<body>

    <h2>Bicka V 3.0.7</h2>
<h1>اللهم صلي وسلم على نبينا محمد وعلى آله وصحبه أجمعين وسلم تسليما كثيرا </h1>

    <div class="clock-container">
        <div class="clock-label">Original Clock (Device Clock 24h/d)</div>
        <div class="digital-clock device-clock" id="device-clock">00:00:00</div>

        <div class="clock-label">Modern Clock (Future Clock 30h/d)</div> 
        <div class="digital-clock custom-clock" id="custom-clock">00:00:00</div>
    </div>

    <script>
        // تحميل Google Translate API
        function loadGoogleTranslateAPI() {
            const script = document.createElement('script');
            script.src = 'https://translate.google.com/translate_a/element.js?cb=googleTranslateElementInit';
            document.body.appendChild(script);
        }

        // تفعيل Google Translate API
        window.googleTranslateElementInit = function () {
            new google.translate.TranslateElement(
                { pageLanguage: 'en', includedLanguages: 'ar,en,fr,es,de' },
                'google-translate-element'
            );
        };

        // تأجيل تحميل Google Translate API حتى يتم تحميل الصفحة
        window.onload = function () {
            loadGoogleTranslateAPI();
        };

        // تعريف الساعتين
        const deviceClockDisplay = document.getElementById('device-clock');
        const customClockDisplay = document.getElementById('custom-clock');

        const hoursInDay = 30; // عدد الساعات في اليوم المخصص
        const timeScaleFactor = 1; // معدل سرعة الوقت (كل 4 ساعات حقيقية = 5 ساعات محدثة)

        function updateDeviceClock() {
            const now = new Date();
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            deviceClockDisplay.textContent = `${hours}:${minutes}:${seconds}`;
        }

        function customClock() {
            const secondsPerMinute = 60;
            const minutesPerHour = 60;

            const now = new Date();
            const totalSecondsToday = now.getHours() * secondsPerMinute * minutesPerHour + 
                                      now.getMinutes() * secondsPerMinute + 
                                      now.getSeconds();

            // حساب الزمن المخصص بناءً على الساعة الحقيقية
            const scaledTimeInSeconds = Math.floor(totalSecondsToday * (hoursInDay / 24) * timeScaleFactor);

            // حساب الزمن في النظام المخصص
            let customHours = Math.floor(scaledTimeInSeconds / (secondsPerMinute * minutesPerHour) % hoursInDay);
            let customMinutes = Math.floor(scaledTimeInSeconds / secondsPerMinute % minutesPerHour);
            let customSeconds = Math.floor(scaledTimeInSeconds % secondsPerMinute);

            // صياغة النتيجة بتنسيق "HH:MM:SS"
            let formattedCustomTime = 
                String(customHours).padStart(2, '0') + ":" +
                String(customMinutes).padStart(2, '0') + ":" +
                String(customSeconds).padStart(2, '0');

            // تحديث العرض الرقمي للساعة المخصصة
            customClockDisplay.textContent = formattedCustomTime;

            // تحديث الساعة كل 100 ميلي ثانية
            setTimeout(customClock, 100);
        }

        // بدء الساعات عند تحميل الصفحة
        updateDeviceClock();
        setInterval(updateDeviceClock, 1000); // تحديث الساعة الحقيقية كل ثانية
        customClock();
    </script>

    <!-- إضافة عنصر Google Translate -->
    <div id="google-translate-element"></div>

</body>
</html>
