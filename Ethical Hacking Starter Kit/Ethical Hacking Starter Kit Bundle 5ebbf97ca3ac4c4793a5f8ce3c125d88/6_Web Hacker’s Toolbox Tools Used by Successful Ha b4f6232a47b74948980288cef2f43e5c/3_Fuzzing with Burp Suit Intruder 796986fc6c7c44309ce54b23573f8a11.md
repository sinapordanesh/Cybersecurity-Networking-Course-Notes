# 3_Fuzzing with Burp Suit Intruder

# The Basics of Fuzzing

- Semi-automated vulnerability detection technique
- Fuzzing: automated attack + manual verification
- 1. Automated attack (Burp Suite Intruder)
- 2. Manual verification:
find anomalies (length of response, time of response, ...)
- 3. Vulnerability: Yes / No

# Fuzzing with Burp Suit Intruder

- Burp Suite Intruder is a part of Burp Suite
- Burp Suite: an integrated platform for web application security testing
- Burp Suite Intruder is used for fuzzing
- 1. Payload position
- 2. List of payloads
- 3. Attack type: sniper
- Where can I find a list of payloads?
- `/us/share/wfuzz/wordlist/Injections` (Kali Linux)

## Demo

Here are the steps to perform SQL injection fuzzing through the search bar using Burp Suite:

1. Open Burp Suite and go to the "Proxy" tab.
2. Configure your browser to use Burp Suite as a proxy.
3. Visit the website that you want to test.
4. Perform a search through the search bar.
5. In Burp Suite, go to the "Proxy" tab and find the request for the search.
6. Right-click on the request and select "Send to Intruder."
7. In the Intruder tab, select the "Positions" tab and click on "Clear."
8. Highlight the search parameter in the request and click on "Add" to add it as a position.
9. Go to the "Payloads" tab and select "Payload type" as "Simple list."
10. In the "Payload options" section, click on "Load" and select a wordlist for SQL injection (such as `/usr/share/wfuzz/wordlist/Injections/sql.txt`).
11. Go to the "Options" tab and select "Sniper" as the attack type.
12. Click on "Start attack" to begin the SQL injection fuzzing.
13. Check the responses for **anomalies** such as error messages or delays. If there are any anomalies, investigate further for potential SQL injection vulnerabilities.

# Fuzzing for Path Traversal

Here are the steps to perform path traversal injection fuzzing through a URL parameter using Burp Suite:

1. Open Burp Suite and go to the "Proxy" tab.
2. Configure your browser to use Burp Suite as a proxy.
3. Visit the website that you want to test.
4. Identify the URL parameter that you want to test for path traversal injection.
5. In Burp Suite, go to the "Proxy" tab and find the request with the URL parameter.
6. Right-click on the request and select "Send to Intruder."
7. In the Intruder tab, select the "Positions" tab and click on "Clear."
8. Highlight the URL parameter in the request and click on "Add" to add it as a position.
9. Go to the "Payloads" tab and select "Payload type" as "Simple list."
10. In the "Payload options" section, click on "Load" and select a wordlist for path traversal injection (such as `/usr/share/wfuzz/wordlist/Injections/traversal.txt`).
11. Go to the "Options" tab and select "Sniper" as the attack type.
12. Click on "Start attack" to begin the path traversal injection fuzzing.
13. Check the responses for **anomalies** such as directory listings or sensitive file contents. If there are any anomalies, investigate further for potential path traversal vulnerabilities.

Remember to use this technique only on systems that you have permission to test.

# Fuzzing with Burp Suit Intruder - Tips and Tricks

## Throttle

When performing fuzzing with Burp Suite Intruder, consider the impact of the attack on the target system. To avoid overwhelming the system and causing it to crash, you can use the "Throttle" function in Burp Suite Intruder.

To enable Throttling in Burp Suite Intruder, go to the "Options" tab in the Intruder tab and select "Throttle requests". Set the desired number of requests per second for a balance between attack speed and system stability.

## Grep-Match

When fuzzing with Burp Suite Intruder, you can use the "Grep-Match" function to search for specific strings in the response. This can help you to quickly identify responses that contain interesting information, such as error messages or sensitive data.

To use Grep-Match in Burp Suite Intruder, go to the "Payloads" tab in the Intruder tab and select "Payload processing". Click on "Add" and select "Grep - Match". Enter the string that you want to search for in the response, and select whether you want the search to be case-sensitive or not.

When you run the attack, Burp Suite Intruder will highlight any responses that contain the string that you specified. This can help you to quickly identify potentially interesting responses and investigate them further.