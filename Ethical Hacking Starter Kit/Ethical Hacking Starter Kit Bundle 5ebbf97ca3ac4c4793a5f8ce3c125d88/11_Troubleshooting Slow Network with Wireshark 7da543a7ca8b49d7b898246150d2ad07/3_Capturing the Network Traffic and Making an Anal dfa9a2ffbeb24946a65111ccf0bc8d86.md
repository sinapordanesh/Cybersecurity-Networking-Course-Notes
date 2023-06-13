# 3_Capturing the Network Traffic and Making an Analysis

# Different Capture Technique

### the promiscuous mode of capturing

`Promiscuous` mode is a technique used in network packet capturing, including in Wireshark, that allows a network device to intercept and read data packets that are not intended for it. This mode is often used for network monitoring and analysis purposes.

### Capture filter

One technique for capturing network traffic is by using a capture filter in Wireshark. A capture filter allows the user to specify which packets to capture based on certain criteria, such as packet source or destination. This can help reduce the amount of data captured and make analysis more efficient.

## **`Tshark`**

`Tshark` is a command-line tool used for capturing and analyzing network traffic. It is a part of the Wireshark network analysis suite. Tshark is similar to Wireshark, but it can be used directly from the command line, making it a powerful tool for automating network analysis tasks.

**`tshark -i WiFi -w <file directory location>`**

The `tshark` command captures and analyzes network traffic. Here is an explanation of the flags used in the command:

- `-i WiFi`: specifies the interface to capture traffic on. In this case, the interface is `WiFi`. You can replace `WiFi` with the name of the interface you want to capture traffic on.
- `w`: specifies the file to write the captured traffic to. You should replace `<file directory location>` with the desired directory where you want to save the captured data. For example, `w /home/user/captured_data.pcapng`

## Capture remote interface

To capture a remote interface in Wireshark, you can use the `Remote Capture` feature. This allows you to capture network traffic from a remote computer or device. To use this feature, go to `Capture` -> `Options` -> `Remote Capture`. Here, you can specify the IP address and port of the remote system, as well as the interface to capture traffic on. Once you have entered this information, click `Start` to begin capturing traffic from the remote interface.

# Wireshark Interface and OSI Model

![Screenshot 2023-06-05 at 2.43.47 PM.png](3_Capturing%20the%20Network%20Traffic%20and%20Making%20an%20Anal%20dfa9a2ffbeb24946a65111ccf0bc8d86/Screenshot_2023-06-05_at_2.43.47_PM.png)

![Screenshot 2023-06-05 at 2.45.23 PM.png](3_Capturing%20the%20Network%20Traffic%20and%20Making%20an%20Anal%20dfa9a2ffbeb24946a65111ccf0bc8d86/Screenshot_2023-06-05_at_2.45.23_PM.png)

## TLS

![Screenshot 2023-06-05 at 2.48.25 PM.png](3_Capturing%20the%20Network%20Traffic%20and%20Making%20an%20Anal%20dfa9a2ffbeb24946a65111ccf0bc8d86/Screenshot_2023-06-05_at_2.48.25_PM.png)

# Network Traffic Analysis in Practice

## Types Of Network Traffic Analysis

- **Descriptive Analysis**
    - This type of analysis involves summarizing and describing the characteristics of the network and its components.
- **Diagnostic Analysis**
    - This type of analysis involves identifying issues or problems within the network. This can include identifying nodes or edges that are causing bottlenecks or congestion within the network or identifying nodes that are vulnerable to failure or attack.
- **Predictive Analysis**
    - This type of analysis involves using data and statistical techniques to make
    predictions about future behaviour or outcomes within the network.
- **Prescriptive Analysis**
    - Prescriptive analysis is a type of analysis that involves using data and statistical techniques to recommend actions or decisions based on the results of descriptive and predictive analyses.
    
    ## SMB Protocol
    
    The Server Message Block (SMB) protocol is a network file sharing protocol that allows applications on a computer to read and write files and to request services from server programs in a computer network. SMB is used by Microsoft Windows and other operating systems to facilitate file sharing and other network operations. It can be captured and analyzed using techniques such as Wireshark and Tshark.
    
    #