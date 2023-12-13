# LibrePass User Endpoint Documentation

## User

The `User` endpoint is responsible for managing user-related actions within the LibrePass application. This includes changing passwords, setting up two-factor authentication (2FA), and deleting user accounts.

### Endpoints

#### 1. Change Password

**Endpoint:** `PATCH /api/user/password`

**Description:** Allows a user to change their password and update related information.

**Request:**

```json
{
  "oldSharedKey": "string",
  "newPublicKey": "string",
  "newSharedKey": "string",
  "newPasswordHint": "string",
  "parallelism": 1,
  "memory": 1024,
  "iterations": 10,
  "ciphers": [
    {
      "id": 1,
      "data": "string"
    }
  ]
}
```

**Response:** Returns a standard response indicating the success or failure of the password change operation.

#### 2. Setup Two-Factor Authentication

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

#### 3. Delete Account

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
