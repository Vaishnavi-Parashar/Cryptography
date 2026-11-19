# Experiment 4: Implementation of RSA-Based File Encryption and Decryption Using OpenSSL

## 1. Aim

To create RSA public and private keys with the help of OpenSSL and demonstrate the encryption and decryption of a sample file using asymmetric cryptography.

## 2. Software Requirements

- OpenSSL
- Windows Command Prompt (CMD)
- Visual Studio Code (VS Code) or any text editor

## 3. Theory

RSA is a widely used asymmetric encryption technique that works with a pair of mathematically related keys. These keys perform different functions during the encryption and decryption process.

The two keys involved are:

- **Public Key:** This key is used to encrypt information and can be distributed to other users.
- **Private Key:** This key is required to decrypt the encrypted information and must be stored securely.

Unlike symmetric encryption, RSA does not require the same key for both operations. The public key can be shared openly, whereas the private key must remain confidential.

## 4. Implementation Procedure

### Step 1: Creating the RSA Private Key

First, generate a private key with a length of 2048 bits using the following command:

```cmd
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
```

This instruction creates an RSA private key and stores it in a file named `private_key.pem`. The generated key is used during the decryption process.

### Step 2: Extracting the Public Key

After creating the private key, obtain its corresponding public key by executing:

```cmd
openssl pkey -in private_key.pem -pubout -out public_key.pem
```

This command reads the private key file, extracts the associated public key, and saves it separately as `public_key.pem`.

### Step 3: Preparing the Message File

Create a new text document named `message.txt` using VS Code or another text editor.

Enter the following sample content:

```text
This is a sample message for RSA encryption.
```

Save the file because it will be used as the original input for the encryption operation.

### Step 4: Encrypting the Original File

Use the generated public key to convert the original message into encrypted data.

Execute the following command:

```cmd
openssl pkeyutl -encrypt -in message.txt -pubin -inkey public_key.pem -out encrypted.bin
```

This command takes the contents of `message.txt`, applies RSA encryption with the public key, and writes the resulting ciphertext into `encrypted.bin`.

**Note:** RSA encryption has a restriction on the amount of data that can be processed directly. For a 2048-bit RSA key using OAEP with SHA-256, the maximum message size is 190 bytes. Larger files should be protected using AES encryption, while RSA can be used to encrypt the AES secret key.

### Step 5: Recovering the Original File

To convert the encrypted information back into its readable form, execute:

```cmd
openssl pkeyutl -decrypt -in encrypted.bin -inkey private_key.pem -out decrypted.txt
```

The command uses the previously generated private key to decrypt the ciphertext and stores the recovered information in `decrypted.txt`.

### Step 6: Checking the Decrypted Output

Once decryption is completed, display the recovered message through CMD:

```cmd
type decrypted.txt
```

To ensure that the decrypted content is identical to the original input, compare both files using:

```cmd
fc /b message.txt decrypted.txt
```

If both files contain identical data, the comparison confirms that the original message has been successfully restored.

## 5. Files Generated During Execution

The following files are produced throughout the experiment:

| File Name | Purpose |
|---|---|
| `private_key.pem` | Stores the RSA private key |
| `public_key.pem` | Contains the corresponding public key |
| `message.txt` | Holds the original readable message |
| `encrypted.bin` | Contains the encrypted message |
| `decrypted.txt` | Stores the recovered plaintext |

## 6. Result

RSA key generation and file encryption operations were successfully demonstrated using OpenSSL. A 2048-bit public-private key pair was generated, and the sample message was encrypted using the public key.

The encrypted data was subsequently decrypted using its corresponding private key, allowing the original message to be recovered and verified.

## 7. Conclusion

This experiment demonstrated the practical application of RSA asymmetric encryption through OpenSSL. The process included generating a key pair, preparing an input file, encrypting its contents, and retrieving the original information through decryption.

It was understood that the public key is responsible for encryption, while the private key is necessary for decryption. The experiment also highlighted the importance of protecting private keys and using hybrid encryption techniques when handling larger files.

## 8. Screenshots

Capture and save the screenshots showing the successful execution of the following operations inside the `screenshots/` directory:

1. RSA private and public key generation.
2. Encryption of the sample message.
3. Successful decryption and verification of the recovered file.

---

**Tool Used:** OpenSSL  
**Operating System:** Windows  
**Subject:** Cryptography and Network Security  
**Experiment Topic:** RSA-Based File Encryption and Decryption