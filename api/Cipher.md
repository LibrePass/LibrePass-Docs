# LibrePass Cipher Endpoint Documentation

## Cipher

The `Cipher` endpoint handles operations related to user ciphers in the LibrePass application. This includes inserting new ciphers, retrieving all ciphers, syncing ciphers, fetching a specific cipher, updating a cipher, and deleting a cipher.

### Endpoints

#### 1. Save Cipher

**Endpoint:** `PUT /api/cipher`

**Description:** Inserts or updates cipher for the authenticated user.

**Request:**

```json
{
  "protectedData": "string",
  "owner": "string"
}
```

**Response:** Returns the ID of the cipher.

#### 2. Insert Cipher

> [!WARNING]
> Deprecated, use [save](#1-save-cipher) instead

**Endpoint:** `PUT /api/cipher`

**Description:** Inserts a new cipher for the authenticated user.

**Request:**

```json
{
  "protectedData": "string",
  "owner": "string"
}
```

**Response:** Returns the ID of the newly created cipher.

#### 3. Get All Ciphers

**Endpoint:** `GET /api/cipher`

**Description:** Retrieves all ciphers for the authenticated user.

**Response:** Returns an array of encrypted ciphers.

#### 4. Sync Ciphers

**Endpoint:** `GET /api/cipher/sync`

**Description:** Syncs ciphers based on the last synchronization timestamp.

**Query Parameters:**

- `lastSync`: Unix timestamp of the last synchronization.

**Response:** Returns a `SyncResponse` object containing updated cipher IDs and encrypted ciphers.

#### 5. Get Cipher

**Endpoint:** `GET /api/cipher/{id}`

**Description:** Retrieves a specific cipher for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the cipher to retrieve.

**Response:** Returns the encrypted details of the specified cipher.

#### 6. Update Cipher

> [!WARNING]
> Deprecated, use [save](#1-save-cipher) instead

**Endpoint:** `PATCH /api/cipher/{id}`

**Description:** Updates an existing cipher for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the cipher to update.

**Request:**

```json
{
  "protectedData": "string"
}
```

**Response:** Returns the ID of the updated cipher.

#### 7. Delete Cipher

**Endpoint:** `DELETE /api/cipher/{id}`

**Description:** Deletes a specific cipher for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the cipher to delete.

**Response:** Returns the ID of the deleted cipher.

#### 8. Get Website Icon

**Endpoint:** `GET /api/cipher/icon`

**Description:** Retrieves the website icon for a given domain.

**Query Parameter:**

- `domain`: Domain for which to fetch the icon.

**Response:** Returns the website icon in PNG format or a "Not Found" response if the icon is not available.

### Dependencies

The `Cipher` endpoint relies on the following repository for database operations:

- `CipherRepository`: Manages user ciphers.

### Important Notes

1. **Validation:** Hexadecimal validation is performed using the `Validator.hexValidator` function.

2. **Cipher Size Limit:** The maximum allowed length for cipher data is specified by the `cipherMaxLength` configuration.

3. **Sync Timestamp:** The synchronization timestamp is used to retrieve updated ciphers since the last synchronization.

4. **Icon Retrieval:** The `getWebsiteIcon` endpoint retrieves a website's icon using the Google API. If unsuccessful, it returns a "Not Found" response.
