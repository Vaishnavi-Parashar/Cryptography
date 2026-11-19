# Experiment: Development of a Secure Text Messaging Application Using AES and SHA-256

## 1. Aim

To create a Python-based program that protects text messages through AES encryption and uses SHA-256 hashing to check whether the original data remains unchanged after decryption.

## 2. Introduction

Cryptography provides different methods for protecting digital information against unauthorized access and modification. Two commonly used techniques are encryption and hashing.

Encryption transforms an understandable message, called plaintext, into an unreadable form known as ciphertext. Hashing, on the other hand, produces a fixed-length digital fingerprint that can be used to check data integrity.

In this practical, a Python application is developed to combine AES-based encryption with SHA-256 hashing. The program accepts a message from the user, encrypts it, retrieves the original content through decryption, and compares the hash values to verify that the data has not been changed.

## 3. Technologies Used

- Programming Language: Python
- Development Environment: Visual Studio Code
- Required Library: Cryptography
- Encryption Technique: AES
- Hashing Technique: SHA-256

## 4. Software Requirements

- Python 3.x
- Visual Studio Code
- Python Cryptography Library

## 5. Library Installation

Before executing the program, install the required cryptographic package through the terminal using:

```bash
pip install cryptography
```

This package provides the necessary functions for generating encryption keys and performing authenticated encryption and decryption.

## 6. Implementation

### Step 1: Import the Required Modules

Start by importing the Python modules needed for hashing and encryption.

```python
import hashlib
from cryptography.fernet import Fernet
```

Here, `hashlib` is responsible for generating SHA-256 digests, while `Fernet` provides the encryption and decryption functionality.

### Step 2: Create an Encryption Key

Generate a secure encryption key and initialize the Fernet object.

```python
key = Fernet.generate_key()
cipher = Fernet(key)
```

The generated key is used by the application for both encryption and decryption operations.

### Step 3: Calculate the Original Message Hash

Generate the SHA-256 digest of the message entered by the user.

```python
hash_value = hashlib.sha256(message.encode()).hexdigest()
```

The input message is first converted into bytes, after which SHA-256 produces a 256-bit digest represented by 64 hexadecimal characters.

### Step 4: Encrypt the Input Message

Apply the Fernet encryption mechanism to convert the readable message into ciphertext.

```python
encrypted = cipher.encrypt(message.encode())
```

The encryption process internally uses AES-128-CBC along with HMAC-SHA256 authentication to protect the encrypted information.

### Step 5: Decrypt the Encrypted Data

Recover the original message by applying the decryption operation with the same encryption key.

```python
decrypted = cipher.decrypt(encrypted).decode()
```

The encrypted bytes are converted back into readable text after successful decryption.

### Step 6: Verify the Message Using SHA-256

Calculate another hash from the decrypted message and compare it with the previously generated hash.

```python
new_hash = hashlib.sha256(decrypted.encode()).hexdigest()

if hash_value == new_hash:
    print("Hash Verified Successfully!")
else:
    print("Hash Verification Failed!")
```

If both digest values are identical, it indicates that the decrypted message matches the original message.

## 7. Sample Output

The following output illustrates how the application behaves during execution:

```text
Enter your message: Hello Yogendra

Original Message: Hello Yogendra

SHA-256 Hash:
[64-character hexadecimal hash]

Encrypted Message:
[gAAAAAB... encrypted text]

Decrypted Message: Hello Yogendra

Hash Verified Successfully!
```

**Note:** The encryption key, hash digest, and ciphertext are generated dynamically. Therefore, their actual values may differ every time the program is executed.

## 8. Working Procedure

The complete application follows the sequence given below:

1. The program accepts a message from the user through keyboard input.
2. SHA-256 is applied to the original message to generate its initial hash.
3. A new encryption key is created using the Fernet library.
4. The plaintext is converted into ciphertext through AES-based encryption.
5. The ciphertext is decrypted using the same generated key.
6. The recovered message is passed through SHA-256 again.
7. The newly calculated digest is compared with the original hash.
8. If both values match, the application displays a successful verification message.

## 9. Algorithms and Their Functions

The application combines the following cryptographic techniques:

| Algorithm / Technique | Application |
|---|---|
| AES-128-CBC | Performs message encryption and decryption |
| SHA-256 | Produces a fixed 256-bit message digest |
| HMAC-SHA256 | Provides authentication and integrity protection for encrypted data |
| Fernet | Implements authenticated symmetric encryption |

## 10. Results and Observations

The following observations were obtained after executing the Python application:

1. An encryption key was successfully generated using the Fernet library.
2. The user-provided text was converted into encrypted ciphertext.
3. SHA-256 successfully generated the hash of the original message.
4. The encrypted information was successfully converted back into readable text.
5. A second hash was calculated using the decrypted message.
6. Both hash values matched, resulting in successful integrity verification.

## 11. Conclusion

This practical demonstrated the development of a secure text messaging application using Python and cryptographic libraries. AES-based encryption was used to protect the message, while SHA-256 hashing helped compare the original and recovered information.

The application successfully completed encryption, decryption, and hash comparison. It demonstrated how encryption and hashing can work together to protect confidential information and identify changes in message content.

---

**Experiment Topic:** Secure Text Message Encryption and Hash Verification  
**Subject:** Cryptography and Network Security  
**Programming Language:** Python  
**Development Environment:** Visual Studio Code  
**Encryption Technique:** AES (Fernet)  
**Hashing Algorithm:** SHA-256