# Introduction to Cryptography: The Caesar Cipher in Python

People sometimes need to keep secrets. The challenge is how to keep a
secret from some people, while communicating the secret to other...

### Introduction to Cryptography: The Caesar Cipher in Python
People sometimes need to keep secrets. The challenge is how to keep a
secret from some people, while communicating the secret to other people.
One of the simplest and best known encryption techniques is the Caesar
cipher, named after Julius Caesar who allegedly used it to communicate
with his generals.


<figcaption>Photo by <a
href="https://unsplash.com/@danabailey?utm_source=medium&amp;utm_medium=referral"
class="markup--anchor markup--figure-anchor"
data-href="https://unsplash.com/@danabailey?utm_source=medium&amp;utm_medium=referral"
rel="photo-creator noopener" target="_blank">Dana Bailey</a> on <a
href="https://unsplash.com?utm_source=medium&amp;utm_medium=referral"
class="markup--anchor markup--figure-anchor"
data-href="https://unsplash.com?utm_source=medium&amp;utm_medium=referral"
rel="photo-source noopener" target="_blank">Unsplash</a></figcaption>


In this post, we'll explore the Caesar cipher and implement it in
Python, demonstrating both encryption and decryption processes.

#### What is the Caesar Cipher?
The Caesar cipher is a substitution cipher where each letter in the
plaintext is shifted a certain number of places down the alphabet. For
example, with a shift of 3:

\- A would become D\
- B would become E\
- C would become F\
- ...and so on.

#### Implementing the Caesar Cipher in Python
Let's start with a simple implementation of the Caesar cipher in Python:

```python
from string import ascii_uppercase
from typing import Literal
def caesar_cipher(message: str, key: int, mode: Literal['encrypt', 'decrypt'] = 'encrypt') -> str:
 shift = key if mode == 'encrypt' else -key
 return ''.join(
 ascii_uppercase[(ascii_uppercase.index(char) + shift) % 26] if char in ascii_uppercase
 else char
 for char in message.upper()
 )

# Example usage:
message = "HELLO WORLD"
key = 3
encrypted = caesar_cipher(message, key)
print(f"Encrypted: {encrypted}")
decrypted = caesar_cipher(encrypted, key, 'decrypt')
print(f"Decrypted: {decrypted}")
```

This code defines a \`caesar_cipher\` function that can both encrypt and
decrypt messages. Let's break down how it works:

1\. We import \`ascii_uppercase\` from the \`string\` module to get the
uppercase alphabet.\
2. The function takes three parameters: the message, the key (shift
amount), and the mode (encrypt or decrypt).\
3. We use a list comprehension to process each character in the
message:\
 --- If the character is in the alphabet, we shift it by the key
amount.\
 --- If not, we leave it unchanged.\
4. We use modulo 26 to handle wraparound (e.g., Z shifting forward
becomes A).

#### Cracking the Caesar Cipher
One weakness of the Caesar cipher is that it's vulnerable to brute-force
attacks. Since there are only 26 possible shifts, an attacker can try
all possibilities quickly. Here's how we might implement a brute-force
attack:

```python
from string import ascii_letters, digits
def caesar_cipher_decrypt(message: str, key: int, symbols: str) -> str:
 return ''.join(
 symbols[(symbols.index(char) - key) % len(symbols)] if char in symbols
 else char
 for char in message
 )
def brute_force_caesar(message: str, symbols: str = ascii_letters + digits + ' !?.') -> None:
 for key in range(len(symbols)):
 decrypted = caesar_cipher_decrypt(message, key, symbols)
 print(f'Key #{key}: {decrypted}')
# Example usage
encrypted_message = 'VJy29rJ3!7u21K'
brute_force_caesar(encrypted_message)
```

This script will attempt to decrypt the message using every possible
key, printing each result. The correct decryption will likely be
recognizable among the output.

#### Wrapping up
The Caesar cipher is very simple introduction to cryptography. While
it's not secure for modern use due to its vulnerability to brute-force
attacks, understanding it provides a foundation for learning more
complex encryption methods.

Python's flexibility and readability make it an excellent language for
experimenting with cryptography concepts. Remember, while it's fun and
educational to play around with cryptography, in the real workd you
should use modern encryption methods for your applications.

Happy coding and decoding!
::::::::By [Kyle Jones](https://medium.com/@kyle-t-jones) on
[November 11, 2024](https://medium.com/p/6bca72f4f815).

[Canonical
link](https://medium.com/@kyle-t-jones/introduction-to-cryptography-the-caesar-cipher-in-python-6bca72f4f815)

Exported from [Medium](https://medium.com) on November 10, 2025.
