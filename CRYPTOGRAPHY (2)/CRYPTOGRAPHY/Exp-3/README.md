# Experiment: Implementation and Comparison of DES and AES Encryption

## 1. Aim

To implement DES (Data Encryption Standard) and AES (Advanced Encryption Standard) for encrypting sample data and examine the differences between them in terms of security, working principles, and performance.

## 2. Introduction

Cryptography plays an important role in securing digital information from unauthorized users. Encryption is one of its major techniques, in which original readable information, known as plaintext, is converted into an unreadable form called ciphertext using a secret key and an encryption algorithm.

This experiment focuses on two symmetric encryption techniques:

- **DES (Data Encryption Standard):** A traditional block encryption technique that works with a 64-bit block and has an effective key length of 56 bits.
- **AES (Advanced Encryption Standard):** A modern encryption technique that supports three different key lengths: 128, 192, and 256 bits.

Both algorithms are applied to identical input data to understand their functionality and compare their security strengths.

## 3. Software and Hardware Requirements

- CrypTool 2
- Windows Operating System
- Fundamental understanding of Cryptography and Network Security

## 4. Encryption Algorithms

### A. DES (Data Encryption Standard)

DES is a symmetric encryption algorithm that processes information in fixed blocks of 64 bits. It follows a Feistel-based design and performs multiple rounds of transformation to produce encrypted output.

**Main Characteristics:**

- Block Length: 64 bits
- Effective Key Length: 56 bits
- Design Structure: Feistel Network
- Total Encryption Rounds: 16
- The same secret key is used for both encryption and decryption.

**Configuration Details:**

| Parameter | Selected Value |
|---|---|
| Input Text | Yogendra |
| Secret Key | 12345678 |
| Encryption Algorithm | DES |
| Operation | Encrypt |
| Block Mode | ECB |
| Padding Method | Zeros |
| Result Format | Hexadecimal |

**Generated Ciphertext:**

```text
87 B8 F1 3E 0A A3 26 4E
```

### B. AES (Advanced Encryption Standard)

AES is a modern symmetric block encryption algorithm developed to provide a higher level of security. It uses a substitution-permutation structure and supports different key lengths depending on the required security level.

**Main Characteristics:**

- Block Length: 128 bits
- Supported Key Lengths: 128, 192, and 256 bits
- Design Structure: Substitution-Permutation Network
- Number of Rounds:
  - AES-128: 10 rounds
  - AES-192: 12 rounds
  - AES-256: 14 rounds

**Configuration Details:**

| Parameter | Selected Value |
|---|---|
| Input Text | Yogendra |
| Encryption Algorithm | AES |
| Operation | Encrypt |
| Key Length | 256 bits |
| Block Mode | ECB |
| Padding Method | Zeros |
| Result Format | Hexadecimal |

**Key Requirement:** For AES-256 encryption, the secret key must contain exactly 32 bytes. A valid 32-byte key must be provided before executing the encryption process.

## 5. Implementation Steps

### A. Performing DES Encryption

1. Start the CrypTool 2 application and create a new workspace.
2. Insert a Text Input component and provide `Yogendra` as the input.
3. Attach a String Decoder to convert the entered text into the required data format.
4. Place another Text Input component to specify the encryption key.
5. Enter `12345678` as the DES secret key.
6. Connect the key input to a separate String Decoder.
7. Add the DES encryption component to the workspace.
8. Set its operation to Encrypt.
9. Choose ECB as the chaining mode and Zeros as the padding method.
10. Link the decoded plaintext and secret key to the DES component.
11. Connect the encrypted result to a String Encoder.
12. Set the encoder's output representation to Hexadecimal.
13. Finally, connect it to Text Output to display the encrypted data.

### B. Performing AES Encryption

1. Launch CrypTool 2 and open a new project.
2. Add a Text Input component and enter the sample text `Yogendra`.
3. Connect the input to a String Decoder.
4. Insert another Text Input component for entering the AES key.
5. Provide a valid 32-byte secret key for the AES-256 configuration.
6. Attach a String Decoder to the key input.
7. Add the AES encryption component to the workspace.
8. Choose AES as the encryption algorithm and select the Encrypt operation.
9. Set the key length to 256 bits.
10. Configure ECB mode with Zero padding.
11. Connect the plaintext and key inputs to their respective AES component ports.
12. Attach a String Encoder to the encrypted output.
13. Choose Hexadecimal as the output representation.
14. Connect the encoder to Text Output to display the final ciphertext.

## 6. Comparative Study of DES and AES

The following table highlights the major differences between the two encryption techniques.

| Parameter | DES | AES |
|---|---|---|
| Full Name | Data Encryption Standard | Advanced Encryption Standard |
| Block Length | 64 bits | 128 bits |
| Key Length | 56 effective bits | 128/192/256 bits |
| Internal Structure | Feistel Network | Substitution-Permutation Network |
| Number of Rounds | 16 | 10/12/14 |
| Security Level | Weak and outdated | Strong |
| Processing Speed | Depends on implementation | Generally efficient on modern hardware |
| Application | Older systems | Current security applications |

## 7. Security Evaluation

**DES:**

- Its limited key length makes it vulnerable to brute-force attacks.
- The 56-bit effective key provides insufficient protection against modern computing capabilities.
- It is no longer considered suitable for protecting sensitive information.
- It is primarily useful for studying traditional encryption methods.

**AES:**

- Offers multiple key lengths for different security requirements.
- Provides strong resistance against practical brute-force attacks.
- Is widely implemented in modern information security systems.
- Can securely protect confidential information when used with appropriate configurations.

## 8. Performance Evaluation

The execution efficiency of DES and AES can vary depending on the system and configuration used during encryption.

Some important factors affecting their performance include:

- Amount of data being encrypted.
- Length of the encryption key.
- Available hardware resources.
- Efficiency of the software implementation.
- Selected encryption mode.

AES is generally considered efficient on modern computing systems, especially when the processor supports dedicated AES hardware instructions. It also provides a considerably higher level of security than DES.

**Note:** The actual execution time depends on the system configuration. No fixed performance measurements are assumed in this experiment.

## 9. Experimental Observations

1. The DES algorithm successfully processes the given plaintext using the specified 8-byte secret key.
2. AES performs encryption using a valid 256-bit secret key.
3. Both encryption techniques transform the readable input into ciphertext.
4. DES operates on 64-bit blocks, while AES processes data in 128-bit blocks.
5. AES provides a much stronger level of protection because of its larger supported key sizes.
6. The experiment illustrates the difference between an older encryption standard and a modern cryptographic algorithm.

## 10. Result

DES and AES encryption were successfully studied and implemented using CrypTool 2. The sample input was used to understand the encryption process, and the two algorithms were compared based on their block sizes, key lengths, internal structures, security properties, and performance factors.

The comparison indicates that AES provides stronger security and is more appropriate for present-day encryption requirements, whereas DES is outdated because of its comparatively small effective key size.

## 11. Conclusion

Through this practical experiment, the working principles of DES and AES encryption algorithms were explored. Both techniques use secret keys to convert plaintext into ciphertext, but they differ in their internal structures, key lengths, and security capabilities.

It was observed that AES is a more reliable choice for modern data protection because it supports larger keys and offers stronger security. DES, on the other hand, is mainly useful for understanding the basics of symmetric-key encryption.

---

**Tool:** CrypTool 2  
**Subject:** Cryptography and Network Security  
**Practical Topic:** Implementation and Comparative Analysis of DES and AES