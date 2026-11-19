# Experiment–9: Implementation of Password Hashing With and Without Salting Using Python

## 1. Aim

To implement password hashing techniques with and without salting in Python and compare their effectiveness against common security threats, including dictionary attacks, brute-force attacks, and rainbow table attacks.

## 2. Introduction

Password hashing is a security mechanism that converts a user's password into a fixed-length hash value. Instead of storing passwords in their original form, systems store their corresponding hash values.

Salting adds an extra layer of protection by combining a randomly generated value with the password before hashing. As a result, even identical passwords produce different hash values when different salts are used.

In this experiment, both salted and unsalted password hashing methods are implemented in Python to understand their security differences.

## 3. Technologies Used

- Programming Language: Python
- IDE: Visual Studio Code
- Hashing Algorithm: SHA-256
- Password Hashing Algorithm: PBKDF2-HMAC-SHA256
- Python Modules: `hashlib`, `secrets`, `hmac`

## 4. Software Requirements

- Python 3.x
- Visual Studio Code

## 5. Concepts Used

### A. Password Hashing Without Salting

In this approach, the password is directly processed using the SHA-256 hashing algorithm to generate a fixed-length hash value.

**Key Features:**
- Uses the SHA-256 algorithm to generate hashes.
- Identical passwords always produce identical hash values.
- Susceptible to precomputed rainbow table attacks.
- Its fast execution makes repeated password guessing easier.

### B. Password Hashing With Salting

In this approach, a randomly generated salt is combined with the password before applying PBKDF2-HMAC-SHA256.

**Key Features:**
- Generates a random 16-byte salt for each password.
- Produces different hash values for identical passwords when different salts are used.
- Provides protection against precomputed rainbow table attacks.
- PBKDF2 increases the time and computational effort required for password guessing.

## 6. Implementation

### Step 1: Import the Necessary Modules

```python
import hashlib
import secrets
import hmac
```

### Step 2: Generate Hash Without Salt

```python
def hash_without_salt(password):
    return hashlib.sha256(password.encode()).hexdigest()
```

### Step 3: Generate Hash With Salt

```python
def hash_with_salt(password):
    salt = secrets.token_bytes(16)

    hashed = hashlib.pbkdf2_hmac(
        'sha256',
        password.encode(),
        salt,
        100000
    )

    return salt, hashed
```

### Step 4: Verify the Entered Password

```python
def verify_password(password, salt, stored_hash):
    new_hash = hashlib.pbkdf2_hmac(
        'sha256',
        password.encode(),
        salt,
        100000
    )

    return hmac.compare_digest(new_hash, stored_hash)
```

### Step 5: Demonstrate a Dictionary Attack

A predefined collection of commonly used passwords is used to demonstrate how an attacker can compare password guesses with an unsalted SHA-256 hash and identify a matching password.

## 7. Sample Output

**Input:**

```text
Enter your password: 1020abc
```

### A. Hashing Without Salt

```text
--- WITHOUT SALT ---

Hash 1: d1420181360fd1a7e8a407c7bf47586ed99eba817bad573c39e94c26af2b785a

Hash 2: d1420181360fd1a7e8a407c7bf47586ed99eba817bad573c39e94c26af2b785a

Same Hash: True
```

### B. Hashing With Salt

```text
--- WITH SALT ---

Salt 1: 13f9c4df52129c9ac291a54fef3fd208

Hash 1: 1bd87225d9acc3f2995c81eb4ae51bc779b4e0517d90a4a00166470d3c8d389e

Salt 2: 1681dae98c9aa3b405d32080ab649193

Hash 2: be89e2c9dde256ea5b09a1ca66b4265fb43f154cd774c04903ee83be4f06d75f

Same Hash: False
```

### C. Password Verification

```text
--- PASSWORD VERIFICATION ---

Re-enter your password: 1020aaa

Incorrect Password!
```

The system rejected the entered password because it was different from the original password.

### D. Dictionary Attack Demonstration

```text
--- DICTIONARY ATTACK DEMO ---

Password found: password
```

The dictionary attack successfully identified the common password `password` by matching its unsalted hash against the predefined password list.

## 8. Comparison Between Hashing Techniques

| Feature | Without Salt | With Salt |
|---|---|---|
| Algorithm | SHA-256 | PBKDF2-SHA256 |
| Random Salt | Not Used | Used |
| Identical Passwords | Same Hash | Different Hashes |
| Rainbow Table Protection | Low | High |
| Dictionary Attack Protection | Low | Improved |
| Brute-force Protection | Low | Improved |

## 9. Evaluation Against Common Password Attacks

**1. Dictionary Attack:**

In an unsalted hashing system, attackers can compare common password guesses with previously calculated hash values. Salting prevents direct reuse of precomputed hash tables, although weak passwords can still be guessed.

**2. Brute-force Attack:**

In this attack, an attacker repeatedly tries different password combinations until the correct one is found. PBKDF2 makes every guessing attempt more computationally expensive, slowing down the attack.

**3. Rainbow Table Attack:**

Rainbow tables contain precomputed password and hash combinations. Since salting produces different hashes for identical passwords, these precomputed tables become impractical to reuse.

## 10. Results and Observations

1. SHA-256 generated identical hash values when the same password was entered without salting.
2. Different random salts produced different hash values for the same password.
3. Password verification correctly identified an incorrect password.
4. The dictionary attack successfully detected the common password `password`.
5. PBKDF2 combined with random salting offered better protection against common password attacks than direct SHA-256 hashing.

## 11. Conclusion

In this experiment, password hashing was successfully implemented in Python using both salted and unsalted techniques. The results showed that unsalted SHA-256 generates identical hash values for identical passwords, whereas salted hashing produces different values by using randomly generated salts.

The implementation also demonstrated how PBKDF2 increases the computational effort required for password guessing and how random salting helps prevent the reuse of precomputed rainbow tables.

---

**Experiment Number:** 09  
**Subject:** Cryptography and Network Security  
**Programming Language:** Python  
**IDE:** Visual Studio Code  
**Hashing Algorithms:** SHA-256 and PBKDF2-HMAC-SHA256