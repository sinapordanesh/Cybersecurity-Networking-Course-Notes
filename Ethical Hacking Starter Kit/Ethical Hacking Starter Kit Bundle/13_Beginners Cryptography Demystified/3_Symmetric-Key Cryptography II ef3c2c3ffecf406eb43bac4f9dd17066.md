# 3_Symmetric-Key Cryptography II

# Cryptographic Hashing

- Can hash data of arbitrary length.
- Produce a digest (hash) of fixed length (e.g., 256 bits - sha256).

![Screenshot 2023-06-07 at 10.49.10 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_10.49.10_PM.png)

## Properties of
Cryptographic Hashing

![Screenshot 2023-06-07 at 10.50.32 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_10.50.32_PM.png)

## Integrity Check

- Adversary can not find a malicious image s.t.
- sha256(malicious.exe) = sha256(ubuntu-21.10.iso) - resistance to 2nd preimage attack.

![Screenshot 2023-06-07 at 10.51.20 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_10.51.20_PM.png)

## Commitment

- Hiding: Bob is not able to determine Alice's value - resistance to 1st preimage attack.
- Biding: Alice cannot change her commitment - resistance to collisions.
    - Can not find another random' s.t. sha256 (random' || "Scissors*) = sha256 (random || "Rock).d

![Screenshot 2023-06-07 at 10.53.56 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_10.53.56_PM.png)

## Cryptographic Hash Functions

![Screenshot 2023-06-07 at 10.56.18 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_10.56.18_PM.png)

# Message Authentication Codes (MAC)

## Message Integrity

![Screenshot 2023-06-07 at 10.58.51 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_10.58.51_PM.png)

## Message Authentication

![Screenshot 2023-06-07 at 10.59.57 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_10.59.57_PM.png)

## Message Authentication Codes (MAC)

- Functionality: MAC(k, x) = C
- Security:
    - Adversary is unable to forge new messages - unforgeability.

![Screenshot 2023-06-07 at 11.00.28 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_11.00.28_PM.png)

## Unforgettability

- Security: Adversary is unable to forge new messages - unforgeability.
- - data origin authentication and data integrity.

![Screenshot 2023-06-07 at 11.01.47 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_11.01.47_PM.png)

## MAC From CBC

- Take the last encrypted block of the CBC encryption of the message a MAC.
- Security Problems!

![Screenshot 2023-06-07 at 11.02.44 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_11.02.44_PM.png)

## MAC From CBC

![Screenshot 2023-06-07 at 11.04.08 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_11.04.08_PM.png)

## Secure MAC From CBC

![Screenshot 2023-06-07 at 11.07.17 PM.png](3_Symmetric-Key%20Cryptography%20II%20ef3c2c3ffecf406eb43bac4f9dd17066/Screenshot_2023-06-07_at_11.07.17_PM.png)

## MAC From Cryptographic Hashing

- HMAC - RFC 2104:
- ipad and opad are 2 fixed bitstrings.
- ipad consists of B bytes equal to 0x36.
- opad consists of B bytes equal to 0x5c.
- k is hashed (if longer than B).
- k is padded to have exactly B bytes (if shorter than B) -K.
- Compute H(K@opad|H(K®ipad|x)).
- Truncate the result to its T leftmost bytes.