# Experiment 13: Password Strength Auditing Using John the Ripper in Kali Linux

## 1. Aim

To examine password strength using John the Ripper in Kali Linux and assess the vulnerability of weak passwords to dictionary and brute-force attacks.

## 2. Introduction

Password auditing is a security process used to identify weak passwords that can be easily guessed or recovered through password-cracking techniques.

John the Ripper is a widely used password security auditing tool that analyzes password hashes and attempts to identify their original passwords using techniques such as dictionary attacks and brute-force attacks.

In this experiment, OpenSSL is used to generate a salted SHA-512 crypt password hash. The generated hash is then tested using John the Ripper and the RockYou wordlist to evaluate password strength.

## 3. Requirements

- Kali Linux
- John the Ripper
- OpenSSL
- RockYou password wordlist
- Linux Terminal

## 4. Theory

### A. Password Hashing

Password hashing is a process that transforms a password into a fixed-length or algorithm-dependent hash representation. It is designed to be a one-way operation, making it difficult to obtain the original password directly from its hash.

### B. Salt

A salt is a randomly generated value added to a password during the hashing process.

**Key Features:**
- Makes identical passwords produce different hashes when different salts are used.
- Prevents direct reuse of precomputed rainbow tables.
- Makes large-scale password hash comparisons more difficult.

### C. Dictionary Attack

A dictionary attack attempts to recover a password by testing words and commonly used passwords from a predefined wordlist.

If the original password is included in the wordlist, the tool may successfully identify it.

### D. Brute-Force Attack

A brute-force attack attempts different password combinations systematically until the correct password is discovered.

The time required depends on factors such as password length, character variety, search space, and the computational cost of the hashing algorithm.

## 5. Procedure

### Step 1: Create a Working Directory

Create a separate folder to store the files required for the password auditing experiment.

```bash
mkdir password_audit
cd ~/password_audit
```

### Step 2: Generate a Salted Password Hash

Use OpenSSL to generate a SHA-512 crypt password hash with a specified salt.

```bash
openssl passwd -6 -salt s1bqi password
```

The command generates a password hash containing the salt and the resulting hashed value.

### Step 3: Store the Generated Hash

Save the complete hash generated in the previous step into a file named `hashes.txt`.

```bash
echo '$6$s1bqi$GENERATED_HASH_HERE' > hashes.txt
```

Replace `GENERATED_HASH_HERE` with the complete hash produced by OpenSSL.

### Step 4: Execute a Dictionary Attack

Run John the Ripper with the RockYou wordlist to test possible passwords against the stored hash.

```bash
john --format=sha512crypt --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

John the Ripper reads the stored hash and compares it against password candidates generated from the supplied wordlist.

### Step 5: Display the Recovered Password

Use the following command to display the password recovered during the auditing process:

```bash
john --show --format=sha512crypt hashes.txt
```

If the password is successfully identified, John displays the recovered password along with the number of cracked hashes.

## 6. Types of Password Attacks

| Attack Type | Description |
|---|---|
| Dictionary Attack | Tests commonly used passwords from a predefined wordlist such as RockYou. |
| Brute-Force Attack | Attempts different possible password combinations systematically. |
| Hybrid Attack | Combines dictionary words with additional numbers, symbols, or characters. |

## 7. Observations

During the experiment, a salted SHA-512 crypt password hash was generated using OpenSSL and stored in a text file.

John the Ripper was then executed with the RockYou wordlist to perform a dictionary-based password audit.

The tool successfully identified the weak password, and the recovered result was displayed using the `--show` option.

**Observed Output:**

```text
1 password hash cracked, 0 left
```

This output indicates that the password hash was successfully cracked.

## 8. Result Analysis

The experiment demonstrated that password hashes generated from weak passwords can still be recovered through password-guessing techniques.

The following observations were made:

- Dictionary attacks can successfully identify common and predictable passwords.
- Brute-force attacks can test possible password combinations, although the time required increases with the search space.
- Longer passwords with unpredictable character combinations are more difficult to recover.
- Salting prevents direct reuse of precomputed hash tables but does not prevent password guessing.
- Computationally expensive password-hashing algorithms make repeated guessing more difficult.

## 9. Security Recommendations

- Create long passwords, preferably 12–16 characters or more.
- Avoid commonly used words, personal information, and predictable patterns.
- Use a different password for each online account.
- Use a password manager to generate and securely store strong passwords.
- Prefer secure password-hashing algorithms such as Argon2id, bcrypt, or scrypt.
- Enable multi-factor authentication (MFA) whenever available.

## 10. Conclusion

In this experiment, password auditing was successfully carried out using John the Ripper in Kali Linux. A salted SHA-512 crypt hash was generated through OpenSSL and tested against the RockYou wordlist using a dictionary attack.

The successful recovery of the weak password demonstrated that commonly used and predictable passwords remain vulnerable even when stored in hashed form.

The experiment highlighted the importance of using strong passwords, random salts, and computationally expensive password-hashing algorithms to improve credential security.