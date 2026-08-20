# دليل بناء APK عبر Codemagic

Codemagic لا يقبل رفع ملف zip مباشرة للبناء — لازم يكون المشروع على
مستودع Git (GitHub / GitLab / Bitbucket) أولاً. الخطوات بالترتيب:

## 1) ارفع المشروع على GitHub (مجاني، 5 دقائق)

1. اعمل حساب على https://github.com إن لم يكن لديك واحد.
2. اضغط **New repository** واختر اسم مثل `masjid-al-maghfira` واجعله
   **Private** أو **Public** حسب رغبتك، ثم **Create repository**.
3. على جهازك، جوه مجلد المشروع (بعد فك الضغط)، نفّذ:

   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/USERNAME/masjid-al-maghfira.git
   git push -u origin main
   ```

   (بدّل `USERNAME` باسم حسابك، و`masjid-al-maghfira` باسم المستودع
   اللي اخترته.)

   > لو معندكش Git مثبت، نزّله من https://git-scm.com، أو استخدم
   > GitHub Desktop (واجهة رسومية بدون أوامر): https://desktop.github.com

## 2) اربط Codemagic بالمستودع

1. روح https://codemagic.io واعمل حساب مجاني (تقدر تسجل دخول
   مباشرة بحساب GitHub بتاعك — أسهل خطوة).
2. اضغط **Add application**.
3. اختر GitHub، وامنح Codemagic صلاحية الوصول لمستودعك (أو لكل
   المستودعات).
4. اختر المستودع `masjid-al-maghfira` من القائمة.
5. Codemagic هيكتشف تلقائيًا وجود ملف `codemagic.yaml` في جذر
   المشروع (مضاف بالفعل) ويستخدمه كإعداد البناء — مفيش حاجة تانية
   تظبطها يدويًا.

## 3) شغّل البناء

1. من صفحة التطبيق، اختر الـ workflow اسمه **android-apk**.
2. اضغط **Start new build**.
3. البناء بياخد حوالي 5-10 دقايق. هيعمل تلقائيًا:
   - توليد مجلد `android/` (غير موجود حاليًا في المشروع)
   - تثبيت الحزم (`flutter pub get`)
   - توليد أيقونة التطبيق
   - بناء `app-release.apk` (نسخة غير موقّعة — تكفي للتجربة والتوزيع
     المباشر، لكن لو هترفعه على Google Play محتاج توقيع لاحقًا)
4. بعد انتهاء البناء، هتلاقي رابط تنزيل الملف في قسم **Artifacts**
   باسم `app-release.apk`.

## ملاحظة مهمة قبل التوزيع الفعلي

مجلد `assets/books/` فاضي من ملفات PDF حقيقية حاليًا — التطبيق
هيشتغل ويُبنى بنجاح، لكن قسم الكتب هيظهر برسالة "سيتم إضافة المحتوى
الموثق قريباً" لحد ما تضيف ملفات PDF فعلية وتحدّث
`lib/data/mock_data.dart`.
