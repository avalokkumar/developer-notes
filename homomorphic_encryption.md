## Homomorphic Encryption (HE)

Homomorphic encryption is a powerful but complex form of encryption that allows you to perform mathematical operations on encrypted data without decrypting it first.

Imagine you have a locked box containing a number, and you want to multiply it by 2 without ever knowing the actual number inside. With traditional encryption, you'd need to unlock the box, perform the multiplication, and then re-encrypt the result. But with homomorphic encryption, you can directly multiply the encrypted number by 2, and the resulting ciphertext will still hold the encrypted product without revealing the original number.

### Types of HE algorithms:

#### * Fully Homomorphic Encryption (FHE):
##### * BGV scheme: Popular for its practicality and uses polynomial rings.

The BGV scheme (Brakerski-Gentry-Vaikuntanathan) is a fully homomorphic encryption (FHE) scheme, which means it allows for arbitrary computations to be performed on encrypted data without decrypting it. This capability is highly desirable for privacy-preserving computation, as it enables computations on sensitive data while keeping it encrypted throughout the entire process.

Here's a detailed explanation of the BGV scheme, focusing on its practicality and use of polynomial rings:

1. **Background on Fully Homomorphic Encryption (FHE)**:
   - Fully homomorphic encryption (FHE) is a form of encryption that supports both addition and multiplication operations on encrypted data.
   - In other words, given ciphertexts representing plaintexts \(x\) and \(y\), an FHE scheme allows computation of a ciphertext representing \(x + y\) and \(x \times y\) without knowledge of the plaintexts.
   - This enables computation on encrypted data without the need to decrypt it first, thus preserving privacy and security.

2. **Polynomial Ring Structure**:
   - The BGV scheme is based on polynomial rings, specifically the ring of polynomials with coefficients modulo some integer \(q\).
   - Encryption and decryption operations involve polynomial operations and polynomial evaluation.
   - Addition and multiplication operations on ciphertexts are performed using polynomial addition and multiplication modulo \(q\).

3. **Key Components**:
   - **Key Generation**: Involves generating public and private keys. The public key is used for encryption, while the private key is used for decryption.
   - **Encryption**: Encrypts plaintext messages into ciphertexts using the public key. This process involves encoding the plaintext as a polynomial and adding noise to the polynomial to preserve security.
   - **Decryption**: Decrypts ciphertexts back to plaintext messages using the private key. This process involves evaluating a polynomial using the private key.

4. **Practicality and Uses**:
   - While fully homomorphic encryption was initially considered impractical due to its computational complexity and overhead, advancements in schemes like BGV have made it more practical for real-world applications.
   - BGV and similar schemes have found applications in various domains, including:
     - Privacy-preserving computation: Allows computation on encrypted data in scenarios where data privacy is critical, such as medical research, financial analysis, and data outsourcing.
     - Secure outsourcing of computations: Enables offloading computations to untrusted servers while keeping sensitive data encrypted.
     - Secure multiparty computation: Facilitates collaborative computation among multiple parties without revealing their inputs.

5. **Example**:
   - Suppose we want to perform addition and multiplication operations on encrypted integers using the BGV scheme.
   - Given ciphertexts \(c_1\) and \(c_2\) representing encrypted integers \(x\) and \(y\), we can compute ciphertexts representing \(x + y\) and \(x \times y\) using homomorphic addition and multiplication operations.
   - The result of the computation will be a ciphertext representing the encrypted sum \(x + y\) and product \(x \times y\), respectively.



##### * CKKS scheme: Supports fixed-point arithmetic and is efficient for specific use cases.

The CKKS scheme (Cheon-Kim-Kim-Song) is a fully homomorphic encryption (FHE) scheme that supports fixed-point arithmetic and is designed to be efficient for specific use cases. It is particularly well-suited for applications where computations involve real numbers and require high performance. Here's a detailed explanation of the CKKS scheme, along with examples:

1. **Background on Fully Homomorphic Encryption (FHE)**:
   - Fully homomorphic encryption (FHE) is a form of encryption that supports arbitrary computations on encrypted data without decryption.
   - FHE schemes enable computations on encrypted data while preserving privacy and security, making them valuable for applications that involve sensitive data.

2. **Fixed-Point Arithmetic**:
   - CKKS employs fixed-point arithmetic, which is a method of representing and performing arithmetic operations on real numbers with fixed precision.
   - In fixed-point arithmetic, real numbers are represented as integers scaled by a fixed factor. This allows for efficient arithmetic operations using integer arithmetic.

3. **Efficiency and Use Cases**:
   - The CKKS scheme is designed to be efficient for specific use cases, particularly those involving computations on real numbers with fixed precision.
   - It offers advantages such as faster encryption and decryption, reduced noise growth during homomorphic operations, and improved performance for computations on real-number data.
   - CKKS is well-suited for applications such as:
     - Secure machine learning: Allows for training and inference on encrypted data without compromising privacy.
     - Privacy-preserving analytics: Enables computation on sensitive data while keeping it encrypted, ensuring privacy and confidentiality.
     - Secure outsourcing of computations: Facilitates offloading computations to untrusted servers while protecting the confidentiality of the data.

4. **Key Components**:
   - **Key Generation**: Involves generating public and private keys for encryption and decryption operations.
   - **Encryption**: Encrypts real-number plaintexts into ciphertexts using the public key. This process involves encoding real numbers as polynomials and adding noise to the polynomials to preserve security.
   - **Decryption**: Decrypts ciphertexts back to real-number plaintexts using the private key. This process involves evaluating polynomials and scaling the result to obtain the original real-number plaintext.

5. **Example**:
   - Suppose we want to perform computations on encrypted real numbers using the CKKS scheme.
   - Given a ciphertext representing an encrypted real number \(x\), we can perform arithmetic operations such as addition, multiplication, and other mathematical functions on \(x\) without decrypting it.
   - For example, we can compute the sum \(x + y\) or the product \(x \times y\) of two encrypted real numbers without revealing their values.



#### * Somewhat Homomorphic Encryption (SHE):
##### * Paillier cryptosystem: Allows efficient additions and limited multiplications.

The Paillier cryptosystem is a type of somewhat homomorphic encryption scheme that allows for efficient additions and limited multiplications on encrypted data. It was proposed by Pascal Paillier in 1999 and is widely used in various applications where homomorphic properties are required. Here's a detailed explanation of the Paillier cryptosystem, along with examples:

1. **Background on Somewhat Homomorphic Encryption (SHE)**:
   - Somewhat homomorphic encryption (SHE) schemes allow for a limited number of homomorphic operations on encrypted data.
   - Unlike fully homomorphic encryption (FHE), SHE schemes support either addition or multiplication operations on encrypted data, but not both simultaneously.

2. **Properties of the Paillier Cryptosystem**:
   - The Paillier cryptosystem is an example of an SHE scheme that supports homomorphic addition and limited homomorphic multiplication operations.
   - It is based on the difficulty of the decisional composite residuosity assumption (DCRA), which is related to the computational hardness of factoring large composite numbers.
   - The key properties of the Paillier cryptosystem include:
     - Additive homomorphism: Given ciphertexts representing plaintexts \(x\) and \(y\), the sum \(x + y\) can be computed homomorphically without knowledge of the plaintexts.
     - Limited multiplicative homomorphism: While the Paillier cryptosystem does not directly support homomorphic multiplication, it allows for the multiplication of an encrypted value by a plaintext constant.

3. **Key Components**:
   - **Key Generation**: Involves generating public and private keys for encryption and decryption operations.
   - **Encryption**: Encrypts plaintext messages into ciphertexts using the public key. This process involves encoding the plaintext as an integer and adding random noise to enhance security.
   - **Decryption**: Decrypts ciphertexts back to plaintext messages using the private key. This process involves applying modular exponentiation and modular inversion operations to recover the original plaintext.

4. **Example**:
   - Suppose we want to perform addition and limited multiplication operations on encrypted integers using the Paillier cryptosystem.
   - Given ciphertexts \(c_1\) and \(c_2\) representing encrypted integers \(x\) and \(y\), we can compute a ciphertext representing the encrypted sum \(x + y\) using homomorphic addition.
   - Additionally, we can multiply a ciphertext \(c_1\) representing an encrypted integer \(x\) by a plaintext constant \(k\) to obtain a ciphertext representing the encrypted product \(kx\).

   Example Code (Python):
   ```python
   from phe import paillier

   # Key generation
   public_key, private_key = paillier.generate_paillier_keypair()

   # Encryption
   x = 10
   y = 20
   c1 = public_key.encrypt(x)
   c2 = public_key.encrypt(y)

   # Homomorphic addition
   c_sum = c1 + c2
   decrypted_sum = private_key.decrypt(c_sum)
   print("Decrypted sum:", decrypted_sum)

   # Limited multiplicative homomorphism
   k = 2
   c_product = c1 * k
   decrypted_product = private_key.decrypt(c_product)
   print("Decrypted product:", decrypted_product)
   ```

##### * ElGamal cryptosystem: Supports additions and single multiplications.

The ElGamal cryptosystem is a type of somewhat homomorphic encryption (SHE) scheme that supports additions and single multiplications on encrypted data. Proposed by Taher ElGamal in 1985, it is based on the difficulty of the discrete logarithm problem and is widely used in practice due to its efficiency and homomorphic properties. Here's a detailed explanation of the ElGamal cryptosystem, along with examples:

1. **Background on Somewhat Homomorphic Encryption (SHE)**:
   - Somewhat homomorphic encryption (SHE) schemes allow for a limited number of homomorphic operations on encrypted data.
   - Unlike fully homomorphic encryption (FHE), SHE schemes support either addition or multiplication operations on encrypted data, but not both simultaneously.

2. **Properties of the ElGamal Cryptosystem**:
   - The ElGamal cryptosystem is an example of an SHE scheme that supports homomorphic addition and limited homomorphic multiplication operations.
   - It is based on the difficulty of computing discrete logarithms in finite cyclic groups, typically in the multiplicative group of a finite field or elliptic curve group.
   - The key properties of the ElGamal cryptosystem include:
     - Additive homomorphism: Given ciphertexts representing plaintexts \(x\) and \(y\), the sum \(x + y\) can be computed homomorphically without knowledge of the plaintexts.
     - Limited multiplicative homomorphism: While the ElGamal cryptosystem does not directly support homomorphic multiplication, it allows for the multiplication of an encrypted value by a plaintext constant.

3. **Key Components**:
   - **Key Generation**: Involves generating public and private keys for encryption and decryption operations.
   - **Encryption**: Encrypts plaintext messages into ciphertexts using the public key. This process involves selecting random parameters and computing a shared secret, which is then used to generate ciphertexts.
   - **Decryption**: Decrypts ciphertexts back to plaintext messages using the private key. This process involves applying modular exponentiation and modular inversion operations to recover the original plaintext.

4. **Example**:
   - Suppose we want to perform addition and limited multiplication operations on encrypted integers using the ElGamal cryptosystem.
   - Given ciphertexts \(c_1\) and \(c_2\) representing encrypted integers \(x\) and \(y\), we can compute a ciphertext representing the encrypted sum \(x + y\) using homomorphic addition.
   - Additionally, we can multiply a ciphertext \(c_1\) representing an encrypted integer \(x\) by a plaintext constant \(k\) to obtain a ciphertext representing the encrypted product \(kx\).

   Example Code (Python):
   ```python
   from Crypto.Util.number import getPrime
   from Crypto.Random import get_random_bytes

   # Key generation
   p = getPrime(128)
   g = 2  # Generator
   x = get_random_bytes(16)  # Private key
   h = pow(g, x, p)  # Public key

   # Encryption
   m1 = 10
   m2 = 20
   r1 = get_random_bytes(16)
   r2 = get_random_bytes(16)
   c1 = (pow(g, r1, p), (pow(h, r1, p) * m1) % p)
   c2 = (pow(g, r2, p), (pow(h, r2, p) * m2) % p)

   # Homomorphic addition
   c_sum = (c1[0] * c2[0] % p, c1[1] * c2[1] % p)
   decrypted_sum = (c_sum[1] * pow(c_sum[0], -x, p)) % p
   print("Decrypted sum:", decrypted_sum)

   # Limited multiplicative homomorphism
   k = 2
   c_product = (pow(g, r1, p), (pow(h, r1, p) * (m1 * k)) % p)
   decrypted_product = (c_product[1] * pow(c_product[0], -x, p)) % p
   print("Decrypted product:", decrypted_product)
   ```

### Understanding the algorithms:

Each HE algorithm has its own mathematical foundation and implementation intricacies. Grasping their underlying mathematics (e.g., lattice-based cryptography for BGV) is crucial for choosing the right one for your needs.


### Libraries and implementations:

Open-source libraries like HElib, SEAL, and PALISade offer implementations of various HE schemes in different programming languages (C++, C#, Python). Exploring their documentation and tutorials is crucial for learning how to use them practically.

### Complexity and performance:

HE algorithms are computationally expensive, and their performance depends on factors like data size, operation type, and desired security level. Consider trade-offs between security and efficiency when choosing an algorithm and implementation.

### Security considerations:

While HE protects data during computations, it's essential to understand potential vulnerabilities like side-channel attacks and implement proper countermeasures.

> Homomorphic Encryption (HE) involves understanding various algorithms and their implementations. However, due to the complexity and rapidly evolving nature of HE, providing specific instructions on their usage goes beyond the scope of this notes.

**For more information on homomorphic encryption, you can refer to the following resources:**
- [Homomorphic Encryption Standardization](https://homomorphicencryption.org/)
- [Microsoft SEAL](https://www.microsoft.com/en-us/research/project/microsoft-seal/)

---
