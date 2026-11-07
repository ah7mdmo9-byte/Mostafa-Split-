# Mostafa🐺Split

تطبيق جيم بيجمع مميزات Strong وHevy وJEFIT وBoostcamp:

- جدول أسبوعي وتسجيل كل مجموعة (وزن وعدات ونوع المجموعة)
- أرقام قياسية و1RM تقديري وإحماء تلقائي
- تايمر راحة يشتغل بعد كل مجموعة، وبإشعار صوتي حتى لو التطبيق مقفول
- متابعة الوزن وقياسات الجسم ورسوم التقدم
- حاسبة بلاطات وحاسبة 1RM وبرامج جاهزة وتصدير CSV

## بناء الـ APK على GitHub (من غير ما تركّب حاجة على جهازك)

1. اعمل Repository جديد على GitHub وارفع محتويات المجلد ده كله (مع مجلد `.github`).
2. افتح تبويب **Actions** واختار **Build Android APK**، وبعدين **Run workflow**.
3. بعد ما يخلص (حوالي 5 إلى 10 دقايق) نزّل الملف `gym-all-in-one-apk` من آخر تشغيل.
4. فك الضغط وانقل `app-debug.apk` لموبايل الأندرويد وثبّته (فعّل "التثبيت من مصادر غير معروفة").
5. أول ما التايمر يشتغل هيطلب إذن الإشعارات. وافق عليه، ومن إعدادات الأندرويد اسمح للتطبيق بالتنبيهات الدقيقة (Alarms & reminders).

## أيقونة التطبيق

الأيقونة بتتولّد تلقائي من مجلد `assets` (الملفات `icon-only.png` و`icon-foreground.png` و`icon-background.png`). لتغيير الصورة بدّل الملفات دي بصور 1024×1024 بنفس الأسماء.

## التحديثات من غير رسالة "التطبيق غير مثبت"

- المشروع فيه ملف `debug.keystore` ثابت، وكل بناء بيتوقّع بيه، فالتحديث بيتركّب فوق النسخة القديمة.
- رقم الإصدار (`versionCode`) بيزيد تلقائي مع كل تشغيل للـ workflow.
- **مرة واحدة بس:** لو عندك نسخة اتبنت قبل إضافة الملف ده، احذفها من الموبايل قبل ما تركّب الجديدة (لأن التوقيع اتغير). بياناتك هتتمسح معاها، فصدّرها CSV الأول.
- **متمسحش `debug.keystore` ولا تغيّره**، ولا تحذف التطبيق من الريبو.
- الملف ده للاستخدام الشخصي. لو الريبو عام فالأفضل تخليه Private.

## البناء على جهازك

```bash
npm install
npx cap add android
npx cap sync android
npx cap open android   # يفتح Android Studio
```

بعد `cap add android` ضيف الصلاحيات دي في `android/app/src/main/AndroidManifest.xml` قبل وسم `<application`:

```xml
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>
<uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM"/>
<uses-permission android:name="android.permission.USE_EXACT_ALARM"/>
```

## تعديل التطبيق

كل كود التطبيق في ملف واحد: `www/index.html`. بعد أي تعديل شغّل `npx cap sync android`.

## ملاحظات

- البيانات بتتخزن على الجهاز نفسه (localStorage).
- الـ APK ده نسخة تجريبية (debug). لنشره على Google Play محتاج توقيع Release.
- لو نسخة Capacitor 7 اتغيرت، حدّث الأرقام في `package.json`.
- iOS محتاج جهاز Mac: `npm i @capacitor/ios` ثم `npx cap add ios`.
