[English](./README.md) · **العربية**

# Healthy Scan (هيلثي سكان)

<p align="center">
  <img src="assets/logo.png" alt="Healthy Scan" width="120" />
</p>

<p align="center">
  <b>امسح. فكّك. قرّر.</b><br/>
  تطبيق Flutter للهواتف يحوّل الباركود الخاص بالمنتجات إلى إشارات واضحة عن التغذية والاستدامة.
</p>

<p align="center">
  <img alt="Flutter" src="https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white" />
  <img alt="Dart" src="https://img.shields.io/badge/Dart-3.9-0175C2?style=flat-square&logo=dart&logoColor=white" />
  <img alt="Firebase" src="https://img.shields.io/badge/Firebase-Auth-FFCA28?style=flat-square&logo=firebase&logoColor=black" />
  <img alt="OpenFoodFacts" src="https://img.shields.io/badge/OpenFoodFacts-API-5A9E6F?style=flat-square" />
  <img alt="State" src="https://img.shields.io/badge/State-Provider-purple?style=flat-square" />
</p>

---

## لماذا أُنشئ هذا التطبيق

معظم المتسوقين يرون باركود. Healthy Scan يرى سطح قرار.

وجّه الكاميرا إلى منتج → احصل على بيانات غذائية منظّمة من **Open Food Facts** → اعرض **Nutri-Score** و **Eco-Score** و **NOVA** والمغذيات الكبرى والمحسّسات والمكونات في شاشة منتج نظيفة.

بُني كتطبيق Flutter باحترافية: هوية Firebase، مسح واعٍ بالأذونات، شبكات عبر طبقة خدمات، وحالة واجهة مدفوعة بـ Provider.

## الميزات

| المجال | ما الذي تحصل عليه |
|------|----------------|
| المصادقة | بريد/كلمة مرور + تسجيل دخول Google عبر Firebase Auth |
| المسح | مسح باركود بالكاميرا مع معالجة أذونات في وقت التشغيل |
| بيانات المنتج | الاسم، العلامة، الصورة، الكمية، المكونات، المحسّسات |
| التقييمات | Nutri-Score · Eco-Score · مجموعة المعالجة NOVA |
| التغذية | الطاقة، المغذيات الكبرى، الملح/الصوديوم والمغذيات ذات الصلة (لكل 100غ) |
| UX | ترحيب، زر مسح مدمج، تنقل سفلي متحرك، صور منتجات مخزّنة |
| المعمارية | Views → Providers → Services → Models |

## تدفق المستخدم

```text
الترحيب → تسجيل / تسجيل دخول (بريد أو Google)
       → الرئيسية (تثقيف NOVA / Nutri / Eco)
       → زر المسح → الكاميرا → الباركود
       → تفاصيل المنتج (تقييمات + تغذية + مكونات)
       → الملف الشخصي / الإعدادات
```

## العرض

شاشات حقيقية من التطبيق (بوضع عمودي):

### المصادقة
<table>
  <tr>
    <td align="center"><img src="showcase/login1-portrait.png" alt="دخول 1" width="220"/></td>
    <td align="center"><img src="showcase/login2-portrait.png" alt="دخول 2" width="220"/></td>
    <td align="center"><img src="showcase/login3-portrait.png" alt="دخول 3" width="220"/></td>
  </tr>
</table>

### الرئيسية والإعدادات
<table>
  <tr>
    <td align="center"><img src="showcase/main%20page-portrait.png" alt="الصفحة الرئيسية" width="220"/></td>
    <td align="center"><img src="showcase/settings-portrait.png" alt="الإعدادات" width="220"/></td>
  </tr>
</table>

### صفحات المنتج
<table>
  <tr>
    <td align="center"><img src="showcase/product1-portrait.png" alt="منتج 1" width="220"/></td>
    <td align="center"><img src="showcase/product2-portrait.png" alt="منتج 2" width="220"/></td>
  </tr>
</table>

## المعمارية

```text
┌──────────────────┐     ┌────────────────────┐     ┌─────────────────────┐
│  Views / Widgets │ ──▶ │  Providers (state) │ ──▶ │  Services / Models  │
│  screens + UI    │     │  Auth · Barcode    │     │  Dio · OFF · DTOs   │
└──────────────────┘     └────────────────────┘     └─────────────────────┘
         │                          │
         │                          ▼
         │                 Firebase Auth / Google
         ▼
   الكاميرا + الأذونات → بيانات منتج Open Food Facts
```

**فصل المسؤوليات**
- `views/` — الشاشات وودجت العرض
- `providers/` — تنسيق المصادقة والمسح (`ChangeNotifier`)
- `service/` — جلب المنتجات عبر HTTP (Dio → Open Food Facts)
- `modules/` — نماذج منتج/مغذيات ذات أنواع من JSON الـ API

## هيكل المشروع

```text
lib/
├── main.dart                 # تهيئة Firebase + تشغيل MultiProvider
├── firebase_options.dart     # إعداد منصات FlutterFire
├── modules/
│   └── product.module.dart   # ProductsModel · Product · Nutriments
├── providers/
│   ├── auth_provider.dart    # بريد/كلمة مرور + تسجيل دخول Google
│   └── bracode_provider.dart # أذونات الكاميرا + تدفق الماسح
├── service/
│   └── product.service.dart  # عميل API الخاص بـ Open Food Facts
└── views/
    ├── screens/              # الترحيب، المصادقة، الرئيسية، المنتج، الهيكل الرئيسي
    └── widgets/              # رأس المنتج وقطع UI مشتركة

assets/                       # الهوية + صور الترحيب
showcase/                     # لقطات شاشة لهذا الـ README
android/ · ios/               # مشاريع المنصات + إعداد Firebase
```

## التقنيات المستخدمة

| الطبقة | الاختيار |
|-------|--------|
| الإطار | Flutter · Dart `^3.9.2` |
| المصادقة | `firebase_core` · `firebase_auth` · `google_sign_in` |
| الحالة | `provider` |
| الشبكات | `dio` → Open Food Facts REST (`/api/v0/product/{barcode}`) |
| المسح | `simple_barcode_scanner` · `permission_handler` |
| UI | `animated_bottom_navigation_bar` · `cached_network_image` · `icons_plus` |
| التحقق | `email_validator` |

قائمة الاعتماديات الكاملة: [`pubspec.yaml`](pubspec.yaml)

## حقول Open Food Facts المستخدمة

يطلب مشغّل المنتجات مجموعة حقول مركّزة (وليس التفريغ الكامل):

`product_name` · `brands` · `quantity` · `nutriscore_grade` · `ecoscore_grade` · `ingredients_text` · `allergens_tags` · `nutriments` · `categories_tags` · `image_url` · `nova_group`

## البدء

**المتطلبات الأساسية**
- Flutter SDK (Dart 3.9+)
- Android Studio / Xcode حسب الحاجة
- مشروع Firebase مع تفعيل المصادقة (بريد + Google)

```bash
git clone https://github.com/baraa404/Healthy_scan.git
cd Healthy_scan
flutter pub get
```

**Firebase**
- تأكد من [`lib/firebase_options.dart`](lib/firebase_options.dart)
- Android: `android/app/google-services.json`
- iOS: `GoogleService-Info.plist` داخل هدف Runner

**الأذونات**
- إدخالات الكاميرا في Android داخل `AndroidManifest.xml`
- سلسلة استخدام الكاميرا في iOS داخل `ios/Runner/Info.plist`

**التشغيل**

```bash
flutter devices
flutter run -d android   # أو ios / chrome / linux / macos / windows
```

## أوامر مفيدة

```bash
flutter clean && flutter pub get
flutter analyze
flutter test
```

## ملاحظات للمراجعين

- اسم الحزمة في `pubspec.yaml` ما زال `depi_project` (معرّف الدورة/المشروع الأصلي)؛ الاسم التجاري للمنتج هو **Healthy Scan**.
- إعداد Firebase للعميل متوقع في تطبيقات Flutter؛ لا ترفع أسرار خادم خاصة.
- مسح الكاميرا يُختبر بشكل أفضل على **جهاز حقيقي**.

## الترخيص

مشروع شخصي / بورتفوليو. تواصل معي إن أردت إعادة استخدامه أو توسعته.