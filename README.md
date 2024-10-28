# Numerical Cryptography Analysis

## Project Overview

The **Numerical Cryptography Analysis** project focuses on exploring basic cryptographic techniques through the implementation of the Caesar and Vigenère ciphers. These classical encryption methods provide insights into the fundamental principles of cryptography, including encryption, decryption, and frequency analysis, which are essential for understanding modern cryptographic systems.

## Introduction to Cryptography

Cryptography is the practice and study of techniques for securing communication and information. It enables the protection of sensitive data against unauthorized access and ensures the confidentiality, integrity, and authenticity of messages. The project highlights two classic cipher techniques:

1. **Caesar Cipher**: A substitution cipher where each letter in the plaintext is shifted by a fixed number of places down or up the alphabet.
2. **Vigenère Cipher**: A more complex form of substitution cipher that uses a keyword to determine the shift for each letter in the plaintext.

### Key Concepts

- **Encryption**: The process of converting plaintext into ciphertext using a specific algorithm and key.
- **Decryption**: The reverse process of converting ciphertext back into plaintext.
- **Frequency Analysis**: A technique used to analyze the frequency of letters in the ciphertext to derive potential keys or insights about the plaintext.

## Code Explanation

The project is implemented in Python and leverages the **collections** module for frequency counting. Below are the key components of the code.

### Imports

```python
import string
from collections import Counter
```

- **string**: Although not used in the provided code, this module provides various string constants and classes.
- **Counter**: A dictionary subclass from the **collections** module that counts the occurrences of elements in a collection.

### Caesar Cipher Functions

1. **caesar_encrypt(plaintext, shift)**: Encrypts plaintext using the Caesar cipher with a specified shift.

   - **Parameters**:
     - `plaintext`: The text to be encrypted.
     - `shift`: The number of positions to shift each letter.
   
   - **Returns**: The encrypted ciphertext.

   - **Logic**:
     - For each character in the plaintext, if it’s an alphabet letter, the function calculates its new position by applying the shift. Non-alphabet characters remain unchanged.

```python
def caesar_encrypt(plaintext, shift):
    encrypted_text = ""
    for char in plaintext:
        if char.isalpha():  # Check if character is a letter
            shift_base = ord('A') if char.isupper() else ord('a')
            encrypted_text += chr((ord(char) - shift_base + shift) % 26 + shift_base)
        else:
            encrypted_text += char  # Non-alphabet characters remain unchanged
    return encrypted_text
```

2. **caesar_decrypt(ciphertext, shift)**: Decrypts ciphertext using the Caesar cipher by reusing the encryption function with a negative shift.

```python
def caesar_decrypt(ciphertext, shift):
    return caesar_encrypt(ciphertext, -shift)  # Reuse encryption with negative shift for decryption
```

### Vigenère Cipher Functions

1. **vigenere_encrypt(plaintext, keyword)**: Encrypts plaintext using the Vigenère cipher based on the provided keyword.

   - **Parameters**:
     - `plaintext`: The text to be encrypted.
     - `keyword`: The keyword used to determine shifts for each letter.
   
   - **Returns**: The encrypted ciphertext.

   - **Logic**:
     - Each letter in the plaintext is shifted according to the corresponding letter in the keyword. Non-alphabet characters remain unchanged.

```python
def vigenere_encrypt(plaintext, keyword):
    encrypted_text = ""
    keyword = keyword.lower()
    keyword_length = len(keyword)
    for i, char in enumerate(plaintext):
        if char.isalpha():
            shift = ord(keyword[i % keyword_length]) - ord('a')
            shift_base = ord('A') if char.isupper() else ord('a')
            encrypted_text += chr((ord(char) - shift_base + shift) % 26 + shift_base)
        else:
            encrypted_text += char  # Non-alphabet characters remain unchanged
    return encrypted_text
```

2. **vigenere_decrypt(ciphertext, keyword)**: Decrypts ciphertext using the Vigenère cipher by reversing the encryption logic.

```python
def vigenere_decrypt(ciphertext, keyword):
    decrypted_text = ""
    keyword = keyword.lower()
    keyword_length = len(keyword)
    for i, char in enumerate(ciphertext):
        if char.isalpha():
            shift = ord(keyword[i % keyword_length]) - ord('a')
            shift_base = ord('A') if char.isupper() else ord('a')
            decrypted_text += chr((ord(char) - shift_base - shift) % 26 + shift_base)
        else:
            decrypted_text += char  # Non-alphabet characters remain unchanged
    return decrypted_text
```

### Frequency Analysis Function

**frequency_analysis(text)**: Analyzes the frequency of letters in a given text and calculates the percentage occurrence of each letter.

- **Parameters**:
  - `text`: The input text for which the frequency is to be calculated.

- **Returns**: A dictionary with letters as keys and their frequency as values.

- **Logic**:
  - It uses the `Counter` class to count the occurrences of each letter, normalizing the counts to percentages.

```python
def frequency_analysis(text):
    frequency = Counter(char.lower() for char in text if char.isalpha())
    total = sum(frequency.values())
    if total == 0:  # Avoid division by zero
        return frequency
    for letter in frequency:
        frequency[letter] /= total
    return frequency
```

### Example Usage

In the provided code, an example usage demonstrates the functionality of the Caesar and Vigenère ciphers along with frequency analysis.

```python
plaintext = "I AM NIMRA"
shift = 3
keyword = "KEY"

# Caesar Cipher Example
print("Original Text:", plaintext)
encrypted_caesar = caesar_encrypt(plaintext, shift)
print("Encrypted with Caesar:", encrypted_caesar)
decrypted_caesar = caesar_decrypt(encrypted_caesar, shift)
print("Decrypted with Caesar:", decrypted_caesar)

# Vigenère Cipher Example
encrypted_vigenere = vigenere_encrypt(plaintext, keyword)
print("Encrypted with Vigenere:", encrypted_vigenere)
decrypted_vigenere = vigenere_decrypt(encrypted_vigenere, keyword)
print("Decrypted with Vigenere:", decrypted_vigenere)

# Frequency Analysis
sample_text = "THIS IS A SAMPLE TEXT FOR FREQUENCY ANALYSIS"
print("\nFrequency Analysis of Sample Text:")
frequency = frequency_analysis(sample_text)
for char, freq in sorted(frequency.items()):
    print(f"{char}: {freq:.2%}")
```

## Conclusion

The **Numerical Cryptography Analysis** project provides a foundational understanding of classical cryptography techniques through practical implementation. By experimenting with the Caesar and Vigenère ciphers, users can appreciate the principles of encryption and decryption, along with the significance of frequency analysis in breaking ciphers.
