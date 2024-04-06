# Cipher Endpoint

The `Cipher` endpoint handles operations related to user ciphers in the LibrePass application.
This includes inserting new ciphers, retrieving all ciphers, syncing ciphers,
fetching a specific cipher, updating a cipher, and deleting a cipher.

## Endpoints

### Sync Ciphers

Synchronize the local ciphers database with the server database.

**Endpoint:** `POST /api/cipher/sync`

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

- `lastSyncTimestamp`: The unix timestamp (seconds) of the last synchronization (time of last successful synchronization)
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

### Get Website Icon

Retrieve website icon for a given domain. Currently, uses Google API for retrieving icons.

**Endpoint:** `GET /api/cipher/icon`

**Query Parameter:**

- `domain`: Domain for which to fetch the icon.

**Response:** Returns the website icon in PNG format or a "Not Found" response if the icon is not available.

## Important Notes

- **Rate Limiting:** The endpoint is protected by rate limits.
