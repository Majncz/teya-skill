# Introduction to All-In-One Integration

The All-In-One (AIO) integration allows the ePOS application and the Teya payment terminal application to run on the same Android device. Both applications communicate via deeplinks, while the SDK handles authentication and provides a ready-to-use payment UI. This integration is ideal for partners who want a single-device solution.

## When to Use All-In-One

Choose All-In-One when you want a single-device solution that combines the POS and payment terminal functions. For example:

- Running your ePOS app directly on a Teya Android terminal to take payments and print receipts from the same device.

## Key Benefits

- **Single-Device Workflow:** POS and payment terminal operate on the same Android device
- **Receipt Printing Support:** Can use Sunmi or PAX printer SDKs for receipt printing
- **Direct Communication:** Applications communicate via deeplinks without cloud dependency
- **Consistent Payment Experience:** SDK provides ready-to-use payment UI

## Integration Checklist

### 1. Request a Debug Terminal

- Contact your **Partnership Manager** to request a **debug terminal**.
- When requesting, specify which **terminal model** (e.g., Sunmi or PAX) you need for development.

### 2. Test Merchant Account

- A **test merchant account** must be registered and assigned to the debug terminal.
- Your Partnership Manager will assist with creating and linking this account.

### 3. Start Development

- Once the debug terminal and test merchant account are set up, you can start development by integrating the SDK using the guides and code samples.

## Supported Terminal Models

- **Sunmi** terminals
- **PAX** terminals

## Platform Support

- **Android only** - All-In-One integration is exclusively for Android devices
