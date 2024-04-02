# Cipher Endpoint

## Cipher

The `Cipher` endpoint handles operations related to user ciphers in the LibrePass application. This includes inserting new ciphers, retrieving all ciphers, syncing ciphers, fetching a specific cipher, updating a cipher, and deleting a cipher.

### Endpoints

#### Save Cipher

**Endpoint:** `PUT /api/cipher`

**Description:** Inserts or updates cipher for the authenticated user.

**Request:** The [Encrypted Cipher](../crypto/cipher.md#encrypted-cipher-in-json-format).

**Response:** Returns the ID of the cipher.

#### Insert Cipher

!!!warning
    Deprecated, use [save](#save-cipher) instead


**Endpoint:** `PUT /api/cipher`

**Description:** Inserts a new cipher for the authenticated user.

**Request:** The [Encrypted Cipher](../crypto/cipher.md#encrypted-cipher-in-json-format).

**Response:** Returns the ID of the newly created cipher.

#### Get All Ciphers

**Endpoint:** `GET /api/cipher`

**Description:** Retrieves all ciphers for the authenticated user.

**Response:** Returns an array of encrypted ciphers.

#### Sync Ciphers

**Endpoint:** `GET /api/cipher/sync`

**Description:** Syncs ciphers based on the last synchronization timestamp.

**Query Parameters:**

- `lastSync`: Unix timestamp of the last synchronization.

**Response:** Returns a `SyncResponse` object containing updated cipher IDs and encrypted ciphers.

#### Get Cipher

**Endpoint:** `GET /api/cipher/{id}`

**Description:** Retrieves a specific cipher for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the cipher to retrieve.

**Response:** Returns the [Encrypted Cipher](../crypto/cipher.md#encrypted-cipher-in-json-format).

#### Update Cipher

!!!warning
    Deprecated, use [save](#save-cipher) instead


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

#### Delete Cipher

**Endpoint:** `DELETE /api/cipher/{id}`

**Description:** Deletes a specific cipher for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the cipher to delete.

**Response:** Returns the ID of the deleted cipher.

#### Get Website Icon

**Endpoint:** `GET /api/cipher/icon`

**Description:** Retrieves the website icon for a given domain.

**Query Parameter:**

- `domain`: Domain for which to fetch the icon.

**Response:** Returns the website icon in PNG format or a "Not Found" response if the icon is not available.

### Important Notes

- **Cipher Size Limit:** The maximum allowed length for cipher data is specified in the server configuration by the `cipherMaxLength` value.
- **Sync Timestamp:** The synchronization timestamp is used to retrieve updated ciphers since the last synchronization.
- **Icon Retrieval:** The `/api/cipher/icon` endpoint retrieves a website's icon using the Google API. If unsuccessful, it returns a "Not Found" response.
