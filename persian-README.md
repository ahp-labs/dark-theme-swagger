# 🌙 تم تاریک Swagger — مستندات فارسی

این ریپازیتوری شامل یک **تم حرفه‌ای، مدرن و Dark-Neon** برای Swagger UI است که ظاهر پیش‌فرض را کاملاً تغییر می‌دهد و یک رابط کاربری بسیار جذاب شبیه پنل‌های DevOps مدرن ایجاد می‌کند.

این README توضیح می‌دهد که چگونه این تم را در هر دو فریم‌ورک **Express.js** و **NestJS** استفاده کنید.

---

## 🔄 تغییر زبان

**[English Version](./README.md)**

---

# ✨ امکانات تم

* طراحی تاریک حرفه‌ای با گرادیان‌ها و شیشه‌ای (Glassmorphism)
* استایل اختصاصی کارت API ها، دکمه‌ها، اینپوت‌ها و هدرها
* سازگار با Swagger UI نسخه‌های جدید
* هدر سفارشی با لوگو
* رنگ‌بندی جداگانه برای GET, POST, PUT, DELETE
* اصلاح کامل بخش Server ها (رفع باکس سفید)

---

# 📁 ساختار پوشه پیشنهادی

```
project-root/
 ├── swagger/
 │    ├── dark-swagger.css
 │    └── swagger.js   ← فقط برای پروژه‌های Express
 └── ...
```

---

# 🚀 استفاده در Express.js

## 1) نصب پکیج‌ها

```bash
npm install swagger-ui-express swagger-jsdoc
```

## 2) قرار دادن فایل CSS

فایل **dark-swagger.css** را در مسیر زیر قرار دهید:

```
/swagger/dark-swagger.css
```

## 3) پیکربندی swagger.js

```js
const swaggerJsdoc = require('swagger-jsdoc');
const swaggerUi = require('swagger-ui-express');
const path = require('path');
const fs = require('fs');

const swaggerOptions = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'API Documentation',
      version: '1.0.0',
      description: 'Dark Swagger Theme Example',
    },
  },
  apis: ['./routes/*.js'],
};

const swaggerSpec = swaggerJsdoc(swaggerOptions);

module.exports = (app) => {
  app.use('/docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec, {
    customCss: fs.readFileSync(path.join(__dirname, 'dark-swagger.css'), 'utf8'),
    customJs: `
      const header = document.createElement('div');
      header.className = 'custom-header';
      header.innerHTML = ` +
      "`<span class=\"custom-header-title\">Dark Swagger Theme</span>`" + `;
      document.body.prepend(header);
    `,
    customSiteTitle: 'Dark Swagger UI',
  }));
};
```

## 4) استفاده در app.js

```js
const express = require('express');
const app = express();

require('./swagger/swagger')(app);

app.listen(3000, () => console.log('Docs → http://localhost:3000/docs'));
```

---

# 🚀 استفاده در NestJS

## 1) نصب پکیج Swagger

```bash
npm install @nestjs/swagger swagger-ui-express
```

## 2) اضافه کردن فایل CSS

```
/swagger/dark-swagger.css
```

## 3) پیکربندی main.ts

```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';
import * as fs from 'fs';
import * as path from 'path';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('Dark Swagger Theme')
    .setDescription('Custom Swagger Theme for NestJS')
    .setVersion('1.0')
    .build();

  const document = SwaggerModule.createDocument(app, config);

  SwaggerModule.setup('docs', app, document, {
    customCss: fs.readFileSync(path.join(__dirname, '../swagger/dark-swagger.css'), 'utf8'),
    customJs: `
      const header = document.createElement('div');
      header.className = 'custom-header';
      header.innerHTML = `<span class=\"custom-header-title\">Dark Swagger Theme</span>`;
      document.body.prepend(header);
    `,
    customSiteTitle: 'Dark Swagger UI for Nest',
  });

  await app.listen(3000);
  console.log('Docs → http://localhost:3000/docs');
}
bootstrap();
```

---

# 🧪 تست تم

با اجرای پروژه، Swagger UI با ظاهر کاملاً جدید لود می‌شود.

✔ GET – آبی
✔ POST – سبز
✔ PUT – نارنجی
✔ DELETE – قرمز

---

# ❤️ نویسنده

این تم توسط **ahp-labs** طراحی شده.
