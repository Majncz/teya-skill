# ePOS SDK Glossary

Understand key terms and concepts used throughout the Teya ePOS SDK documentation. This glossary covers technical terminology, payment processing concepts, and industry-specific definitions.

## A - E

### API (Application Programming Interface)
A set of protocols and tools that allow different software applications to communicate with each other. The ePOS SDK provides APIs for payment processing, inventory management, and hardware integration.

### Authorization
The process of verifying that a payment card has sufficient funds and that the transaction is legitimate. This step occurs before a payment is captured or settled.

### Batch Processing
The practice of processing multiple transactions together at scheduled intervals, typically used for settlement and reporting purposes.

### Capture
The process of requesting funds transfer from a previously authorized transaction. Funds are typically captured when goods are shipped or services are delivered.

### EMV
Europay, Mastercard, and Visa standard for chip card payments that provides enhanced security through dynamic authentication for each transaction.

### ePOS (Electronic Point of Sale)
A digital system that combines hardware and software to process sales transactions, manage inventory, track customers, and generate reports.

## F - P

### Gateway
A service that processes payment transactions by securely transmitting transaction data between merchants, payment processors, and banks.

### Inventory Management
The system for tracking product quantities, locations, and movement throughout the supply chain, integrated into the ePOS system for real-time stock updates.

### Merchant Account
A special type of business bank account that allows merchants to accept and process electronic payments from customers.

### NFC (Near Field Communication)
A wireless communication technology that enables contactless payments by allowing devices to exchange data when in close proximity (typically within 4 cm).

### PCI DSS
Payment Card Industry Data Security Standard - a set of security requirements designed to protect cardholder data throughout payment processing.

### POSLink
A communication protocol that enables ePOS applications to integrate with external systems, including legacy POS systems, payment terminals, and back-office software.

## R - Z

### Refund
The process of returning funds to a customer's payment method, typically for returned merchandise or cancelled services.

### SDK (Software Development Kit)
A collection of software development tools, documentation, code samples, and guides that developers use to create applications for specific platforms or services.

### Settlement
The final step in payment processing where funds are transferred from the customer's account to the merchant's account, typically occurring 1-3 business days after authorization.

### Terminal
A hardware device used to process payment transactions, including card readers, PIN pads, and contactless payment acceptance devices.

### Token/Tokenization
A security technique that replaces sensitive payment card data with unique identification symbols (tokens) that retain essential information without compromising security.

### Void
The cancellation of a transaction before settlement, preventing funds from being transferred. Voids must typically occur on the same business day as the original transaction.

### Webhook
An HTTP callback mechanism that allows the ePOS system to receive real-time notifications about events such as successful payments, failed transactions, or inventory updates.

## Payment Methods

### Traditional Cards
- Visa, Mastercard, American Express
- Debit cards with PIN verification
- Chip and PIN/signature cards
- Magnetic stripe (legacy support)

### Digital Payments
- Apple Pay, Google Pay, Samsung Pay
- Contactless card payments (tap to pay)
- QR code payments
- Bank transfer integrations

> **Tip:** Use this glossary as a quick reference while implementing ePOS SDK features in your application.
