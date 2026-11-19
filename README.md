# EXP-1: Implementation of Classical Encryption Techniques

## Aim
To develop and demonstrate Caesar Cipher, Vigenère Cipher, and Rail Fence Cipher techniques for encrypting and decrypting the given plaintext **"HELLO WORLD"**, and understand the differences in their working and security.

## Plaintext
```text
HELLO WORLD
```

## 1. Caesar Cipher

Caesar Cipher is a basic substitution technique in which every character of the plaintext is moved forward by a fixed number of positions in the English alphabet.

- **Plaintext:** `HELLO WORLD`
- **Key:** 3
- **Encryption:** Every letter is replaced by the letter that comes three positions after it in the alphabet.
- **Decryption:** The encrypted letters are shifted three positions backward to obtain the original message.

**Encrypted text:**
```text
KHOOR ZRUOG
```

### Screenshot
![Caesar Cipher Screenshot](screenshots/caesar.png)

## 2. Vigenère Cipher

Vigenère Cipher is a polyalphabetic substitution technique that encrypts a message using a keyword. Each letter of the keyword determines the shifting value for the corresponding plaintext letter.

- **Plaintext:** `HELLO WORLD`
- **Key:** `KEY`
- **Encryption:** The keyword is repeatedly used to match the plaintext letters, while spaces are ignored during encryption.
- **Decryption:** The same keyword is applied to reverse the shifts and obtain the original message.

**Encrypted text:**
```text
RIJVS UYVJN
```

### Screenshot
![Vigenère Cipher Screenshot](screenshots/vigenere.png)

## 3. Rail Fence Cipher

Rail Fence Cipher is a transposition-based encryption method in which plaintext characters are placed in a zigzag sequence across a specified number of rails. The encrypted message is obtained by reading the characters row by row.

- **Plaintext:** `HELLO WORLD`
- **Key:** 2 rails
- **Encryption:** The letters are written in a zigzag arrangement across two rails and then read row-wise to generate the encrypted message.
- **Decryption:** The original zigzag pattern is recreated to rearrange the encrypted characters and recover the plaintext.

**Encrypted text (2 rails, spaces removed):**
```text
HLOWRD EL OL
```

### Screenshot
![Rail Fence Cipher Screenshot](screenshots/rail-fence.png)

## Comparison

| Feature | Caesar Cipher | Vigenère Cipher | Rail Fence Cipher |
|---|---|---|---|
| Cipher type | Substitution | Polyalphabetic substitution | Transposition |
| Key | Fixed numerical shift | Keyword | Number of rails |
| Working | Moves letters by fixed positions | Applies different shifts using a keyword | Changes the arrangement of letters |
| Security | Very weak | More secure than Caesar, but weak with short or repeated keys | Very weak |
| Main limitation | Can be cracked using brute force | Can be attacked through cryptanalysis when keys are weak | Letter arrangement can be reconstructed |

## Conclusion

Caesar, Vigenère, and Rail Fence are classical encryption techniques that demonstrate different approaches to protecting plaintext. Caesar and Vigenère change the letters through substitution, whereas Rail Fence changes their positions through transposition. These methods are useful for understanding cryptography fundamentals but are not secure enough for modern applications.