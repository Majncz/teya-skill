# Payments Gateway Service Overview (beta)

The Payments Gateway Service API is a comprehensive RESTful API that processes payment transactions, handles refunds and reversals, and manages captures for the Teya Platform. This API enables secure payment processing for various transaction types including card-present, MOTO, and SoftPOS transactions.

For online and e-commerce payment processing, see the [E-Commerce API](./e-commerce-introduction.md).

## Authentication

The API uses OAuth 2.0 authentication with the following flows:
- Authorization Code flow for external access

**Token URLs:**
- **Development:** https://id.teya.xyz/oauth/v2/oauth-token
- **Production:** https://id.teya.com/oauth/v2/oauth-token

## Use Cases and Workflows

### Card Present Transactions

**Endpoint:** `POST /v1/transactions/card-present`

**When to use:**
- Physical terminal/POS transactions
- Card is physically present and inserted/tapped
- EMV chip card transactions
- Contactless payments

**Example - Processing €25 card present transaction:**

```bash
curl -X POST "https://base-url.salt/api/v1/transactions/card-present" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: terminal-txn-12345" \
  -d '{
    "type": "SALE",
    "entry_mode": "CONTACT_EMV",
    "verification_method": "ONLINE_PIN",
    "amounts": {
      "amount": 2500,
      "currency": "EUR"
    },
    "emv_data": "5F2A020978820200009F3602...",
    "track_data": {
      "encryption_key_id": "5EE0",
      "encrypted_track": "5188340000000011D241212099999999",
      "encryption_ksn": "123456789012"
    },
    "transacted_at": "2024-01-15T10:30:00.000Z"
  }'
```

### Pre-auth & Capture

**Endpoints:** 
- `POST /v1/transactions/card-present` (with PRE_AUTHORISATION type)
- `POST /v1/transactions/{id}/capture`

**When to use:**
- Hotel, car rental, or reservation scenarios with physical card
- Need to reserve funds before actual charge
- Variable final amount (e.g., with tips or additional services)
- Card is physically present for pre-authorization

**Example - Hotel reservation (€100 pre-auth, €120 capture):**

```bash
# Step 1: Create pre-authorization at hotel front desk
curl -X POST "https://base-url.salt/api/v1/transactions/card-present" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: hotel-preauth-12345" \
  -d '{
    "type": "PRE_AUTHORISATION",
    "entry_mode": "CONTACT_EMV",
    "verification_method": "ONLINE_PIN",
    "amounts": {
      "amount": 10000,
      "currency": "EUR"
    },
    "emv_data": "5F2A020978820200009F3602...",
    "track_data": {
      "encryption_key_id": "5EE0",
      "encrypted_track": "5188340000000011D241212099999999",
      "encryption_ksn": "123456789012"
    },
    "transacted_at": "2024-01-15T14:00:00.000Z"
  }'

# Step 2: Capture with final amount at checkout
curl -X POST "https://base-url.salt/api/v1/transactions/tr_12345/capture" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: hotel-capture-12345" \
  -d '{
    "amount": 12000
  }'
```

### Refunds

**Endpoint:** `POST /v3/refunds`

**When to use:**
- Customer requests refund for completed transaction
- Partial or full refund scenarios
- Returns processing

**Example - Processing €30 partial refund from €50 transaction:**

```bash
curl -X POST "https://base-url.salt/api/v3/refunds" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: refund-67890" \
  -d '{
    "transaction_id": "tr_87de9bea-b32d-4ef5-a481-b8ba48764325",
    "amount": 3000
  }'
```

## Usage Notes

1. **UUID Format:** Transaction IDs and merchant IDs must be valid UUIDs where specified
2. **Amount Format:** Amounts are in minor units (e.g., 100 for €1.00, 5000 for €50.00)
3. **Currency Format:** All currencies must be in ISO-4217 format (3-letter codes: EUR, USD, GBP, etc.)
4. **Idempotency:** Use Idempotency-Key headers to prevent duplicate transactions
5. **Authentication:** All requests require valid OAuth 2.0 bearer tokens
6. **Transaction Types:** Supported types include AUTHORISATION, CAPTURE, REFUND, REVERSAL
7. **Card Brands:** Supported brands include VISA, MASTERCARD, MAESTRO, AMEX, JCB, DINERS, DISCOVER
8. **Date Format:** All timestamps use ISO-8601 format

## Additional Resources

- **Test Cards:** See [test-cards.md](./test-cards.md) for test card numbers
