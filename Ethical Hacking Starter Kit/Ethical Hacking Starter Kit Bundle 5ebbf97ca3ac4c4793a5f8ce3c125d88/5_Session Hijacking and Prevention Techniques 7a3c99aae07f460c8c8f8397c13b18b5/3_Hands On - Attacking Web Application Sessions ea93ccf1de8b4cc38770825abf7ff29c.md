# 3_Hands On - Attacking Web Application Sessions

# Cookies Exploitation with XSS

![Screenshot 2023-05-29 at 3.21.28 PM.png](3_Hands%20On%20-%20Attacking%20Web%20Application%20Sessions%20ea93ccf1de8b4cc38770825abf7ff29c/Screenshot_2023-05-29_at_3.21.28_PM.png)

### Example 1 - Cross-Site Scripting (XSS) attacks

```
site.com/phpcookiexss/site/?error= <script> alert(1)</script>

```

This URL can be used for testing the vulnerability of a web application to Cross-Site Scripting (XSS) attacks.
If the web application is vulnerable to XSS attacks, an attacker can inject malicious code into the page and execute it in the context of the victim's browser, potentially allowing the attacker to steal sensitive information or take control of the victim's account.

### Example 2 - cookie exploitation attack

The URL `hackit.com/phpcookiexss/site/?error=<script> alert (document.cookie)</script>` is an example of a cookie exploitation attack using XSS. If the web application is vulnerable to this type of attack, an attacker can inject malicious code into the page and execute it in the context of the victim's browser. The injected code can steal the victim's cookies, which may contain sensitive information such as login credentials or session tokens. Once the attacker has access to the victim's cookies, they can use them to authenticate themselves as the victim and gain access to the victim's account on the web application. This attack can be prevented by properly validating and sanitizing user input, as well as using secure cookies with the HttpOnly and Secure flags set.

### Example

![Screenshot 2023-05-29 at 3.31.11 PM.png](3_Hands%20On%20-%20Attacking%20Web%20Application%20Sessions%20ea93ccf1de8b4cc38770825abf7ff29c/Screenshot_2023-05-29_at_3.31.11_PM.png)

# Session Fixation

## Session Fixation Attack

A session fixation attack is another type of attack that can be used to exploit web applications. In this type of attack, an attacker tricks a user into using a predetermined session ID, which the attacker can then use to hijack the user's session. The attacker can then use the hijacked session to perform actions on behalf of the user, potentially resulting in the theft of sensitive information or the unauthorized modification of the user's data.

To prevent session fixation attacks, web applications should generate a new session ID for each user upon login. Additionally, session IDs should be invalidated upon logout or after a certain period of inactivity. Proper session management is critical to the security of web applications, and should be a top priority for developers and security professionals.

![Screenshot 2023-05-29 at 3.35.24 PM.png](3_Hands%20On%20-%20Attacking%20Web%20Application%20Sessions%20ea93ccf1de8b4cc38770825abf7ff29c/Screenshot_2023-05-29_at_3.35.24_PM.png)

![Screenshot 2023-05-29 at 3.36.03 PM.png](3_Hands%20On%20-%20Attacking%20Web%20Application%20Sessions%20ea93ccf1de8b4cc38770825abf7ff29c/Screenshot_2023-05-29_at_3.36.03_PM.png)

# Session IDs manipulation with Brute Force Attack

Session IDs manipulation with Brute Force Attack is a type of attack where an attacker attempts to guess the session ID of a user by trying a large number of possible values. The attacker may use automated tools to generate and submit session ID values in an attempt to find a valid one. Once a valid session ID is found, the attacker can use it to hijack the user's session, potentially allowing them to perform actions on behalf of the user.

To prevent session ID manipulation attacks, web applications should use session IDs that are long, random, and difficult to guess. Additionally, session IDs should be invalidated after a certain period of inactivity or upon logout. Proper session management is critical to the security of web applications, and should be a top priority for developers and security professionals.

Burp Suite can intercept and modify HTTP requests to try a large number of possible session ID values in an attempt to find a valid one, allowing attackers to hijack the user's session. Additionally, Burp Suite includes a scanner that can be used to automatically detect and exploit vulnerabilities in web applications related to session management. It is a powerful tool for security professionals and developers who want to ensure the security of web applications.

![Screenshot 2023-05-30 at 3.42.19 PM.png](3_Hands%20On%20-%20Attacking%20Web%20Application%20Sessions%20ea93ccf1de8b4cc38770825abf7ff29c/Screenshot_2023-05-30_at_3.42.19_PM.png)

# Session Donation

Session donation is a type of attack where an attacker donates their own session to a victim, allowing the victim to take over the attacker's session. This can be done by manipulating the session ID or by other means. Once the victim has taken over the attacker's session, they can perform actions on behalf of the attacker, potentially leading to the theft of sensitive information or the unauthorized modification of the attacker's data. This attack can be prevented by properly validating and sanitizing user input, as well as using secure session management techniques such as generating a new session ID for each user upon login and invalidating session IDs after a certain period of inactivity.

![Screenshot 2023-05-30 at 3.47.04 PM.png](3_Hands%20On%20-%20Attacking%20Web%20Application%20Sessions%20ea93ccf1de8b4cc38770825abf7ff29c/Screenshot_2023-05-30_at_3.47.04_PM.png)

# MITB (Man in the Browser) - Malware

## Man-In-The-Browser

© Man-in-the-Browser is a client-side MITM attack, adversaries will exploit vulnerabilities in a victim's web browser to gain partial or full control.

© Having control over the browser, using man-in-the-middle it is very hard to distinguish legitimate client behavior from the attacker's injected malicious activity.

- Common attack vectors are:
    - Browser Extension
    - API Hooking
    - Malicious Content Script

## Lab

BeEF (Browser Exploitation Framework) is a powerful tool for performing Man-In-The-Browser (MITB) attacks. It allows attackers to take control of a victim's web browser and execute commands on their behalf. BeEF includes a wide range of modules for performing various types of attacks, including XSS, CSRF, and file upload vulnerabilities. It can be used to gather sensitive information, such as login credentials and session tokens, from victims. BeEF is a popular tool among penetration testers and security researchers, as well as malicious actors. However, it is important to note that using BeEF for malicious purposes is illegal and can result in severe legal consequences. 

[https://www.youtube.com/watch?v=EL96fXFNLNA](https://www.youtube.com/watch?v=EL96fXFNLNA)

![Screenshot 2023-05-30 at 3.59.10 PM.png](3_Hands%20On%20-%20Attacking%20Web%20Application%20Sessions%20ea93ccf1de8b4cc38770825abf7ff29c/Screenshot_2023-05-30_at_3.59.10_PM.png)