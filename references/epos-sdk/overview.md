# ePOS SDK Overview

The Teya Unified SDK enables ePOS applications to integrate with Teya payment terminals on different frameworks using a plug-and-play approach. It removes the complexity of handling authentication, token refresh, and payment flow logic so that partners can focus on their business use cases.

> **Note:** The SDK supports two integration approaches, and partners should choose based on how their ePOS application and terminal will be used.

## Integration Options

### PosLink Integration
When the ePOS application and payment terminal are on separate devices.

### All-In-One Integration
When the ePOS application and payment terminal run on the same Android device.

---

## PosLink Integration

### What Is Poslink?
PosLink is a cloud-based integration where your ePOS application communicates with a Teya payment terminal over the cloud. The SDK manages authentication using OAuth 2.0, handles token refresh automatically, and provides prebuilt payment UI screens out of the box.

### When to use Poslink?
Choose PosLink when your ePOS app runs on a tablet, PC, or Android device that is physically separate from the payment terminal. For example:

- A Windows-based POS system in a retail store that connects to a countertop terminal.
- An Android tablet POS app that pairs with a wireless Teya payment terminal.

### Key Benefits

**Managed Authentication**  
The SDK handles OAuth client authentication and token refresh automatically.

**Prebuilt Payment UI**  
Includes ready-to-use payment screens for consistent UX without extra development.

**Cross-Platform Support**  
Works on both Android and Windows, with iOS support planned.

**Minimal Setup**  
Only requires configuring the Client ID and Client Secret obtained from the Teya Developer Portal and start development.

---

## All-In-One Integration

### What is All-In-One integration?
All-In-One (AIO) integration is designed for scenarios where the ePOS application and Teya payment app run on the same Android terminal. The two applications communicate directly, while the SDK provides a consistent payment experience.

### When to use All-In-One?
Choose All-In-One when you want a single-device solution that combines the POS and payment terminal functions. For example:

- Running your ePOS app directly on a Teya Android terminal to take payments and print receipts from the same device.

### Key Benefits

**Single-Device Workflow**  
POS and payment terminal operate on the same Android device.

**Receipt Printing Support**  
Can use Sunmi or PAX printer SDKs for receipt printing.

---

## Choose Your Integration Path

Ready to get started? Select the integration approach that best fits your use case:

- **PosLink** - See poslink/ section for Android, Windows, and iOS guides
- **All-In-One** - See all-in-one/ section for Android guides
