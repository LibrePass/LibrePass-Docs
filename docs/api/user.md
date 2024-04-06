# User Endpoint

The `User` endpoint is responsible for managing user-related actions within the LibrePass application.
This includes changing email and password, setting up two-factor authentication (2FA), and deleting user accounts.

## Endpoints

### Change Email Address

Change user's email address and update ciphers due to re-encryption with the new aes key.

**Endpoint:** `PATCH /api/user/email`

**Request:**

```json
{
  "newEmail": "string",
  "oldSharedKey": "string",
  "newPublicKey": "string",
  "newSharedKey": "string",
  "ciphers": [
    {
      "id": "uuid",
      "data": "string"
    }
  ]
}
```

**Where:**

- `newEmail`: The new email address.
- `oldSharedKey`: The [shared key](../crypto/cryptography.md#user-authentication) computed using old email as salt in password hash.
- `newPublicKey`: The [public key](../crypto/cryptography.md#public-key) computed using new email address as salt in password hash.
- `newSharedKey`: The [shared key](../crypto/cryptography.md#user-authentication) computed using new email address as salt in password hash.
- `ciphers`: All user ciphers, re-encrypted with new encryption key.
    - `id`: The cipher identifier.
    - `data`: The encrypted cipher data, only "protectedData" from encrypted cipher.

**Response:** Returns a standard response indicating the success or failure of the email address change operation.

### Verify New Email Address

Verify the user's change email request using a verification code.

**Endpoint:** `GET /api/user/verifyNewEmail`

**Query Parameters:**

- `user`: User ID.
- `code`: Verification code.

**Response:** Redirects to a page with information about a correctly verified email address or returns failure of email verification.

### Change Password

Change user's password and update ciphers due to re-encryption with the new aes key.

**Endpoint:** `PATCH /api/user/password`

**Request:**

```json
{
  "oldSharedKey": "string",
  "newPublicKey": "string",
  "newSharedKey": "string",
  "newPasswordHint": "string",
  "parallelism": 3,
  "memory": 65535,
  "iterations": 4,
  "ciphers": [
    {
      "id": "uuid",
      "data": "string"
    }
  ]
}
```

**Where:**

- `oldSharedKey`: The [shared key](../crypto/cryptography.md#user-authentication) computed using old email as salt in password hash.
- `newPublicKey`: The [public key](../crypto/cryptography.md#public-key) computed using new email address as salt in password hash.
- `newSharedKey`: The [shared key](../crypto/cryptography.md#user-authentication) computed using new email address as salt in password hash.
- `newPasswordHint`: The new user's hint for password (Optional).
- `parallelism`: The argon2id parameter (default is 3)
- `memory`: The argon2id parameter (default is 64MiB)
- `iterations`: The argon2id parameter (default is 4)
- `ciphers`: All user ciphers, re-encrypted with new encryption key.
    - `id`: The cipher identifier.
    - `data`: The encrypted cipher data, only "protectedData" from encrypted cipher.

**Response:** Returns a standard response indicating the success or failure of the password change operation.

### Setup Two-Factor Authentication

Enable two-factor authentication (2FA) for a user and generate a recovery code.

**Endpoint:** `POST /api/user/setup/2fa`

**Request:**

```json
{
  "sharedKey": "string",
  "secret": "string",
  "code": "string"
}
```

**Where:**

- `sharedKey`: The [shared key](../crypto/cryptography.md#user-authentication) for password verification.
- `secret`: The secret for TOTP.
- `code`: The current TOTP code.

**Response:** Returns a response with the generated recovery code if the 2FA setup is successful.

### Delete Account

Delete a user account and associated data.

**Endpoint:** `DELETE /api/user/delete`

**Request:**

```json
{
  "sharedKey": "string",
  "code": "string"
}
```

**Where:**

- `sharedKey`: The [shared key](../crypto/cryptography.md#user-authentication) for password verification.
- `code`: The current TOTP code (Only if 2-fa is enabled).

**Response:** Returns a standard response indicating the success or failure of the account deletion.
