---
layout: page
---

# CH 9 | Security

* (Discussion from 2019)[https://missing.csail.mit.edu/2019/security/]

* **Plaintext** represents inputs, while **ciphertext** represents outputs

### Entropy

* A measure of information, as well as randomness

* Use 40+ bits of entropy for secure passwords

![passwords](../resources/password_strength.png)

### Hash Functions

* Maps any amount of data to a fixed size, similar to a pointer

* Often has few additional properties that make it useful for security purposes

```bash
# Hash Example

    "An example of a hash function is SHA1, which is used in Git. It maps arbitrary-sized inputs to 160-bit outputs (which can be represented as 40 hexadecimal characters). We can try out the SHA1 hash on an input using the sha1sum command:"

    $ printf 'hello' | sha1sum
    aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
    $ printf 'hello' | sha1sum
    aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
    $ printf 'Hello' | sha1sum 
    f7ff9e8b7bb2e09b70935a5d785e0cc5d9d0abf0

    "At a high level, a hash function can be thought of as a hard-to-invert random-looking (but deterministic) function..."
```

```bash
# Qualities of a Hash Function

    Deterministic               # The same input always generates the same output.
    Non-invertible              # It is hard to find an input m such that hash(m) = h for some desired output h.
    Target collision resistant  # Given an input m_1, it’s hard to find a different input m_2 such that hash(m_1) = hash(m_2).
    Collision resistant        # It’s hard to find two inputs m_1 and m_2 such that hash(m_1) = hash(m_2) (note that this is a strictly stronger property than target collision resistance).
```

### Key Derivation Functions

* Algorithms that produce fixed-length keys

* Often used to store login credentials, via "salting" the password and storing

```bash
# Salt Example

Username 	Password
user1 	    password123
user2 	    password123

Username 	Salt value 	        String to be hashed 	        Hashed value = SHA256 (Password + Salt value)
user1 	    E1F53135E559C253 	password123E1F53135E559C253 	72AE25495A7981C40622D49F9A52E4F1565C90F048F59027BD9C8C8900D5C3D8
user2 	    84B03D034B409D4E 	password12384B03D034B409D4E 	B4B6603ABC670967E99C7E7F1389E40CD16E78AD38EB1468EC2AA1E62B8BED3A
```

### Symmetric and Asymmetric Cryptography

```java
// Cryptography Pseudocode 
"Symmetric and asymmetric encryption can be compared to physical locks. A symmetric cryptosystem is like a door lock: anyone with the key can lock and unlock it. Asymmetric encryption is like a padlock with a key. You could give the unlocked lock to someone (the public key), they could put a message in a box and then put the lock on, and after that, only you could open the lock because you kept the key (the private key)."


// Symmetric Cryptography
keygen() -> key  //(this function is randomized)

encrypt(plaintext: array<byte>, key) -> array<byte>  //(the ciphertext)
decrypt(ciphertext: array<byte>, key) -> array<byte>  //(the plaintext)

decrypt(encrypt(m, k), k) = m  //(decrypt undoes encrypt)


// Asymmetric Cryptography
keygen() -> (public key, private key)  //(this function is randomized)

encrypt(plaintext: array<byte>, public key) -> array<byte>  //(the ciphertext)
decrypt(ciphertext: array<byte>, private key) -> array<byte>  //(the plaintext)

decrypt(encrypt(m, public key), private key) = m  //(decrypt undoes encrypt)

sign(message: array<byte>, private key) -> array<byte>  //(the signature)
verify(message: array<byte>, signature: array<byte>, public key) -> bool  //(whether or not the signature is valid)

verify(message, sign(message, private key), public key) = true //(verify matches sign)
```

### Case Studies

| Use Case         | Security Type            | Description                        |
|------------------|--------------------------|------------------------------------|
| Git References   | Hash                     | Pointers to Git objects            |
| Salted Passwords | Key Derivation Functions | Store passwords in a secure manner |
| SSH              | Asymmetric Cryptography  | Safely connect to trusted servers  |