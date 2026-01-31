# OAuth Authentication Experience for ePOS Partners

This page explains the OAuth design for Poslink integrations. It focuses on clarity and brevity so you can quickly choose the right approach.

## Overview

Teya supports two ways to handle OAuth for ePOS integrations:

- **Use the Teya ePOS SDK** – simplest option; SDK handles all OAuth UI, token management, and refresh. You only provide an entry point such as **"Connect to Teya"**. After completion, you get tokens and proceed directly to store/terminal selection.
- **Direct REST (Poslink) integration** – you build the OAuth flow yourself using Teya's APIs. You must implement the UX, error handling, token storage, and refresh.

---

If you choose Direct REST, you must support **one** of these OAuth 2.0 flows:

### Flow 1: Device Code (QR Scan)

Best for devices without a browser or limited input.

1. Merchant taps **Connect to Teya** in your ePOS.  
2. ePOS shows a QR code + short code.  
3. Merchant scans code or visits URL on their phone.  
4. Merchant logs in with their Teya account email.  
5. Teya authorises the ePOS → your backend receives tokens.  
6. Confirmation shown: *Connected and ready*.  

---

### Flow 2: Authorisation Code with PKCE (Redirect)

Best for devices that can open a browser or webview.

1. Merchant taps **Connect to Teya** in your ePOS.  
2. ePOS opens Teya login in browser/webview.  
3. Merchant logs in with Teya account.  
4. Teya redirects back with an auth code.  
5. Your backend exchanges code → receives tokens.  
6. Confirmation shown: *Connected and ready*.  

---

## After authentication: store and terminal pairing

Once tokens are issued, merchants must select **store** and **terminal**:

1. **Get stores** → call the *Get List of Stores API*. Merchant chooses one.  
   - Example: Merchant owns 3 stores → selects *Store B*.  
2. **Get terminals** → call the *Get List of Terminals API* for the chosen store.  
   - Example: Store B has 4 terminals → selects *Terminal #3*.  
3. Pairing complete → payment requests now route to the selected terminal.  

---

## Token lifecycle & session continuity

To keep the merchant experience seamless:

- **Secure storage** → store refresh tokens in OS keychain/keystore.  
- **Proactive refresh** → refresh access tokens in background at ~70–80% of lifetime.  
- **Retry on 401** → refresh once silently; if it fails, prompt *"Session expired – reconnect to continue."*  
- **Rotation & revocation** → handle rotated refresh tokens; if revoked, route back to **Connect to Teya**.  
- **Never interrupt payments** → queue re-authentication until after a payment flow ends.  

---

## Impact if not handled

- Store/terminal lists fail to load.  
- Random logouts during checkout.  
- Failed or abandoned payments.  
- Increased merchant support contacts.  

---

## Key takeaways

- Use the **SDK** if you want OAuth handled for you.  
- Use **Direct REST** if you need full control.  
- For Direct REST, pick **one flow**:  
  - Device Code (QR) for limited-input devices.  
  - PKCE Redirect for browser-capable devices.  
- After login, always require merchants to:  
  1. Select store  
  2. Select terminal  
- Implement **robust token refresh** to avoid checkout disruption.  
- Keep error states clear and actionable.  
