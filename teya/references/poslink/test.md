# Stage 3: Test

These are the test scenarios that should be covered to ensure that Certification process runs smoothly:

1. **[Mandatory]** Setup Flow
2. **[Mandatory]** Payment Flow
3. **[Mandatory]** Cancellation Flow
4. **[Optional]** Refund Flow
5. **[Optional]** Tips Flow

## Setup Flow

The installation and setup represent the merchant's first experience, so it's imperative that it occurs quickly and seamlessly.

### Test Cases: Happy Path

| Case # | Mandatory/Optional | Scenario | Actions to take | Expected Result |
|--------|-------------------|----------|-----------------|-----------------|
| 1 | **Mandatory** | Connect Teya Account to ePOS | Partner Navigates to Settings > Add Payment Method | Partner Prompted to `Connect Teya Account` |
| 2 | **Mandatory** | Teya ID Login | Partner Enters Valid Merchant Teya ID Credentials | 1. Successful login to TeyaID 2. ePOS is Authorised to Communicate to Teya Services on Merchant's Behalf |
| 3 | Optional | Show Store(s) | Partner views list of stores returned via POSLink | 1. ePOS fetches list of Stores via POSLink 2. List of Stores associated to Merchant is shown on ePOS |
| 4 | **Mandatory** | Select Store | Partner selects store to set-up | 1. ePOS obtains `store_id` for Terminal Set-up |
| 5 | Optional | Show Terminal(s) | Partner navigates to terminal setup area | 1. ePOS fetches list of Terminals via POSLink 2. List of Pre-Registered Terminals Shown to Merchant on ePOS App |
| 6 | **Mandatory** | Select Terminal(s) | Partner Selects Terminal to Pair | 1. Successful pairing between ePOS and Terminal 2. ePOS stores `terminal_id` for sending Payment Requests |
| 7 | **Mandatory** | Configure Terminal | Enable Pay at Counter Mode in Terminal features menu | 1. Terminal now in state ready to automatically pick-up payment requests |

### Test Cases: Unhappy Path

| Case # | Mandatory/Optional | Scenario | Actions to take | Expected Result | How to avoid |
|--------|-------------------|----------|-----------------|-----------------|--------------|
| 1 | **Mandatory** | Refresh token already used | 1. Do not store the new `Refresh Token` 2. Sends a new request to get the new `Refresh Token` | 1. ePOS receives a 400 error 2. ePOS Requests user to re-authenticate | Read recommendations on token refresh |

## Payment Flow

### Test Cases: Happy Path

| Case # | Mandatory/Optional | Scenario | Actions to take | Expected Result |
|--------|-------------------|----------|-----------------|-----------------|
| 1 | **Mandatory** | Send Payment Request | Partner sends payment request to POSLink | 1. Payment Request sent from ePOS App to POSLink 2. ePOS blocks further Payment Requests being sent 3. Terminal App Retrieves Payment Request from POSLink |
| 2 | **Mandatory** | Present Payment Card | Customer presents payment card | 1. POSLink updates ePOS with Payment Request state 2. ePOS reflects closed Payment Request 3. ePOS allows Partner to send another Payment Request |

### Test Cases: Unhappy Path

| Case # | Mandatory/Optional | Scenario | Actions to take | Result | How to avoid |
|--------|-------------------|----------|-----------------|--------|--------------|
| 1 | **Mandatory** | Access token expires during payment | 1. Send a Payment Request when the Access Token only has 1 minute to live 2. Wait 1 minute 3. Proceed with the payment in the terminal | 1. ePOS receives error that the Access Token is no longer valid 2. ePOS requests new Access Token in background 3. ePOS receives payment successful | Preemptive refresh before expiring and during ePOS idle time |
| 2 | **Mandatory** | Terminal doesn't receive request | 1. Turn off terminal 2. Partner sends payment request from ePOS | 1. Payment Request sent from ePOS App to POSLink 2. Error is returned | Display message to merchant to check terminal status |

## Cancellation Flow

### Test Cases: Happy Path

| Case # | Mandatory/Optional | Scenario | Actions to take | Expected Result |
|--------|-------------------|----------|-----------------|-----------------|
| 1 | Optional | Cancellation Requested from ePOS | Partner sends Cancel Request from POSLink | 1. ePOS updates Terminal that request is cancelled |
| 2 | **Mandatory** | Cancellation on Terminal | Merchant / Customer clicks 'Cancel' on Terminal | 1. POSLink updates ePOS that request is cancelled |

## Refund Flow

In case you decide to implement the Refund flow, the following test cases are mandatory:

### Test Cases: Happy Path

| Case # | Mandatory/Optional | Scenario | Actions to take | Expected Result |
|--------|-------------------|----------|-----------------|-----------------|
| 1 | **Mandatory** | Customer wants a refund | Merchant initiates refund against order on ePOS | 1. ePOS advised if success or fail |
| 2 | **Mandatory** | Customer wants receipt of refund | Merchant prints refund via ePOS | 1. Receipt printed from ePOS with refund success or fail state |

## Tips Flow

In case you decide to implement the Tips flow, the following test cases are mandatory:

### Test Cases: Happy Path

| Case # | Mandatory/Optional | Scenario | Actions to take | Expected Result |
|--------|-------------------|----------|-----------------|-----------------|
| 1 | **Mandatory** | Tip via ePOS | Send tip with payment request via ePOS | 1. Terminal shows total amount including tip |
| 2 | **Mandatory** | Tip via Terminal | Send payment request with no tip present | 1. Terminal prompts customer for tip on screen |

---

If you have any questions or need further assistance please don't hesitate to reach out to our support team by sending an email to partnersupport@teya.com.
