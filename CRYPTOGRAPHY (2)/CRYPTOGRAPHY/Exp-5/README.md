# Experiment 5: Implementation of SHA-256 Hashing and RSA Digital Signatures Using OpenSSL

## 1. Aim

To calculate SHA-256 message digests, generate RSA-based digital signatures, and check their validity using OpenSSL commands.

## 2. Introduction

Cryptographic techniques are widely used to protect information and ensure that data remains trustworthy during communication. Hash functions and digital signatures are two important mechanisms that help maintain the integrity and authenticity of digital information.

In this practical, OpenSSL is used to calculate the SHA-256 digest of a sample message and perform digital signature operations using RSA. The message is signed with a private key, and the generated signature is checked with its matching public key.

## 3. Software Requirements

- Operating System: Windows
- Application: OpenSSL
- Working Environment: Windows Command Prompt (CMD)
- Hash Function: SHA-256
- Signature Technique: RSA
- Key Length: 2048 bits

## 4. Theoretical Concepts

### A. SHA-256 (Secure Hash Algorithm)

SHA-256 is a cryptographic hashing technique that converts input information into a fixed-size digest of 256 bits, represented by 64 hexadecimal characters.

**Key Characteristics:**

- Generates a fixed 256-bit output regardless of the input size.
- Works as a one-way function, making it practically infeasible to recover the original input from its hash.
- Even a minor modification in the input produces a substantially different digest.
- Commonly applied to check whether information has been altered.

### B. RSA-Based Digital Signature

RSA is an asymmetric cryptographic technique that can be used to generate and validate digital signatures through a related pair of cryptographic keys.

**Key Characteristics:**

- Operates with a public key and a private key.
- The sender uses the private key to generate a digital signature.
- The receiver uses the corresponding public key to validate the signature.
- Helps establish the integrity and authenticity of a signed message.

## 5. Implementation Procedure

### Step 1: Verify OpenSSL Availability

Initially, check whether OpenSSL is properly installed and accessible through the command prompt.

Execute:

```cmd
openssl version
```

This displays the installed OpenSSL version and confirms that the command-line utility is accessible.

### Step 2: Set Up the Working Folder

Create a separate directory for storing all the files generated during the practical.

```cmd
mkdir Experiment-5
cd Experiment-5
```

All subsequent operations will be performed inside this directory.

### Step 3: Prepare the Input Message

Create a text file containing the sample information using the following command:

```cmd
echo This is my secret message 123123 > message.txt
```

To check the contents of the newly created file, execute:

```cmd
type message.txt
```

This displays the original message that will be used for hashing and digital signature generation.

### Step 4: Calculate the SHA-256 Digest

Generate the hash value of the input file using:

```cmd
openssl dgst -sha256 message.txt
```

To store the generated hash information in a separate file, use:

```cmd
openssl dgst -sha256 message.txt > hash.txt
```

**Generated Hash Value:**

```text
02e57d8a03895879292d58e7c6d787df5a67de21563a717c019d66e734bb9f71
```

The output represents the SHA-256 digest calculated from the original message.

### Step 5: Create an RSA Private Key

Generate an RSA private key with a size of 2048 bits by executing:

```cmd
openssl genrsa -out private_key.pem 2048
```

The command creates a private key and stores it in `private_key.pem`. This key will be required to sign the message.

### Step 6: Obtain the Corresponding Public Key

After generating the private key, extract its associated public key using:

```cmd
openssl rsa -in private_key.pem -pubout -out public_key.pem
```

The resulting public key is saved in `public_key.pem` and will be used later to verify the digital signature.

### Step 7: Generate the Digital Signature

Use the RSA private key along with the SHA-256 algorithm to sign the original message.

Run the following command:

```cmd
openssl dgst -sha256 -sign private_key.pem -out signature.bin message.txt
```

This operation calculates the message digest and creates its RSA digital signature using the private key. The resulting signature is stored in `signature.bin`.

### Step 8: Validate the Generated Signature

To check whether the signature belongs to the original message, execute the following verification command:

```cmd
openssl dgst -sha256 -verify public_key.pem -signature signature.bin message.txt
```

**Expected Result:**

```text
Verified OK
```

The successful verification indicates that the signature is valid for the supplied message and the corresponding public key.

### Step 9: Examine the Effect of Message Modification

To demonstrate the importance of message integrity, change the contents of the original text file.

Execute:

```cmd
echo This message has been modified. > message.txt
```

Now perform signature verification once again:

```cmd
openssl dgst -sha256 -verify public_key.pem -signature signature.bin message.txt
```

**Expected Result:**

```text
Verification failure
```

Since the message has been changed after signing, its calculated hash no longer matches the digest associated with the original signature. Consequently, the verification operation fails.

Depending on the installed OpenSSL version, additional diagnostic information may also appear.

## 6. Results and Observations

The following table summarizes the outcomes obtained during the practical:

| Operation Performed | Observation |
|---|---|
| SHA-256 Digest Calculation | Completed successfully |
| RSA Private Key Creation | Generated successfully |
| RSA Public Key Extraction | Completed successfully |
| Digital Signature Generation | Created successfully |
| Verification of Original Message | Verified OK |
| Verification After Modification | Verification Failure |

### Major Observations

1. The SHA-256 algorithm produced a fixed-length digest of 256 bits for the given input.
2. An RSA key pair consisting of a 2048-bit private key and its corresponding public key was generated.
3. The digital signature was successfully created using the private key.
4. Verification of the unchanged message returned the result `Verified OK`.
5. After modifying the message, the verification process returned `Verification failure`.
6. The experiment demonstrated how digital signatures can detect changes in signed information and validate the corresponding signature.

## 7. Directory Structure

All the generated files are organized within the `Experiment-5` directory as shown below:

```text
Experiment-5/
│
├── README.md
├── message.txt
├── hash.txt
├── public_key.pem
├── private_key.pem
└── signature.bin
```

**Security Precaution:** The RSA private key stored in `private_key.pem` contains sensitive cryptographic information. It should never be uploaded to public platforms such as GitHub or shared with unauthorized users.

## 8. Conclusion

The practical implementation of SHA-256 hashing and RSA digital signatures was successfully completed using OpenSSL. The SHA-256 algorithm was used to calculate the digest of the sample message, followed by the creation of an RSA public-private key pair.

A digital signature was generated using the private key and successfully validated using the corresponding public key. When the original message was modified, the verification process failed, confirming that changes in signed data can be detected.

Thus, the experiment demonstrated the importance of cryptographic hashing and digital signatures in maintaining data integrity and verifying message authenticity.

---

**Subject:** Cryptography and Network Security  
**Experiment Number:** 05  
**Software Used:** OpenSSL and Windows Command Prompt  
**Hashing Technique:** SHA-256  
**Digital Signature Technique:** RSA (2048-bit)