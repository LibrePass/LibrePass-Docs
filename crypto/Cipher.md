# Cipher Documentation

## Overview

Ciphers are encoded in json format. They are encrypted using AES GCM encryption.

### Cipher in JSON format

```json

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
```

**Where:**

- `id`: The cipher identifier.
- `owner`: The identifier of the cipher owner.
- `type`: The type of the cipher. [CipherType](#cipher-type)
- `protectedData`: The encrypted cipher data. [CipherData](#cipher-data)
- `collection`: The identifier of the collection to which the cipher belongs. (optional)
- `favorite`: Whether the cipher is marked as favorite.
- `rePrompt`: Whether the password should be re-prompted. (Only UI-related)
- `created`: The date when the cipher was created.
- `lastModified`: The date when the cipher was last modified.

### Cipher Type

Cipher type represents the type of cipher.

**Possible values:**

- `0`: Login cipher
- `1`: Secure note cipher
- `2`: Card cipher

### Cipher Data

#### Login Cipher

Cipher data for logins.

```json
{
  "name": "string",
  "username": "string",
  "email": "string",
  "password": "string",
  "passwordHistory": [
    {
      "password": "string",
      "lastUsed": "unix timestamp",
    }
  ],
  "uris": [
    "string",
  ],
  "twoFactor": "string",
  "notes": "string",
  "fields": [
    {
      "name": "string",
      "type": 0,
      "value": "string",
    }
  ]
}
```

**Where:**

- `name`: The name of the cipher.
- `username`: The login username. (optional)
- `password`: The login password. (optional)
- `email`: The login email. (optional)
- `passwordHistory`: The history of passwords. (optional)
- `uris`: The list of uris. (optional)
- `twoFactor`: The two-factor URI encoded. (optional)
- `notes`: The note for the cipher. (optional)
- `fields`: The custom fields for the cipher. (optional) [Custom Fields](#custom-fields)

#### Secure Note Cipher

Cipher data for secure notes.

```json
{
  "title": "string",
  "note": "string",
  "fields": [
    {
      "name": "string",
      "type": 0,
      "value": "string",
    }
  ]
}
```

**Where:**

- `title`: The title of the note.
- `note`: The secure note.
- `fields`: The custom fields for the cipher. (optional) [Custom Fields](#custom-fields)

#### Card Cipher

Cipher data for cards.

```json
{
  "name": "string",
  "cardholderName": "string",
  "number": "string",
  "expMonth": "09",
  "expYear": "30",
  "code": "string",
  "notes": "string",
  "fields": [
    {
      "name": "string",
      "type": 0,
      "value": "string",
    }
  ]
}
```

**Where:**

- `name`: The name of the cipher.
- `cardholderName`" The cardholder name.
- `number`" The number of the card.
- `expMonth`" The card expiration month. (optional)
- `expYear`" The card expiration year. (optional)
- `code`" The card CVV code. (optional)
- `notes`" The note for the cipher. (optional)
- `fields`: The custom fields for the cipher. (optional) [Custom Fields](#custom-fields)

### Special Fields

#### Custom Fields

```json
[
  {
    "name": "string",
    "type": 0,
    "value": "string",
  }
]
```

**Where:**

- `name`: The name of the field.
- `type`: The type of the field. [Custom Fields Types](#custom-fields-types)
- `value`: The field value.

##### Custom Fields Types

- `0`: Text
- `1`: Hidden

#### Password History

History of passwords stored in login cipher.

```json
[
  {
    "password": "string",
    "lastUsed": "unix timestamp",
  }
]
```

**Where:**

- `password`: The login password.
- `lastUsed`: The date when the password was changed.
