# Test Cards for Payments API

Use these test card numbers to simulate different payment scenarios during development and testing. These cards will trigger various responses and help you test different flows in your integration.

## How to Use Test Cards

- **Environment:** Test cards only work in development/sandbox environments
- **CVV:** Use any 3-digit number for CVV (e.g., 123, 456, 789)
- **Expiry Date:** Use any future date (e.g., 12/25, 06/26, 10/27)
- **Cardholder Name:** Use any name for testing

## Test Payment Cards

| Brand | Card Number | Use Case | CVV |
|-------|-------------|----------|-----|
| Visa | 4242424242424242 | Visa testing | Any 3-digit (e.g., 123) |
| Mastercard | 5555555555554444 | Mastercard testing | Any 3-digit (e.g., 456) |
| American Express | 378282246310005 | Amex testing | Any 4-digit (e.g., 6789) |
| Mastercard | 2223600089700011 | Mastercard DCC testing (EUR) | Any 3-digit (e.g., 123) |

## Testing Best Practices

- **Test All Scenarios:** Use cards from each category to ensure your integration handles all possible responses
- **Error Handling:** Pay special attention to declined and error cards to test your error handling logic
- **Async Processing:** Use processing delay cards to test your webhook and polling implementations
- **Security:** Test 3D Secure cards to ensure your authentication flows work correctly
- **Amount Variations:** Test with different amounts (small, large, with decimals) to ensure proper handling
- **Currency Testing:** Test with different currencies (EUR, USD, GBP) if your integration supports multiple currencies

## Important Notes

> ⚠️ These test card numbers will only work in development/sandbox environments. Never use real card details in testing, and ensure test cards don't work in production.

- **Production Safety:** Test cards are automatically rejected in production environments
- **PCI Compliance:** Never store test card details in production systems
- **Logging:** Be careful when logging test card data - treat it like real card data
- **Documentation:** Always document which test cards you're using in your test scenarios
