# LibrePass User Endpoint Documentation

## User

The `User` endpoint is responsible for managing user-related actions within the LibrePass application. This includes changing email and password, setting up two-factor authentication (2FA), and deleting user accounts.

### Endpoints

#### 1. Change Email Address

**Endpoint:** `PATCH /api/user/email`

**Description:** Allows a user to change their email address and update related information.

**Request:**

```jsonc
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

**Response:** Returns a standard response indicating the success or failure of the email address change operation.

#### 2. Verify New Email Address

**Endpoint:** `GET /api/user/verifyNewEmail`

**Description:** Verifies the user's change email request using a verification code.

**Query Parameters:**

- `user`: User ID.
- `code`: Verification code.

**Response:** Redirects to a page with information about a correctly verified email address or returns failure of email verification.

#### 3. Change Password

**Endpoint:** `PATCH /api/user/password`

**Description:** Allows a user to change their password and update related information.

**Request:**

```jsonc
{
  "oldSharedKey": "string",
  "newPublicKey": "string",
  "newSharedKey": "string",
  "newPasswordHint": "string",
  "parallelism": 3, // Argon2ID parameter (default is 3)
  "memory": 65535, // Argon2ID parameter (default is 64MiB)
  "iterations": 4, // Argon2ID parameter (default is 4)
  "ciphers": [
    {
      "id": "uuid",
      "data": "string"
    }
  ]
}
```

**Response:** Returns a standard response indicating the success or failure of the password change operation.

#### 4. Setup Two-Factor Authentication

**Endpoint:** `POST /api/user/setup/2fa`

**Description:** Enables two-factor authentication (2FA) for a user and generates a recovery code.

**Request:**

```json
{
  "sharedKey": "string",
  "secret": "string",
  "code": "string"
}
```

**Response:** Returns a response with the generated recovery code if the 2FA setup is successful.

#### 5. Delete Account

**Endpoint:** `DELETE /api/user/delete`

**Description:** Deletes a user account and associated data.

**Request:**

```json
{
  "sharedKey": "string",
  "code": "string"
}
```

**Response:** Returns a standard response indicating the success or failure of the account deletion.

### Dependencies

The `User` endpoint relies on several repositories for database operations:

- `UserRepository`: Manages user data.
- `TokenRepository`: Handles user tokens.
- `CipherRepository`: Manages user ciphers.
- `CollectionRepository`: Deals with user collections.

### Important Notes

1. **Authorization:** Endpoints in this endpoint require user authorization, which is handled by the `@AuthorizedUser` annotation.

2. **Validation:** Shared key validation is performed using the `validateSharedKey` function.

3. **Two-Factor Authentication:** Two-factor authentication is implemented using TOTP (Time-based One-Time Password) codes.

4. **Error Handling:** The endpoint throws `InvalidTwoFactorCodeException` in case of an invalid 2FA code.
