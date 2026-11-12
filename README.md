# Stripe Integration: Card Payments (Node.js)

Express server + Stripe Payment Element (PaymentIntents API, cards only).

## Setup
1. Copy your **test** keys from https://dashboard.stripe.com/test/apikeys into `.env`
2. `npm install`
3. `npm run test-install`: verifies the SDK + secret key (creates a test product/price)
4. `npm start` → open http://localhost:4242

## Webhooks (local)
```
stripe login
stripe listen --forward-to localhost:4242/webhook
```
Paste the printed `whsec_...` into `.env` as `STRIPE_WEBHOOK_SECRET`, restart the server.

## Test cards (any future expiry, any CVC, any ZIP)
| Card                | Result                    |
|---------------------|---------------------------|
| 4242 4242 4242 4242 | Succeeds                  |
| 4000 0025 0000 3155 | Requires 3D Secure        |
| 4000 0000 0000 9995 | Declined (insufficient funds) |

## Files
- `server.js`: creates PaymentIntents, handles webhooks
- `public/checkout.js`: mounts the card form, confirms payment
- `public/complete.html`: return page showing final status
# Stripe
