<div align="center">

# 🔁 Replit XHTTP Relay

<img src="https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=node.js&logoColor=white" />
<img src="https://img.shields.io/badge/Replit-Deploy-F26207?style=for-the-badge&logo=replit&logoColor=white" />
<img src="https://img.shields.io/badge/XHTTP-Relay-blue?style=for-the-badge" />

**ريلاي XHTTP خفيف وسريع يعمل على Replit — يقوم بتوجيه الطلبات إلى سيرفرك الخاص (VPS) عبر بروكسي عكسي.**

---

</div>

## 📋 الوصف

هذا المشروع عبارة عن **Reverse Proxy Relay** مبني بـ Node.js، مصمم للعمل على منصة **Replit** كوسيط بين العميل والسيرفر الهدف. يقوم بتمرير جميع الطلبات (GET, POST, PUT, DELETE, etc.) إلى الدومين المستهدف مع تنظيف الهيدرز غير الضرورية للحفاظ على الخصوصية والأمان.

## ✨ المميزات

| الميزة | الوصف |
|--------|-------|
| 🚀 **خفيف وسريع** | لا يحتاج أي مكتبات خارجية — يعمل بـ Node.js الأساسي فقط |
| 🔒 **تنظيف الهيدرز** | يزيل تلقائياً الهيدرز الحساسة والمكشوفة |
| 🌐 **دعم HTTP/HTTPS** | يدعم التوجيه لكلا البروتوكولين |
| 📡 **Streaming** | يدعم تمرير البيانات بالـ Stream للأداء العالي |
| ☁️ **جاهز للنشر** | مُعد مسبقاً للنشر على Replit بضغطة زر |

## ⚠️ إعداد مهم — تعديل الدومين المستهدف

> **يجب عليك تعديل `TARGET_DOMAIN` في ملف [`index.js`](https://github.com/alrufaaey-yahoo/replit-xhttp-relay/blob/master/index.js) ليشير إلى سيرفرك الخاص (VPS) قبل التشغيل.**

افتح ملف `index.js` وعدّل السطر التالي:

```javascript
const TARGET_DOMAIN = 'https://yourvps:443';
```

استبدل `yourvps` بعنوان IP أو دومين سيرفرك الخاص. مثال:

```javascript
const TARGET_DOMAIN = 'https://123.456.789.0:443';
```

أو باستخدام دومين:

```javascript
const TARGET_DOMAIN = 'https://mydomain.com:443';
```

## 🚀 طريقة النشر على Replit

### الطريقة 1: الاستيراد من GitHub
1. سجل الدخول إلى [Replit](https://replit.com)
2. اضغط على **Create Repl** ثم **Import from GitHub**
3. الصق رابط المستودع:
   ```
   https://github.com/alrufaaey-yahoo/replit-xhttp-relay
   ```
4. اضغط **Import from GitHub**
5. **عدّل `TARGET_DOMAIN`** في `index.js` كما هو موضح أعلاه
6. اضغط **Run** للتشغيل
7. اضغط **Deploy** للنشر والحصول على رابط دائم

### الطريقة 2: إنشاء يدوي
1. أنشئ **Repl** جديد واختر **Node.js**
2. انسخ محتوى `index.js` إلى المشروع
3. **عدّل `TARGET_DOMAIN`** ليشير إلى سيرفرك
4. اضغط **Run** ثم **Deploy**

## 📁 هيكل المشروع

```
replit-xhttp-relay/
├── index.js          # الخادم الرئيسي — الريلاي
├── package.json      # إعدادات المشروع
├── .replit           # إعدادات تشغيل ونشر Replit
├── replit.nix        # بيئة Nix لـ Replit
└── README.md         # هذا الملف
```

## 🔧 كيف يعمل

```
العميل  ──►  Replit Relay  ──►  السيرفر الهدف (VPS)
  ◄──          ◄──                ◄──
```

1. يستقبل الريلاي الطلب من العميل
2. ينظف الهيدرز الحساسة (مثل `host`, `x-forwarded-*`, `proxy-*`)
3. يمرر الطلب إلى `TARGET_DOMAIN`
4. يعيد الاستجابة من السيرفر الهدف إلى العميل

### الهيدرز المحذوفة تلقائياً

| Header | السبب |
|--------|-------|
| `host` | يُستبدل بدومين الهدف |
| `connection` / `keep-alive` | هيدرز اتصال غير ضرورية |
| `proxy-*` | هيدرز بروكسي مكشوفة |
| `x-forwarded-*` | تمنع تسريب معلومات الشبكة |
| `transfer-encoding` | يُعاد ضبطه تلقائياً |
| `x-vercel-*` | هيدرز خاصة بالمنصة |

## 🌍 متغيرات البيئة

| المتغير | الوصف | القيمة الافتراضية |
|---------|-------|-------------------|
| `PORT` | منفذ تشغيل الخادم | `3000` |

## 📝 ملاحظات

- تأكد من أن سيرفرك الهدف يقبل الاتصالات من عناوين IP الخاصة بـ Replit
- الرابط بعد النشر سيكون بصيغة: `https://اسم-المشروع.اسم-المستخدم.repl.co`
- المشروع لا يحتاج أي `npm install` — يعمل بمكتبات Node.js الأساسية فقط

---

<div align="center">

## 👨‍💻 المطور

**تم التطوير بواسطة الرفاعي**

[![Telegram](https://img.shields.io/badge/Telegram-@alrufaaey-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/alrufaaey)

---

<sub>إذا أعجبك المشروع، لا تنسَ ⭐ على GitHub</sub>

</div>
