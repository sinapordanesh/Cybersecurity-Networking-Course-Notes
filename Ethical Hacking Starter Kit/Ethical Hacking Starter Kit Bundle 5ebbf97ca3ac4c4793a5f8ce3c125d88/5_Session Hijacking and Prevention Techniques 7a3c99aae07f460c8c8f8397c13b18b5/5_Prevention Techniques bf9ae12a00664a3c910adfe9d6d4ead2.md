# 5_Prevention Techniques

# Securing Web Applications Part 1

## Complex and Strong Session ID

- Session ID provides the unique identity to each session, once generated it should be treated as Passwords. Highly sensitive.
- Should NOT be enumerable. MUST be generated at Random
- Should NOT use only one type characters (Numbers, Alphabets). MUST be a combination of Alphanumeric value.
- The session ID MUST be long enough to prevent brute force attacks

## Avoid URL as Implementation:

- Session ID if implemented as part of URL, will lead to following issues:
- URL if sniffed, will provide attackers access to the session ID.
- Logged in various endpoints (in logs, web browser history and bookmarks, the Referrer header or search engines)
- Use POST method instead of GET
- Use Cookies wherever possible

## Avoid Re-use of Session ID:

- If re-used, session Fixation is one common problem.
- Session ID MUST NOT include any PII as part of it.
- Generate new Session ID once Authenticated.

# Securing Web Applications Part 2

## Cookie Parameters

- HTTP ONLY - The HttpOnly cookie attribute instructs web browsers not to allow scripts access. Only server requires Session to maintain access, client / browser do NOT need access.
- SECURE - The Secure cookie attribute instructs web browsers to only send the cookie through an encrypted HTTPS (SSL/TLS) connection.
- MAX-AGE / EXPIRE - This attribute is used to ensure that the Session ID is not always active but expires within a certain duration.
- SAMESITE / DOMAIN - These two parameters should be defined based on the implementation to ensure which sites need access to the cookie.

# Securing Network using Secure Protocols

## Implement TLS

- Network traffic MUST be protected against Man-in-the-Middle attacks by encrypting the traffic.
- HTTPs MUST be used instead of HTTP.
- FTPs MUST be used instead of FTP.
- IMAP / POP MUST be implemented with SSL / TLS.

## Secure Protocols

- Telnet protocol is a plain text protocol.
- SSH (Secure Shell) MUST be used as an alternative.
- SETP MUST be used instead of FTP.
- VPN access MUST be used when accessing Critical Infrastructures especially while access Open networks.

# Secure Architecture - Design Implementation

## Best Practices

- For all sensitive actions, if possible, generate a new Auth token for actions rather than using Session ID.
- Use Built-in Session Management Implementations for frameworks such as J2EE, PHP, and [ASP.NET](http://asp.net/) technologies.
- Use vs. Accepted Session ID Exchange Mechanisms - Ensure the server accepts only specific types of input for Session ID exchange to avoid attackers feeding the same via alternate channels.

## Best Practices contd.

- HTML5 Web Storage API - secure or sensitive data should not be stored persistently in browser data stores to avoid information leakage on shared systems.
- Session ID MUST be sanitized as any other user input.
- When Using Multiple Cookies, different names MUST be used and both cookies to be validated if valid across the defined scopes.
- User MUST be Re-authenticated before critical actions.
- Wherever possible Session ID MUST be binded with other parameters such as IP, User-Agent etc. to prevent Session Hijacking.

# Course Conclusion - Summary

## Best Practices

- Kali Linux
- Cyber Security on Cloud Interface
- Secure Coding
- Thread Modelling