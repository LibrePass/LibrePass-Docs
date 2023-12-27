# LibrePass Cryptography Documentation

![Cryptography diagram](/diagrams/cryptography.drawio.svg)

## Cryptography Overview

LibrePass employs a robust cryptographic framework to ensure the security and privacy of user data. This documentation outlines the key cryptographic mechanisms used in the project, including password hashing, key pair generation, data encryption, and decryption.

### 1. Password Hashing

LibrePass utilizes the Argon2id hashing algorithm to securely hash user passwords. The parameters for Argon2id, such as parallelism, memory, and iterations, can be customized during user registration.

### 2. Key Pair Generation

#### 2.1 Private Key Generation

The hashed password becomes the user's private key.

#### 2.2 Public Key Generation

The public key is derived using the X25519 elliptic curve Diffie-Hellman (ECDH) key exchange algorithm. The user's private key (hashed password) is used to generate the corresponding public key.

### 3. Encryption Key Derivation

The encryption key used for securing user data is derived from the X25519 shared secret. The shared secret is computed using the private and public user's key pair.

### 4. Data Encryption

The data is encrypted using the derived encryption key and the AES-GCM (Advanced Encryption Standard - Galois/Counter Mode) symmetric encryption algorithm. This ensures the confidentiality and integrity of the stored information.

## Dependencies

The cryptographic operations within LibrePass rely on the following algorithms:

- Argon2id: Used for password hashing.
- X25519: Employed in key pair generation and shared secret computation.
- AES-GCM: Used for data encrypting.
