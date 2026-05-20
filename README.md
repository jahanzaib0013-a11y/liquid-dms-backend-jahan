# Liquid DMS — Backend API

> REST API for **Liquid DMS**, a document management system. Express + Mongoose service powering the admin panel: JWT auth, role-based permissions, document/folder CRUD, uploads with image processing, Redis caching and email notifications.

![Runtime](https://img.shields.io/badge/node-express-green)
![DB](https://img.shields.io/badge/mongo-mongoose-0068a5)
![Cache](https://img.shields.io/badge/redis-ioredis-d82c20)

## Overview

This is the server half of the Liquid DMS product (the client is the admin panel in the companion repo). It is a classic Express MVC service backed by MongoDB, with Redis for sessions/caching and a mail layer for notifications.

**Capabilities**

- **Auth** — JWT access tokens, bcrypt password hashing, refresh/session handling.
- **Users & roles** — role-based access control and permissions across documents.
- **Documents** — folders, categories, metadata, versioning/history, full-text search, pagination/sort/filter.
- **Uploads** — `multer` ingestion to disk/cloud, image thumbnails via `sharp`, bulk upload + tagging.
- **Notifications** — email via Nodemailer and SendGrid; subscription settings.
- **Platform** — Redis-backed sessions and response caching, Winston logging, Helmet security, validation (Joi), audit logging.

## Architecture

```
src/
  app.js            Express app wiring (middleware chain)
  index.js          entrypoint (connect DB/Redis, start server)
  config/           env, db and redis configuration
  models/           Mongoose schemas
  controllers/      request handlers
  router/           route modules per feature
  middleware/       auth, error handling, upload guards
  validations/      Joi request schemas
  functions/ utils/  domain + shared helpers
  templates/        email templates
  uploads/ assets/   served media
```

## Getting started

```bash
cp .env.example .env     # set MONGO_URI, REDIS_URL, JWT_SECRET, mail creds
npm install
npm start               # node src/index.js
```

## Scripts

| Script | Purpose |
| --- | --- |
| `npm start` | Start the API server |
| `prepare` | Install Husky hooks |

## Tech stack

Express · Mongoose/MongoDB · ioredis/redis · JSON Web Tokens · bcryptjs · Joi · multer + sharp · Nodemailer + SendGrid · Helmet · Winston · ESLint + Prettier + Husky.

## Environment

Requires a reachable MongoDB and Redis instance, plus SMTP/SendGrid credentials for outbound mail. Secrets are read from `.env` via `dotenv`.

## License

© [Jahanzaib Iftikhar](https://github.com/jahanzaib0013-a11y)
