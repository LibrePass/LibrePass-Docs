# Cipher Endpoint

## Cipher

The `Cipher` endpoint handles operations related to user ciphers in the LibrePass application. This includes inserting new ciphers, retrieving all ciphers, syncing ciphers, fetching a specific cipher, updating a cipher, and deleting a cipher.

### Endpoints

#### Sync Ciphers

**Endpoint:** `POST /api/cipher/sync`

**Description:** Syncing the local ciphers database with the server database based on the last synchronization timestamp.

**Request:**

```json
{
  "lastSyncTimestamp": "unix timestamp",
  "updated": [
    {
      "id": "uuid",
      "owner": "uuid",
      "type": 0,
      "protectedData": "string",
      "collection": "uuid",
      "favorite": false,
      "rePrompt": false,
      "created": "unix timestamp",
      "lastModified": "unix timestamp"
    }
  ],
  "deleted": [
    "uuid"
  ]
}
```

**Where:**

- `lastSyncTimestamp`: The unix timestamp (seconds) of the last sync.
- `updated`: The new or updated ciphers to save into the server database. (if nothing, send an empty list)
- `deleted`: The IDs with deleted ciphers to delete it from the server database. (if nothing, send an empty list)

**Response:**

```json
{
  "ids": [
    "uuid"
  ],
  "ciphers": [
    {
      "id": "uuid",
      "owner": "uuid",
      "type": 0,
      "protectedData": "string",
      "collection": "uuid",
      "favorite": false,
      "rePrompt": false,
      "created": "unix timestamp",
      "lastModified": "unix timestamp"
    }
  ]
}
```

**Where:**

- `ids`: The list that contains all IDs of ciphers owned by the user. (used for deleting ciphers from the local database)
- `cipher`: The new or updated ciphers updated in the server database since last synchronization.

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
