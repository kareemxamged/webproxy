# Deploy — Corrosion Web Proxy

> A fast, self-hosted web proxy built on the [Corrosion](https://github.com/EnginexNetwork/corrosion) engine.  
> Browse freely with XOR-encoded URLs, full WebSocket support, and instant quick-access links.


![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![Webpack](https://img.shields.io/badge/Webpack-8DD6F9?style=flat&logo=webpack&logoColor=black)
![Bootstrap](https://img.shields.io/badge/Bootstrap_3-7952B3?style=flat&logo=bootstrap&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## Overview

**Deploy** is a lightweight, one-click-deployable web proxy frontend built on top of the **Corrosion** proxy engine. It rewrites HTML, CSS, and JavaScript on the fly so that any web page loads through your own server — keeping your browsing private and unrestricted. URL paths are obfuscated with XOR encoding, and the bundled client script is compiled automatically via Webpack on first boot.

---

## Key Features

- **XOR URL Encoding** — All proxied URLs are encoded with an XOR cipher, obscuring destinations from network observers.
- **Full WebSocket Support** — Proxies real-time WebSocket connections alongside standard HTTP requests.
- **HTML / CSS / JS Rewriting** — On-the-fly rewriting of hyperlinks, stylesheets, and scripts so pages render correctly through the proxy.
- **Response Decompression** — Automatically handles `gzip` / `deflate` / `br` encoded responses.
- **Domain Blacklisting Middleware** — Block specific hostnames (e.g. `accounts.google.com`) with a configurable deny-list.
- **Force HTTPS** — Option to upgrade all proxied requests to HTTPS.
- **Cookie Passthrough** — Preserves session cookies for authenticated browsing.
- **Quick Access Links** — Pre-built shortcuts to YouTube, Twitch, Brave Search, Libreddit, and Invidious.
- **Auto Script Bundling** — Webpack bundles the client-side injection script automatically at startup if no bundle exists.
- **One-Click Deployment** — Ready-to-deploy configs for Heroku, Replit, and Glitch.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Web Framework | Express 4 |
| Proxy Engine | Corrosion 1.x |
| JS Rewriting | acorn-hammerhead |
| HTML Parsing | parse5 |
| CSS Parsing | css-tree |
| Client Bundler | Webpack 5 |
| UI Framework | Bootstrap 3 |
| Icons | Font Awesome 5 |
| Fonts | Google Fonts (Poppins, Montserrat) |

---

## Getting Started

### Prerequisites

- **Node.js** v14 or higher
- **npm** v6 or higher

### Local Setup

```bash
# 1. Clone the repository
git clone https://github.com/kareemxamged/webproxy.git
cd deploy

# 2. Install dependencies
npm install

# 3. Start the server
npm start
```

The proxy will be available at **http://localhost:8080**.

> On first boot, Webpack will automatically compile the client injection bundle (`lib/server/bundle.js`). This may take a few seconds — wait for `Bundled scripts` in the console before testing.

---

## Environment Variables

| Variable | Default | Description |
|---|---|---|
| `PORT` | `8080` | The port the Express server listens on. Automatically set by Heroku, Replit, and Glitch. |

---

## Project Structure

```
deploy/
├── index.js              # Entry point — Express server & Corrosion config
├── package.json
├── public/               # Static frontend assets
│   ├── index.html        # Main proxy UI with search bar & quick links
│   ├── games.html        # Games page
│   ├── about.html        # About page
│   ├── index.js          # Client-side navigation logic
│   ├── app.js            # App utilities
│   ├── style.css         # Global styles
│   └── particles.js      # Particle background animation
└── lib/
    ├── browser/          # Client-side injection scripts (bundled by Webpack)
    │   ├── index.js
    │   ├── document.js
    │   ├── history.js
    │   ├── http.js
    │   ├── location.js
    │   └── worker.js
    └── server/           # Server-side proxy engine
        ├── index.js      # Corrosion class
        ├── request.js    # HTTP request proxy
        ├── upgrade.js    # WebSocket proxy
        ├── gateway.js    # Gateway handler
        ├── headers.js    # Header rewriting
        ├── middleware.js # blacklist / address middleware
        ├── decompress.js # Response decompression
        └── rewrite-body.js
```

---

## Configuration Reference

The proxy is configured in `index.js` via the `Corrosion` constructor:

```js
const proxy = new Corrosion({
    prefix: "/service/",       // URL prefix for all proxied routes
    codec: "xor",              // URL encoding: "xor" | "plain" | "base64"
    title: "Deploy",           // Browser tab title for proxied pages
    forceHttps: true,          // Upgrade proxied requests to HTTPS
    requestMiddleware: [
        Corrosion.middleware.blacklist(["accounts.google.com"], "Page is blocked"),
    ]
})
```

---

## Author

Built by **Kareem Amged**


---

## نظرة عامة

**Deploy** هو واجهة أمامية خفيفة لوكيل الويب قابلة للنشر بنقرة واحدة، مبنية على محرك الوكيل **Corrosion**. يُعيد كتابة HTML وCSS وJavaScript أثناء التحميل بحيث تُحمَّل أي صفحة ويب عبر خادمك الخاص — مما يحافظ على خصوصية تصفحك ويزيل القيود. يتم تشفير مسارات URL باستخدام XOR، ويُجمَّع سكريبت العميل تلقائيًا عبر Webpack عند أول تشغيل.

---

## المميزات الرئيسية

- **ترميز XOR للروابط** — يُشفَّر كل رابط مُوكَّل بشيفرة XOR، مما يُخفي الوجهات عن مراقبي الشبكة.
- **دعم كامل لـ WebSocket** — يُوكِّل اتصالات WebSocket الفورية إلى جانب طلبات HTTP العادية.
- **إعادة كتابة HTML / CSS / JS** — إعادة كتابة فورية للروابط والأنماط والسكريبتات لضمان تحميل الصفحات بشكل صحيح.
- **فك ضغط الاستجابات** — يتعامل تلقائيًا مع الاستجابات المضغوطة بصيغ `gzip` و`deflate` و`br`.
- **وسيط حظر النطاقات** — حظر نطاقات معينة (مثل `accounts.google.com`) بقائمة حظر قابلة للتخصيص.
- **إجبار HTTPS** — خيار لترقية جميع الطلبات المُوكَّلة إلى HTTPS.
- **تمرير ملفات تعريف الارتباط** — يحافظ على جلسات المصادقة.
- **روابط وصول سريع** — اختصارات جاهزة لـ YouTube وTwitch وBrave Search وLibreddit وInvidious.
- **تجميع سكريبت تلقائي** — يُجمِّع Webpack سكريبت الحقن من جانب العميل تلقائيًا عند التشغيل.
- **نشر بنقرة واحدة** — إعدادات جاهزة للنشر على Heroku وReplit وGlitch.

---

## التقنيات المستخدمة

| الطبقة | التقنية |
|---|---|
| بيئة التشغيل | Node.js |
| إطار الويب | Express 4 |
| محرك الوكيل | Corrosion 1.x |
| إعادة كتابة JS | acorn-hammerhead |
| تحليل HTML | parse5 |
| تحليل CSS | css-tree |
| مُجمِّع العميل | Webpack 5 |
| إطار واجهة المستخدم | Bootstrap 3 |
| الأيقونات | Font Awesome 5 |
| الخطوط | Google Fonts (Poppins, Montserrat) |

---

## البدء السريع

### المتطلبات

- **Node.js** الإصدار 14 أو أحدث
- **npm** الإصدار 6 أو أحدث

### الإعداد المحلي

```bash
# 1. استنساخ المستودع
git clone https://github.com/kareemxamged/webproxy.git
cd deploy

# 2. تثبيت التبعيات
npm install

# 3. تشغيل الخادم
npm start
```

سيكون الوكيل متاحًا على **http://localhost:8080**.

> عند التشغيل الأول، سيقوم Webpack تلقائيًا بتجميع حزمة الحقن للعميل (`lib/server/bundle.js`). قد يستغرق هذا بضع ثوانٍ — انتظر ظهور `Bundled scripts` في وحدة التحكم قبل الاختبار.

---

## متغيرات البيئة

| المتغير | القيمة الافتراضية | الوصف |
|---|---|---|
| `PORT` | `8080` | المنفذ الذي يستمع عليه خادم Express. يُضبط تلقائيًا من قِبَل Heroku وReplit وGlitch. |

---

## هيكل المشروع

```
deploy/
├── index.js              # نقطة الدخول — إعداد Express وCorrosion
├── package.json
├── public/               # أصول الواجهة الأمامية الثابتة
│   ├── index.html        # واجهة المستخدم الرئيسية مع شريط البحث وروابط سريعة
│   ├── games.html        # صفحة الألعاب
│   ├── about.html        # صفحة حول المشروع
│   ├── index.js          # منطق التنقل من جانب العميل
│   ├── app.js            # أدوات مساعدة
│   ├── style.css         # الأنماط العامة
│   └── particles.js      # تأثير الجسيمات المتحركة في الخلفية
└── lib/
    ├── browser/          # سكريبتات الحقن للعميل (تُجمَّع بـ Webpack)
    └── server/           # محرك الوكيل من جانب الخادم
```

---

## مرجع الإعداد

يتم تهيئة الوكيل في `index.js` عبر منشئ `Corrosion`:

```js
const proxy = new Corrosion({
    prefix: "/service/",       // بادئة URL لجميع المسارات المُوكَّلة
    codec: "xor",              // ترميز URL: "xor" | "plain" | "base64"
    title: "Deploy",           // عنوان تبويب المتصفح للصفحات المُوكَّلة
    forceHttps: true,          // ترقية الطلبات إلى HTTPS
    requestMiddleware: [
        Corrosion.middleware.blacklist(["accounts.google.com"], "Page is blocked"),
    ]
})
```

---

## المؤلف

أُنشئ بواسطة **Kareem Amged**.
