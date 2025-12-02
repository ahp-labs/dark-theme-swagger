# 📘 Swagger Theme Documentation (English)

This repository includes documentation for using the **Swagger UI Theme** in both **Express.js** and **NestJS**.

➡️ Persian Version: ./persian-README.md

---

# 🚀 Using Swagger Theme in Express.js

This project provides a pre‑built custom Swagger UI theme that you can easily integrate into any Express.js API project.

## 📦 Installation

```bash
npm install swagger-ui-express swagger-jsdoc
```

## 🧩 Folder Structure Example

```
project
 ├─ swagger
 │   ├─ theme.css        # custom theme
 │   └─ swagger.json     # base swagger spec
 └─ src
    └─ app.js
```

## ⚙️ Express Integration Example

```js
const swaggerUi = require('swagger-ui-express');
const swaggerJsdoc = require('swagger-jsdoc');
const path = require('path');

const options = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'API Documentation',
      version: '1.0.0'
    },
  },
  apis: ['./routes/*.js'],
};

const swaggerSpec = swaggerJsdoc(options);

app.use('/docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec, {
  customCss: fs.readFileSync(path.join(__dirname, '../swagger/theme.css'), 'utf8')
}));
```

---

# 🚀 Using Swagger Theme in NestJS

NestJS has built‑in Swagger support. The theme can be applied using the `customCss` property.

## 📦 Installation

```bash
npm install @nestjs/swagger swagger-ui-express
```

## ⚙️ NestJS Integration Example

```ts
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';
import * as fs from 'fs';
import * as path from 'path';

async function setupSwagger(app) {
  const config = new DocumentBuilder()
    .setTitle('API Docs')
    .setVersion('1.0')
    .build();

  const document = SwaggerModule.createDocument(app, config);

  SwaggerModule.setup('docs', app, document, {
    customCss: fs.readFileSync(path.join(__dirname, '..', 'swagger', 'theme.css'), 'utf8'),
  });
}
```

---

## 🎨 Theme File (theme.css)

Just drop your custom CSS here and both Express & NestJS will use it.
Example:

```css
.swagger-ui .topbar { display: none; }
body { background: #0c3066; }
```

---

## 📄 Documentation Versions

* 🇬🇧 English (current)
**[Persian Version](./persian-README.md)**
