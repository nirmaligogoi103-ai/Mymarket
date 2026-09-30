# MyMarket deployment checklist

## Local production-like run
1. Install Docker Desktop.
2. From this folder run: `docker compose up --build`.
3. API health check: `http://localhost:4000/health`.
4. Flutter API URL: set `mobile/lib/config.dart` to the machine's reachable API URL.

## Before real launch
- Use a managed PostgreSQL database and TLS.
- Generate a strong random JWT_SECRET and store it only in hosting secrets.
- Set ALLOW_BOOTSTRAP_ADMIN=false after any one-time admin bootstrap.
- Replace PAYMENT_MODE=mock with the chosen payment provider's server-side integration and verify webhooks.
- Connect a verified OTP/SMS provider.
- Add HTTPS, rate limiting, request validation, backups, logging and monitoring.
- Create Android and iOS signing credentials in the respective developer consoles.
- Never commit `.env`, API secrets, database passwords, signing keys or payment secrets.

## Important
The included payment flow is intentionally mock/test-only. Do not use it to accept real customer payments until a payment provider and webhook verification are configured.
