# مسجد المغفرة

تطبيق Flutter عربي أولاً، بتصميم إسلامي Premium باللون الأخضر الداكن والذهبي. المشروع ليس صفحة ويب أو صورة Prototype؛ بل يحتوي على شاشات وتنقل وحالة وتخزين وبحث وقارئات وتنزيلات قابلة للتشغيل بعد توليد مجلد Android القياسي.

## ملخص التنفيذ

1. **التقنية:** Flutter 3.44+ وDart 3.10+ لتطبيق Android واحد قابل للتوسع.
2. **Architecture:** فصل `core / data / models / state / features / widgets` مع مكونات قابلة لإعادة الاستخدام.
3. **الشاشات:** Splash، الرئيسية، المكتبة، البحث، المفضلة، الإعدادات، تفاصيل الكتاب، القرآن، قارئ القرآن، قارئ PDF، الأذكار، التنزيلات، وأقسام المحتوى.
4. **المكونات:** IslamicCard، BookCard، SectionHeader، AppLogo، BookGlyph، EmptyState، AppLoading وخلفية زخرفية خفيفة.
5. **التخزين:** `SharedPreferencesAsync` للمفضلة والعلامات وآخر قراءة والثيم وحجم الخط ومسارات التنزيل.
6. **PDF:** مكتبة `pdfrx`، تحميل متدفق إلى Documents عبر `http` و`path_provider`، تكبير وانتقال للصفحة ووضع قراءة وعلامات.
7. **البحث:** فهرس محلي سريع مع تطبيع التشكيل وأشكال الألف والياء لنتائج عربية أفضل.
8. **المفضلة:** معرفات محلية بلا Login، وتعمل Offline.

## ما تم تنفيذه

- RTL عربي كامل وMaterial 3.
- Dark / Light Mode محفوظ محلياً.
- الصفحة الرئيسية بالترتيب المطلوب وBottom Navigation من خمسة عناصر.
- الأقسام الثمانية المطلوبة وقائمة 114 سورة.
- بحث عام، مفضلة، علامات، آخر قراءة، تقدم، تنزيلات، وعدّاد أذكار.
- قارئ قرآن UI جاهز للربط بمصدر موثق، وقارئ PDF حقيقي.
- Loading / Empty / Error / No Results / No Downloads / Book Not Found messaging.
- App Icon أصلي داخل `assets/branding/app_icon.png`.
- خطا Noto Kufi Arabic للواجهة وNoto Naskh Arabic للقراءة مضمّنان محلياً.
- لا يوجد Login ولا تخزين بيانات شخصية.
- الدعاء المطلوب للمهندس أحمد رمضان جاد داخل «عن التطبيق».

## المحتوى الديني

لا يختلق المشروع آيات أو أحاديث أو مصادر. باستثناء ورد اليوم المحدد في المواصفات مع مرجعه، يظهر المحتوى غير المتوفر بعبارة واضحة: **سيتم إضافة المحتوى الموثق قريباً**. يجب إضافة الملفات والنصوص بعد مراجعتها قبل النشر.

## التشغيل

المتطلبات: Flutter 3.44 أو أحدث، Android SDK، Java 17، وهاتف/محاكي Android 24+.

من داخل مجلد المشروع:

```bash
bash tool/bootstrap_android.sh
flutter run
```

على Windows PowerShell:

```powershell
powershell -ExecutionPolicy Bypass -File tool/bootstrap_android.ps1
flutter run
```

السكريبت يولد مجلد Android القياسي إن لم يكن موجوداً، يثبت الحزم، يولد أحجام الأيقونة، ثم يشغّل `flutter analyze` و`flutter test`.

## إضافة كتب PDF

- ملف محلي: ضعه داخل `assets/books/` ثم عيّن `assetPath` في الكتاب.
- تحميل: عيّن `remoteUrl` إلى رابط HTTPS مباشر وموثوق للملف.
- لا تحمل كل الملفات مع التطبيق؛ اترك الكتب الكبيرة للتنزيل الاختياري.

## بناء APK / AAB

```bash
flutter build apk --release
flutter build appbundle --release
```

قبل Google Play: أضف توقيع Release، رابط سياسة خصوصية منشور، بيانات المتجر، اختبارات أجهزة حقيقية، وراجع تراخيص ومصادر جميع الكتب.
