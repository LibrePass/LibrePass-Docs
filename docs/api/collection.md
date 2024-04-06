# Collection Endpoint

The `Collection` endpoint manages operations related to user collections in the LibrePass application.
This includes inserting new collections, retrieving all collections, fetching a specific collection,
updating a collection, and deleting a collection.

## Endpoints

### Save Collection

Update or create a new collection for the authenticated user.

**Endpoint:** `PUT /api/collection`

**Request:**

```json
{
  "id": "string",
  "name": "string"
}
```

**Where:**

- `id`: The cipher identifier.
- `name`: The name of the collection.

**Response:**

```json
{
  "id": "uuid"
}
```

### Get All Collections

Retrieve all collections for the authenticated user.

**Endpoint:** `GET /api/collection`

**Response:**

```json
[
  {
    "id": "uuid",
    "owner": "uuid",
    "name": "string",
    "created": "unix timestamp",
    "updated": "unix timestamp"
  }
]
```

### Get Collection

Retrieve a specific collection for the authenticated user.

**Endpoint:** `GET /api/collection/{id}`

**Path Parameter:**

- `{id}`: ID of the collection to retrieve.

**Response:**

```json
{
  "id": "uuid",
  "owner": "uuid",
  "name": "string",
  "created": "unix timestamp",
  "updated": "unix timestamp"
}
```

### Delete Collection

Delete a specific collection for the authenticated user.

**Endpoint:** `DELETE /api/collection/{id}`

**Path Parameter:**

- `{id}`: ID of the collection to delete.

**Response:**

```json
{
  "id": "uuid"
}
```
