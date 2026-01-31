# E-Commerce API (beta)

This guide provides an overview for merchants that want to develop integrations with Teya E-Commerce APIs for Hosted Checkout Sessions, Payment Links and Online Payments.

## Overview

Teya Online payments offers a suite of APIs which can be used to integrate your system with our online payment processing solutions. APIs are available to support a range of scenarios, including Hosted Checkout integration, creation and sending of Payment Links, or direct payment processing for advanced merchants or partners whose systems are fully PCI compliant.

## Integration Options

### Hosted Checkout

The best option for most merchants that capture online sales via their webstore or online booking system. The customer shops on your store, completes their basket and registers with you, but they are redirected briefly to our hosted checkout page so that we can securely capture their payment data and return them to your store.

**How it works:**
1. Your system calls our API to get a checkout URL
2. You redirect the customer to that page
3. We take care of 3DS authentication, card data collection and processing, and payment authorization
4. Once the customer completes the purchase, we send them back to you to finalize the process
5. Our system sends a webhook notification to securely provide you with payment confirmation data

### Payment Links

Our payment links API enables you to collect payment from customers that are not in session on your system. Send them a link via email, SMS or your preferred communication channel so that they can click on it and complete payment at their convenience.

**Use cases:**
- One-off sales
- Linking payment processing directly in an invoice email
- Collecting payment from remote customers
- You can receive notification of payment by email or webhook

### Direct Payment Processing

For more advanced merchants or partners whose systems are PCI certified to process card data directly, you can manage the whole experience on your side, and simply send the instruction to process a given payment on a set of payment data.

## Prerequisites

Ask your Teya representative to set up your Teya merchant account for the Staging environment.

Management of credentials and webhooks is done at the store level, via Teya Business Portal:

- **Staging** (testing): https://business.teya.xyz
- **Production** (live): https://business.teya.com

### Creation and Management of API Credentials

1. In the Teya Business Portal, go to your settings and select the store for which you want to create new API credentials.
2. Under "Integrations", create your new credentials, giving them a significant name.
3. Make sure to securely store your client secret, as it will be only shown once. If you lose your credentials, simply revoke then and create a new set.

### Creation and Management of Webhooks

1. In the Teya Business Portal, go to your settings and select the store for which you want to add a new webhook.
2. Under "Integrations", add your new webhook, giving it a significant name.

**Supported event types:**
- Payment Succeeded

## Token Management

### Important Distinctions Between Test and Live Environments

- **Separate Tokens:** Independent caches for staging and production environments
- **Environment-Specific Endpoints:** Different OAuth URLs for test (id.teya.xyz) vs live (id.teya.com)

### Key Points on Token Behaviour

- **Short-Lived Tokens:** 15 minutes in production, 24 hours in Staging
- **Safety First:** 1-minute buffer prevents API calls with expired tokens

### Exchange Credentials for Tokens

Use the OAuth credentials to obtain access tokens.

> **Note:** The Header Content-Type must be `application/x-www-form-urlencoded`

**POST** `https://id.teya.com/oauth/v2/oauth-token`

#### Parameters

| Param | Description |
|-------|-------------|
| `grant_type` (required) | Credentials created via Teya Business Portal can only be used for `client_credentials` |
| `client_id` (required) | Created in Teya Business Portal |
| `client_secret` (required) | Created in Teya Business Portal |
| `scopes` | Abilities of the token (see below) |

**Available Scopes:**
- `checkout/sessions/create` → create sessions
- `checkout/sessions/id/get` → get sessions
- `payment-links/create` → create payment links
- `payment-links/id/get` → get payment links
- `payment-links/id/update` → update payment links
- `transactions/online/create` → create online transactions
- `transactions/online/id/get` → get online transactions
- `fx/dcc/create` → check DCC eligibility
- `refunds/create` → do refunds
- `transactions/id/receipts/create` → create receipts for a transaction

You can generate the token with any list of scopes your application needs.

#### Request Example

```bash
curl --location --request POST 'https://id.teya.com/oauth/v2/oauth-token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>' \
--data-urlencode 'scope=checkout/sessions/create refunds/create'
```

#### Response Example

```json
{
  "access_token": "_0XBPWQQ_.....",
  "token_type": "bearer",
  "expires_in": 900,
  "scope": "checkout/sessions/create refunds/create"
}
```
