# Crypto Module

The `crypto` module in Node.js is used to secure data through hashing, encryption, decryption, and random token generation.


## 1. Import Crypto

```javascript
const crypto = require('crypto');
```

## 2. Generate a Hash

Hashing converts input data into a fixed-length string.

```javascript
const crypto = require('crypto');

const password = "hello123";

const hash = crypto
    .createHash('sha256')
    .update(password)
    .digest('hex');

console.log(hash);
```

**Purpose:** Used for data integrity checks and generating data fingerprints.

## 3. Generate a Random Token

```javascript
const crypto = require('crypto');

const token = crypto.randomBytes(16).toString('hex');

console.log(token);
```

**Purpose:** Used to generate secure random tokens for:
- Password reset
- Email verification
- Session management

## 4. Where Do We Use Crypto?

- **Login:** Secure password storage and verification.
- **Forgot Password:** Generate password reset tokens.
- **Email Verification:** Generate verification tokens.
- **Payments:** Protect sensitive information.
- **Security:** Encrypt and decrypt confidential data.

## 5. Hashing vs Encryption

| Hashing | Encryption |
|---|---|
| One-way process | Reversible process |
| Cannot be reversed | Can be decrypted using a key |
| Used for password verification | Used to protect sensitive data |
| Example: SHA-256 | Example: AES |

**Important:** For password storage, use password-hashing algorithms like Argon2id or scrypt instead of plain SHA-256.

## Conclusion

The Node.js `crypto` module is used to improve application security and protect sensitive information.