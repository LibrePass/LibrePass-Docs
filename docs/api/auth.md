# Auth Endpoint

## Auth

The `Auth` endpoint is designed to handle user authentication-related actions for the LibrePass application. This includes user registration, login, two-factor authentication, password hint requests, email verification, and other related functionalities.

### Endpoints

#### Register

**Endpoint:** `POST /api/auth/register`

**Description:** Allows users to register with the application, generating a verification token for email verification.

**Request:**

```json
{
  "email": "string",
  "passwordHint": "string",
  "publicKey": "string",
  "sharedKey": "string",
  "parallelism": 3,
  "memory": 65535,
  "iterations": 4
}
```

**Where:**

- `email`: The user's email address.
- `passwordHint`: The user's password hint (optional).
- `publicKey`: The user's public key (x25519 public key). More information about a public key you can read [here](../crypto/cryptography.md#public-key).
- `sharedKey`: The shared key (x25519 shared key) exchanged beetween the user and the server. More information about a shared key you can read [here](../crypto/cryptography.md#user-authentication).
- `parallelism`: The argon2id parameter (Default is 3).
- `memory`: The argon2id parameter (Default is 64MiB).
- `iterations`: The argon2id parameter (Default is 4).

**Response:** Returns a standard response indicating the success or failure of the registration process.

#### Pre-Login

**Endpoint:** `GET /api/auth/preLogin`

**Description:** Retrieves pre-login information, including Argon2id parameters and the server's Curve25519 public key.

**Query Parameters:**

- `email` (optional): User's email for retrieving user-specific parameters.

**Response:** Returns pre-login information based on the provided email or defaults if no email is specified.

#### OAuth

**Endpoint:** `POST /api/auth/oauth`

**Description:** Handles OAuth-based authentication, including login and two-factor authentication.

**Query Parameters:**

- `grantType`: Specifies the OAuth grant type (`login` or `2fa`).
  
**Request:**

```json
// For login grant type
{
  "email": "string",
  "sharedKey": "string"
}

// For 2fa grant type
{
  "apiKey": "string", // API key from "login" grant_type
  "code": "string" // 2-fa code
}
```

**Where:**

***For login grant type:***

- `email`: The user's email address.
- `sharedKey`: The shared key (x25519 shared key) exchanged between the user and the server. More information about a shared key you can read [here](../crypto/cryptography.md#user-authentication).

***For 2fa grant type:***
- `apiKey`: The API key from "login" grant type. This key will be verified after successful 2fa code verification.
- `code`: The current one-time password.

**Response:** Returns a standard response indicating the success or failure of the OAuth authentication process.

#### Password Hint

**Endpoint:** `GET /api/auth/passwordHint`

**Description:** Sends a password hint to the user based on their email.

**Query Parameters:**

- `email`: User's email.

**Response:** Returns a standard response indicating the success or failure of sending the password hint.

#### Verify Email

**Endpoint:** `GET /api/auth/verifyEmail`

**Description:** Verifies the user's email using a verification code. This link is included in verification email.

**Query Parameters:**

- `user`: User ID.
- `code`: Verification code.

**Response:** Redirects to a page with information about a correctly verified email address or returns failure of email verification.

#### Resend Verification Email

**Endpoint:** `GET /api/auth/resendVerificationEmail`

**Description:** Resends the email verification code to the user.

**Query Parameters:**

- `email`: User's email.

**Response:** Returns a standard response indicating the success or failure of resending the verification email.

### Important Notes

- **Rate Limiting:** The endpoint is protected by rate limits.
