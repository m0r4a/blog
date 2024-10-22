---
title: "Summary of Cryptography Exam 2"
draft: false
date: 2024-10-22
description: This is a rewrite of the summary document from the Cryptography class.
summary: This post is a rewrite of the summary document provided by the professor that includes only the topics from exam 2.
---

## Key Management

aaKey management involves managing keys throughout their entire lifecycle, from creation to destruction, including their use, storage, assignment, creation, and destruction.

This allows us to maintain a secure ecosystem, where each user can have access to different permissions with a single key, similar to how master keys used to work.

Keys can be symmetric (single key) for information that will be "at rest" (meaning it won't travel through any medium) such as the keys themselves, or asymmetric (two keys) for information that will be "traveling" between different media.

Typically, a mixture of both cryptographic systems is used, using an asymmetric system to send a symmetric key, since symmetric cryptography is faster but cannot securely transmit the key by itself, so an asymmetric system is used to share the key.

Symmetric keys are symmetrically encrypted on a KM (key manager) server, so the user has to send their certificate (asymmetric cryptography) to the KM server to compare it with the certificate authority, which verifies if they are actually who they claim to be.

Once this is done, the server sends its certificate to the client to establish a connection, and then the KM server decrypts the symmetric key (with another symmetric key) and sends it to the user through a TLS channel.

Asymmetric keys follow a similar path, except that instead of using a TLS channel, it uses the public key of each encryption (user and server) to securely share a symmetric key through a channel (which might not be secure), and in turn, the information encrypted with the symmetric key.

### Authentication Process and Symmetric Encryption with Certificates

{{< figure
    src="resources/symetric_cypher.svg"
    alt="Image showing symmetric encryption on a server"
    nozoom=true
    class="mx-auto"
>}}

### Validation Process and Asymmetric Encryption on a KM Server

{{< figure
    src="resources/asymetric_cypher.svg"
    alt="Image showing asymmetric encryption on a server"
    nozoom=true
    class="mx-auto"
>}}

## Trusted Platform Module and TPM Uses

It is basically a crypto-processor, a physical chip that can come as an add-on, as shown in the photograph, or can be embedded in the motherboard. This chip is responsible for storing keys and processing complex cryptographic systems, assisting the processor (CPU) while being more secure since it can only connect with the processor, preventing unknown hardware from copying the keys or modifying its operation.

Among the things that can be done, the TPM can validate your identity using specific crypto-processor keys (which cannot be modified) or even keys from other applications that are stored within it.

It can also validate the operating system by analyzing signed components, and if the signatures don't match, it's probably because the file has been modified, which could indicate some type of infection (this is normally what prevents "secure boot").

### Different uses for the TPM chip
1. DRM (Digital Rights Management)
2. File and folder encryption
3. Secure email
4. SSL
5. VPN
6. One-time passwords
7. Account management
8. Two-Factor Authentication with chip keys

### Chip Components
1. Random number generator
2. Cryptographic key generation
3. Secure key storage
4. Hashes

## Internet Security

We find cryptography in many different places, especially where some type of authentication is needed, particularly when passwords or certificates are used.

There are 3 authentication methods:

{{< figure
    src="resources/auth_methods.svg"
    alt="Types of authentication methods"
    nozoom=true
    class="mx-auto"
>}}

Symmetric cryptography is for information not in transit, due to its speed and ease of key management.

Asymmetric cryptography is for information in transit, typically used for session management, and once the connection is established, symmetric cryptography is used for sending large volumes of information.

### The Problem of Password Security Management

#### Storage

Passwords should not be stored in plain text, which leads to the idea of storing them as a hash, so that if an attacker steals them, they cannot be reversed.

#### Hash Functions

{{< alert icon="comment" >}}
Cryptographic hash functions ≠ Password hash functions
{{< /alert >}}

The main problem is that cryptographic hash functions are not designed for passwords. They tend to be very fast, and generally this would be good, if it weren't because this benefits an attacker who wants to perform a brute force attack.

#### Recognition

The first step is to check if the password is already in some rainbow table on the internet or similar; if not, proceed with the brute force attack.

#### Speed

Speed plays a crucial role, so if the hashing method is very fast (say 0.1 seconds), the password can be broken in relatively little time, so we seek to keep the hashing process above 0.1 seconds, preferably close to 1 second speed.

#### Salt

Salt is a randomly generated set of letters for each user that changes the output hash, making it (computationally impossible) for the attacker to find the user's password generated in a rainbow table on the internet.

#### Pepper

Like salt, pepper also changes the final hash, but it's usually within the source code. This is useful if for some reason the database where we're storing passwords isn't secure, or we can't trust the traffic from the application to the database. We can add pepper to the source code as an extra security measure.

#### Extension

- PBKDF2
- bcrypt
- scrypt
- Argon2

In these algorithms, the goal is to iterate the use of different hashes and salts to delay the process of obtaining the password hash, and thus strengthen our application against brute force attacks.

The POODLE attack (Padding Oracle On Downgraded Legacy Encryption) is relevant here. For SSL 3.0, only 256 requests were needed to reveal one byte of communication. This attack takes advantage of a mechanism that reduces security in order to maintain interoperability.

For TLS 1.0 to 1.2, the attack is based on flaws in CBC encryption.

#### SSL Handshake

Used to establish the encryption method that will be maintained throughout the communication and session data.

1. Contact and capability establishment:
    - RSA
    - Authenticated Diffie-Hellman
    - Anonymous Diffie-Hellman
    - Fortezza
2. Key exchange and server authentication
3. Key exchange and client authentication
4. Protocol finalization (session keys are created here)

#### SSL Record

Used to transmit information between client and server.

1. Message data
2. Message fragmentation
3. Fragment compression
4. Addition of a message authentication code
5. Data encryption
6. Header addition
7. Sending the cryptogram through TCP

#### File Transfer Protocol

Contains no security layer.

#### File Transfer Protocol / SSL:

It's the same FTP protocol but over SSL protocol (currently TLS).

#### SSH File Transfer Protocol

It's a protocol created from scratch, very different from FTP, that works based on SSH.

#### Secure Copy Protocol

Based on:
- SSH
- FTP
- RCP commands
