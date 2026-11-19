# Experiment 2: Frequency Analysis of Classical Cipher Texts

## Aim

To examine the frequency of letters in classical encrypted messages using CrypTool 2 and understand how frequency patterns can be used to break traditional encryption techniques.

## Tool Required

- CrypTool 2

## Theory

Frequency analysis is a cryptanalysis method in which the occurrence of individual letters in a text is examined. In the English language, certain letters, particularly E, T, A, and O, appear more often than others. These commonly occurring letters can provide useful clues when attempting to decode an encrypted message.

Traditional encryption techniques, such as the Caesar cipher, replace each letter with another letter according to a fixed shifting rule. Although the actual letters change during encryption, their occurrence counts remain unchanged. Therefore, the original frequency distribution is preserved in a shifted form, making such ciphers susceptible to frequency-based attacks, particularly when larger texts are available.

## Procedure

1. Launch CrypTool 2 and start a fresh project.
2. Insert a Text Input component and provide the plaintext `THE CAT IS ON THE MAT`.
3. Attach the input component to the Frequency Test component to examine the frequency of each letter.
4. Include a Caesar Cipher component and configure it for encryption using key value `3`.
5. Connect the encrypted output to another Frequency Test component.
6. Run the complete workflow and examine the frequency graph generated for the encrypted message.
7. Analyze both frequency distributions to understand how encryption affects the arrangement of letters.

## Input

- **Original Text:** `THE CAT IS ON THE MAT`
- **Encryption Method:** Caesar Cipher
- **Shift Key:** 3

## Output and Observation

The Frequency Test component generates a graphical representation of how frequently different letters appear in the given text. Initially, the graph represents the distribution of letters in the original plaintext.

After applying Caesar encryption with a shift of 3, the letters are replaced by their corresponding shifted characters. However, the number of occurrences of each letter remains identical, with only the letter positions changing.

It was also observed that the given input contains very few characters. Therefore, its frequency distribution alone may not provide enough information to accurately determine the original message.

## Vulnerability Analysis

The Caesar cipher has a major weakness because it uses a fixed substitution for every occurrence of a particular letter. This allows an attacker to examine repeated patterns and compare the frequency of ciphertext letters with the usual frequency of letters in English.

By identifying likely letter substitutions or testing the possible shifting values, an attacker can eventually recover the original plaintext. Hence, the Caesar cipher does not provide strong protection against frequency analysis attacks.

## Result

The frequency distribution of plaintext and Caesar-encrypted text was successfully examined using CrypTool 2. The experiment established that Caesar encryption changes the letters but retains their frequency relationships. This demonstrates why classical substitution ciphers are vulnerable to frequency analysis and other cryptographic attacks.

## Screenshots

1. `screenshots/frequency_test.png`
2. `screenshots/frequency_test_caesar.png`