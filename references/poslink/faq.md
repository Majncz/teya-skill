# POSLink Frequently Asked Questions

## Authentication & Credentials

### Do I need a different `Client ID` and `Client Secret` for each merchant?
No, each integrating partner only needs one `Client ID` and `Client Secret` to be used by the application. **The merchant should never have access to this information.** For authentication, merchants will use their own Teya IDs.

### What is Teya ID?
The Teya ID is the user's account used for authentication within the Teya Ecosystem. It should not be confused with the Client ID and Client Secret generated in the developer portal. A user can create their Teya ID at [id.teya.com/authn/registration/email-password](https://id.teya.com/authn/registration/email-password).

### When we create authorization URL for merchant to authorize, how does Teya system differentiate which merchant is it?
The merchant authenticates using their Teya ID when they sign up to their first Teya product.

### How can we ensure that merchants will not see other merchants' stores?
Merchants can only view the stores that are associated with their Teya ID.

## Token Management

### When we perform the refresh of a token is the `Refresh Token` duration also refreshed or is it always 30 days since authentication?
The `Refresh Token` is also refreshed.

### What happens when merchant authenticates from multiple stores at the same time, are all tokens valid?
- The accesses are at a company level, so if these stores are grouped together under one company it would be one Teya ID token, else multiple.
- In the same browser, the first authentication will create an SSO session, and the app will get a token. When the other apps authenticate, they will use the same SSO session, but will each still receive a different token.
- At different browser sessions, the tokens work independently, the activity in one shouldn't affect the other for token/sessions.

### When a merchant calls the oauth-token endpoint will the previous token expire?
A new token will be issued. The others remain valid, since our token invalidation function is not yet live.

### What is `expires_in` value in oauth-token response?
The `expires_in` is the duration of the Access Token and the value is displayed in `seconds`.

### The `Access Token` lasts for 15 minutes. If I call an endpoint with that token after 10 minutes, does the token now last for another 15 minutes?
Only the remaining 5 minutes. Activity does not extend the token lifetime.

### Is it possible to perform authentication on behalf of the merchant?
The merchant can add whoever they want through the Business Portal, and then this person would have the power to authorise on their behalf.

## Technical Implementation

### Which encoding should we use for code_verifier in PKCE?
Either UTF8 or ASCII can be used, but please make sure the code verifier doesn't have any non-ASCII characters.

### Is there any way to test authentication without registering a merchant first?
In order to login with a given user (email and password), this user has to be registered first. The partner can use the self-registration form to register.

## Troubleshooting

### I have selected to pay on the ePOS, but the terminal didn't prompt for payment
The most common reasons are:
1. Terminal is not configured correctly (Enable `Pay at Counter` mode in the feature menu).
2. Check Network Connection (terminal needs to be connected to internet to communicate with POSLink).
3. ePOS authentication has timed out or had an issue, merchant needs to log out and back into their Teya ID account.

### Why can't I see a transaction in the ePOS?
If the original transaction was started on terminal, the ePOS won't know about it.

### Payment was successful/declined in the Terminal, but in the ePOS still says it's In Progress?
1. Check network connection of ePOS and Terminal
   - Terminal could lose connection after successful communication with acquiring gateway but before it sends update to POSLink.
   - If terminal states success/decline, this is the true indicator as to whether customer has been charged or not.
2. If network connection is slow, it can take longer for status to reach ePOS via POSLink.
