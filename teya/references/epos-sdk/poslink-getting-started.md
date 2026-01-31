# POSLink Introduction - Getting Started

PosLink is a cloud-based integration method that connects your ePOS application with Teya payment terminals. It is designed for a plug-and-play experience where the SDK handles authentication, token management, and provides a ready-to-use payment UI.

This page provides a checklist to help developers get started with PosLink integration quickly and correctly.

## Integration Checklist

### 1. Access the Teya Developer Portal

- Go to **[partner.teya.xyz](https://partner.teya.xyz)** (development environment) and create an OAuth application.
- For Unified SDK version 1, only **Device Code Flow** is supported. PKCE support will be added in a future version.
- Create a Device Code Flow application to obtain your **Client ID** and **Client Secret**.

> ⚠️ **Important:**
> - These credentials are unique per partner, not per merchant.
> - "Client" refers to the Partner ID, not the merchant ID.
> - For production, use [partner.teya.com](https://partner.teya.com) to generate production credentials.
> - Any portal with ".xyz" is directing to development environment only.

### 2. Obtain the Teya Payment App APK and Test Cards

- Contact your **Partnership Manager** to receive the Teya mock payment app APK.
- The mock app includes built-in test cards that allow you to simulate various payment scenarios.

### 3. (Optional) Request a Teya Terminal

- If you prefer, you can use the Teya app on any **Android emulator** for testing.
- Alternatively, you may request a **physical Teya terminal** from your Partnership Manager for real-device testing.

### 4. Start Development

After completing the above steps, you can begin development by integrating the SDK into your Android or Windows application using the provided guides and code samples.

## Supported Platforms

- **Android** - Native Android SDK
- **Windows** - Windows SDK for desktop POS systems
- **iOS** - Planned for future release
