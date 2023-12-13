# LibrePass Collection Endpoint Documentation

## Collection

The `Collection` endpoint manages operations related to user collections in the LibrePass application. This includes inserting new collections, retrieving all collections, fetching a specific collection, updating a collection, and deleting a collection.

### Endpoints

#### 1. Insert Collection

**Endpoint:** `PUT /api/collection`

**Description:** Inserts a new collection for the authenticated user.

**Request:**

```json
{
  "id": "string",
  "name": "string"
}
```

**Response:** Returns the ID of the newly created collection.

#### 2. Get All Collections

**Endpoint:** `GET /api/collection`

**Description:** Retrieves all collections for the authenticated user.

**Response:** Returns an array of `CipherCollection` objects containing collection details.

#### 3. Get Collection

**Endpoint:** `GET /api/collection/{id}`

**Description:** Retrieves a specific collection for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the collection to retrieve.

**Response:** Returns the details of the specified collection in the form of a `CipherCollection` object.

#### 4. Update Collection

**Endpoint:** `PATCH /api/collection/{id}`

**Description:** Updates an existing collection for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the collection to update.

**Request:**

```json
{
  "name": "string"
}
```

**Response:** Returns the ID of the updated collection.

#### 5. Delete Collection

**Endpoint:** `DELETE /api/collection/{id}`

**Description:** Deletes a specific collection for the authenticated user.

**Path Parameter:**

- `{id}`: ID of the collection to delete.

**Response:** Returns the ID of the deleted collection.

### Dependencies

The `Collection` endpoint relies on the following repository for database operations:

- `CollectionRepository`: Manages user collections.

### Important Notes

1. **Collection ID:** The collection ID is specified in the request body for inserting a collection and as a path parameter for other operations.

2. **Timestamps:** The `created` and `lastModified` timestamps provide information about the collection's creation and modification times.
