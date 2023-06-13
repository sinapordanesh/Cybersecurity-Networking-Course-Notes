# 2_Symmetric-Key Cryptography I

# Symmetric Encryption

## Symmetric Encryption

- Functionality: Decrypt(k, Encrypt(k, p)) = p
- Security: Adversary that intercepts c= Encrypt(k, y) cannot retrieve p - confidentiality

![Screenshot 2023-06-07 at 9.57.24 AM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_9.57.24_AM.png)

## Vernam Cipher

- Functionality: (p XOR k) XOR k = p
- Security: Adversary that intercepts (p XOR k) cannot retrieve p - confidentiality

![Screenshot 2023-06-07 at 9.59.12 AM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_9.59.12_AM.png)

- Perfect cipher: each plaintext character is
encrypted using its own key.
- Very fast (`XOR`) and requires little memory (store
only the last character).
- `k` must be used only once. 
`c_1=p_1 XOR K, c_2=p_2 " XOR " K → C_1 XOR c_2= (p-1 XOR k) XOR (p *2 " XOR " k) = p* 1XOR p_2`
- It requires a stream setup.
- Best when the amount of data is
unknown/continuous e.g., network streams.

![Screenshot 2023-06-07 at 10.04.06 AM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.04.06_AM.png)

# Block Ciphers

Block Ciphers

- Large granularity: Encrypt a whole block of 64 or 128 bits at a time.
- Diffusion: Information from 1 plaintext bit is diffused into several ciphertext bits
- Advantages:
    - Can provide integrity
    - Less difficult to implement correctly and less prone to weaknesses.
- Disadvantages:
    - Encryption/decryption is slower.
    - More susceptible to noise: an error in 1 bit corrupts the entire block.
- Most symmetric-key ciphers are block ciphers: `DES`, `Triple DES`, `AES`.

![Screenshot 2023-06-07 at 10.08.45 AM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.08.45_AM.png)

![Screenshot 2023-06-07 at 10.09.41 AM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.09.41_AM.png)

![Screenshot 2023-06-07 at 10.15.25 AM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.15.25_AM.png)

# The Advanced Encryption Standard (AES)

- AES is a widely-used block cipher.
- US Standard from NIST (2001), chosen based on a selection process (1997-2000).
- Invented by Vincent Rimen and Joan Daemon - Rindael block cipher.
- AES uses a block of 128-bits.
- Iterative block cipher. AS
- AES allows keys of different sizes
    - AES-128: 128-bits with 10 rounds.
    - AES-192: 192-bits with 12 rounds.
    - AES 256: 256-bits with 14 rounds.
- AES was extensively studied, and no vulnerability have been discovered.

## Overview of AES

![Screenshot 2023-06-07 at 10.31.15 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.31.15_PM.png)

## Round of AES

![Screenshot 2023-06-07 at 10.32.49 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.32.49_PM.png)

## SubBytes

![Screenshot 2023-06-07 at 10.33.36 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.33.36_PM.png)

## ShiftRows

![Screenshot 2023-06-07 at 10.34.28 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.34.28_PM.png)

## MixColumns

![Screenshot 2023-06-07 at 10.35.30 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.35.30_PM.png)

## AddRoundKey

![Screenshot 2023-06-07 at 10.36.11 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.36.11_PM.png)

# Arithmetic of AES

![Screenshot 2023-06-07 at 10.37.23 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.37.23_PM.png)

![Screenshot 2023-06-07 at 10.40.06 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.40.06_PM.png)

![Screenshot 2023-06-07 at 10.41.58 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.41.58_PM.png)

![Screenshot 2023-06-07 at 10.43.27 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.43.27_PM.png)

![Screenshot 2023-06-07 at 10.43.50 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.43.50_PM.png)

![Screenshot 2023-06-07 at 10.45.11 PM.png](2_Symmetric-Key%20Cryptography%20I%203282fb86eb2647188bb6a9ef5350f1f9/Screenshot_2023-06-07_at_10.45.11_PM.png)