# Experiment 6: Creation and Analysis of Self-Signed X.509 Certificates Using OpenSSL

## 1. Aim

To generate a self-signed X.509 certificate with OpenSSL and examine its important properties, certificate validity, and associated security characteristics.

## 2. Software Requirements

- OpenSSL
- Windows Command Prompt (CMD)
- Visual Studio Code (Optional)

## 3. Theory

An X.509 certificate is a digital document that connects the identity of an individual or organization with its public key. It is commonly used in secure communication to establish identity and support authentication.

A digital certificate contains several details, including the owner's identity, issuing authority, public key, validity dates, serial number, and digital signature.

A self-signed certificate is a special type of certificate in which the certificate owner signs it using their own private key instead of obtaining a signature from an external Certificate Authority (CA).

Such certificates are useful for practical demonstrations, development, and testing purposes. However, they are not automatically recognized as trusted certificates by web browsers or operating systems.

## 4. Implementation Procedure

### Step 1: Create an RSA Private Key

Begin by generating a private key using the RSA algorithm with a key length of 2048 bits.

Execute the following command in Windows CMD:

```cmd
openssl genrsa -out private.key 2048
```

This command generates the RSA private key and stores it in a file named `private.key`. The generated key will be used to sign the digital certificate.

### Step 2: Generate the Self-Signed X.509 Certificate

After creating the private key, use it to generate a self-signed digital certificate.

Run the following command:

```cmd
openssl req -new -x509 -key private.key -out certificate.crt -days 365
```

During execution, OpenSSL asks for certain identity-related details that become part of the certificate.

Enter the requested information, including:

- Country Name
- State or Province
- Organization Name
- Organizational Unit
- Common Name (CN)
- Email Address (if requested)

After entering the required details, OpenSSL creates the certificate file `certificate.crt` with a validity period of 365 days.

### Step 3: View the Certificate Information

To examine the complete contents and properties of the generated certificate, execute:

```cmd
openssl x509 -in certificate.crt -text -noout
```

This command displays the certificate information in a readable format.

The following attributes can be identified:

- **Subject:** Contains the identity information of the certificate owner.
- **Issuer:** Specifies the entity responsible for signing the certificate.
- **Serial Number:** Represents the unique identification number assigned to the certificate.
- **Validity Period:** Displays the beginning and expiration dates of the certificate.
- **Public Key:** Contains the public key associated with the certificate.
- **Signature Algorithm:** Indicates the cryptographic algorithm used to generate the certificate signature.

### Step 4: Compare the Subject and Issuer Details

To separately display the Subject and Issuer information, use:

```cmd
openssl x509 -in certificate.crt -noout -subject -issuer
```

The command extracts and displays both identity fields without printing the entire certificate.

Since the certificate is self-signed, its Subject and Issuer should represent the same entity. This confirms that the certificate was issued and signed by the same identity.

## 5. Files Generated

After completing the certificate generation process, the following two files will be available:

| File Name | Description |
|---|---|
| `private.key` | Stores the RSA private key used for signing |
| `certificate.crt` | Contains the generated self-signed X.509 certificate |

The certificate inspection command also provides information about its identity, serial number, validity dates, public key, and signature algorithm.

## 6. Security Analysis

The following points explain the security aspects of the generated certificate:

1. **Private Key Protection:** The private key must be stored securely because anyone possessing it can create signatures using that key.
2. **Certificate Validity:** The validity period specifies the dates during which the certificate is considered time-valid.
3. **Self-Signed Certificate Trust:** A self-signed certificate does not receive authentication from an already trusted Certificate Authority.
4. **RSA Key Strength:** A 2048-bit RSA key provides a commonly used level of cryptographic security. However, security also depends on proper key storage, signature algorithms, certificate configuration, and trust management.

## 7. Expected Output

The experiment produces a private key and a corresponding self-signed certificate.

The certificate inspection operation displays its major attributes, including the Subject, Issuer, Serial Number, Validity Period, Public Key, and Signature Algorithm.

For a successfully generated self-signed certificate, the Subject and Issuer fields identify the same entity.

## 8. Result

A self-signed X.509 digital certificate was successfully generated using OpenSSL with a 2048-bit RSA private key. The certificate was examined to understand its identity details, issuing information, validity period, public key, and signature algorithm.

The relationship between the Subject and Issuer was also checked to understand how self-signed certificates differ from certificates issued by trusted authorities.

## 9. Conclusion

This practical demonstrated the process of generating and examining a self-signed X.509 digital certificate using OpenSSL. The experiment involved creating an RSA private key, generating a certificate, and inspecting its important attributes through command-line operations.

It was understood that X.509 certificates associate public keys with identities and are important in secure communication. The practical also highlighted that self-signed certificates are useful for testing and learning, but they do not automatically provide trust like certificates issued by recognized Certificate Authorities.

## 10. Screenshots

Capture the screenshots of the following operations and store them inside the `screenshots/` folder:

1. Successful generation of the RSA private key.
2. Creation of the self-signed X.509 certificate.
3. Display of certificate attributes using OpenSSL.
4. Comparison of the Subject and Issuer information.

**Security Precaution:** The file `private.key` contains confidential cryptographic information. Never upload it to a public GitHub repository or share it with unauthorized individuals. It should also be excluded from version control.

---

**Subject:** Cryptography and Network Security  
**Experiment Number:** 06  
**Software Used:** OpenSSL and Windows Command Prompt  
**Certificate Standard:** X.509  
**Key Algorithm:** RSA (2048-bit)