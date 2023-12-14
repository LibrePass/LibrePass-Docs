# LibrePass Auth Endpoint Documentation

## Auth

The `Auth` endpoint is designed to handle user authentication-related actions for the LibrePass application. This includes user registration, login, two-factor authentication, password hint requests, email verification, and other related functionalities.

### Endpoints

#### 1. Register

**Endpoint:** `POST /api/auth/register`

**Description:** Allows users to register with the application, generating a verification token for email verification.

**Request:**

```jsonc 
{
  "email": "string",
  "passwordHint": "string",
  "sharedKey": "string",
  "publicKey": "string",
  "parallelism": 3, // Argon2ID parameter (default is 3)
  "memory": 65535, // Argon2ID parameter (default is 64MiB)
  "iterations": 4 // Argon2ID parameter (default is 4)
}
```

**Response:** Returns a standard response indicating the success or failure of the registration process.

#### 2. Pre-Login

**Endpoint:** `GET /api/auth/preLogin`

**Description:** Retrieves pre-login information, including default Argon2id parameters and the server's Curve25519 public key.

**Query Parameters:**

- `email` (optional): User's email for retrieving user-specific parameters.

**Response:** Returns pre-login information based on the provided email or defaults if no email is specified.

#### 3. OAuth

**Endpoint:** `POST /api/auth/oauth`

**Description:** Handles OAuth-based authentication, including login and two-factor authentication.

**Query Parameters:**

- `grantType`: Specifies the OAuth grant type (`login` or `2fa`).
  
**Request:**

```jsonc
// For login grant type
{
  "email": "string",
  "sharedKey": "string"
}

// For 2fa grant type
{
  "apiKey": "string",
  "code": "string"
}
```

**Response:** Returns a standard response indicating the success or failure of the OAuth authentication process.

#### 4. Password Hint

**Endpoint:** `GET /api/auth/passwordHint`

**Description:** Sends a password hint to the user based on their email.

**Query Parameters:**

- `email`: User's email.

**Response:** Returns a standard response indicating the success or failure of sending the password hint.

#### 5. Verify Email

**Endpoint:** `GET /api/auth/verifyEmail`

**Description:** Verifies the user's email using a verification code.

**Query Parameters:**

- `user`: User ID.
- `code`: Verification code.

**Response:** Returns a standard response indicating the success or failure of email verification.

#### 6. Resend Verification Email

**Endpoint:** `GET /api/auth/resendVerificationEmail`

**Description:** Resends the email verification code to the user.

**Query Parameters:**

- `email`: User's email.

**Response:** Returns a standard response indicating the success or failure of resending the verification email.

### Dependencies

The `Auth` endpoint relies on the following repositories and services for database operations and email communication:

- `UserRepository`: Manages user data.
- `TokenRepository`: Handles user tokens.
- `EmailService`: Manages email-related functionalities.

### Configuration

The endpoint uses rate limiting to prevent abuse. The rate limits can be configured using the `AuthControllerRateLimitConfig` and `AuthControllerEmailRateLimitConfig` classes.

### Important Notes

1. **Server Key Pair:** The server's key pair (Curve25519) is dynamically generated at startup for authentication using a shared key.

2. **Email Verification:** Email verification is optional and can be configured through the application properties.

3. **Rate Limiting:** The endpoint implements rate limiting to protect against abuse.

4. **OAuth Authentication:** OAuth-based authentication is supported for login and two-factor authentication.
