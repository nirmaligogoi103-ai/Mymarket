# MyMarket — Phase 5

Original buyer/seller marketplace starter for Android + iOS.

## Included
- Flutter buyer/seller app UI
- Node.js + Express REST API
- PostgreSQL schema
- JWT authentication and role checks
- Seller approval flow
- Product create/update/delete API
- Buyer checkout and order tracking
- Seller order dashboard and status updates
- OTP request/verify foundation
- Buyer–seller chat API + Server-Sent Events stream
- Payment gateway adapter endpoint (safe mock mode until real credentials are added)
- Admin seller/order/statistics APIs

## 1. Backend
Requirements: Node.js 20+, PostgreSQL 15+.

```bash
cd server
npm install
cp .env.example .env
```

Create a PostgreSQL database and run:

```bash
psql "$DATABASE_URL" -f db/schema.sql
npm start
```

The API runs on `http://localhost:4000` by default.

### Environment
Do not put passwords/API secrets in source code or send them in chat. Put them in `.env` or your hosting provider's secret manager.

Important variables:
- `DATABASE_URL`
- `JWT_SECRET`
- `PAYMENT_MODE=mock` initially
- `ALLOW_BOOTSTRAP_ADMIN=false` initially

OTP uses a development code (`123456`) only when `NODE_ENV=development`; connect a real SMS provider before production.

## 2. Flutter app
Install Flutter 3.x, then:

```bash
cd mobile
flutter pub get
flutter run --dart-define=API_BASE_URL=http://10.0.2.2:4000/api
```

For a physical Android phone, replace `10.0.2.2` with the computer's LAN IP, for example:

```bash
flutter run --dart-define=API_BASE_URL=http://192.168.1.10:4000/api
```

For iOS Simulator use `http://127.0.0.1:4000/api`.

## 3. Seller approval
New sellers are not allowed to publish products until an admin approves them.
An admin can use:
- `GET /api/admin/sellers`
- `PATCH /api/admin/sellers/:id/approve`

Bootstrap is intentionally disabled by default. If you control the deployment, enable it temporarily with `ALLOW_BOOTSTRAP_ADMIN=true` and call `POST /api/admin/make-first-admin` with the registered admin email, then disable the flag again.

## 4. Payments
The mobile app creates an order, then requests a payment intent. The API currently returns a mock payment reference. A real provider such as Razorpay can be added inside the payment adapter without exposing secrets to the mobile app.

Never ship secret payment keys inside Flutter code.

## 5. Production checklist
Before publishing:
- HTTPS for API and database connections
- Real SMS/OTP provider
- Real payment gateway + webhook signature verification
- Object storage/CDN for product images
- Push notifications
- Rate limiting and request validation
- Database backups and migrations
- Privacy policy, terms, refund/cancellation rules
- Android Play Console and Apple Developer setup
- Production monitoring/logging

This package is a functional development foundation, not a claim that a store account, payment account, SMS provider, hosting account, or app-store submission has already been connected.
