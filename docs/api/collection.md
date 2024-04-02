# Collection Endpoint

## Collection

The `Collection` endpoint manages operations related to user collections in the LibrePass application. This includes inserting new collections, retrieving all collections, fetching a specific collection, updating a collection, and deleting a collection.

### Endpoints

#### Save Collection

**Endpoint:** `PUT /api/collection`

**Description:** Updates or creates a new collection for the authenticated user.

**Request:**

```json
{
  "id": "string",
  "name": "string"
}
```

**Where:**

- `id`: The cipher identifier (UUID).
- `name`: The name of the collection.

**Response:** Returns the ID of the newly created collection.

#### Get All Collections

**Endpoint:** `GET /api/collection`

**Description:** Retrieves all collections for the authenticated user.

**Response:** Returns an array of `CipherCollection` objects containing collection details.

#### Get Collection

**Endpoint:** `GET /api/collection/{id}`

**Description:** Retrieves a specific collection for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the collection to retrieve.

**Response:** Returns the details of the specified collection in the form of a `CipherCollection` object.

#### Delete Collection

**Endpoint:** `DELETE /api/collection/{id}`

**Description:** Deletes a specific collection for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the collection to delete.

**Response:** Returns the ID of the deleted collection.
