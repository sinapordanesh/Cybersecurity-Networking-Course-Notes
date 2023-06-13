# 4_Filtering Packet and Packet Dissection

# Filtering Techniques

## Wireshark `Manage Capture Filters` Window

![Screenshot 2023-06-05 at 3.38.28 PM.png](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/Screenshot_2023-06-05_at_3.38.28_PM.png)

![Screenshot 2023-06-05 at 3.37.46 PM.png](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/Screenshot_2023-06-05_at_3.37.46_PM.png)

In Wireshark, you can create and manage capture filters using the Manage Capture Filters window. These filters capture packets that match specific criteria, like protocol or source IP address.

To open the Manage Capture Filters window, go to `Capture > Options > Capture Filters`. Here, you can create, edit, and delete filters.

When creating a new filter, choose from criteria like protocol, IP address, and port number. Save filters for future use.

Capture filters reduce the amount of data captured, making analysis and troubleshooting easier. Use them carefully to avoid missing important packets that could help diagnose network issues.

Here are some examples of creating new capture filters and their syntax:

- To capture only ICMP packets, use `icmp` as the filter expression.
- To capture only packets that originate from a specific IP address, use `src host [IP address]`.
- To capture only packets that are destined for a specific IP address, use `dst host [IP address]`.
- To capture only packets that use a specific protocol, use `proto [protocol name]`.
- To capture only packets that use a specific port, use `port [port number]`.
- 

In addition to the capture filters mentioned earlier, Wireshark also supports the following filters:

- **Scope**:
    - To capture packets from a specific host, use `host [host name]`.
    - To capture packets from a specific network, use `net [network address/mask]`.
    - To capture packets from a specific port range, use `portrange [start port]-[end port]`.
- To capture packets in a specific **direction**, use `src [host name]` for outgoing packets **or** `dst [host name]` for incoming packets.
- To capture packets of a specific **protocol**, use `ether`, `wlan`, `ip`, `ip6`, `arp`, or `rarp`.

Remember that the syntax for creating filters can vary depending on the protocol or type of packet you want to capture. Be sure to consult the Wireshark documentation for a full list of available filters and their syntax.

Remember, the syntax for creating filters can vary depending on the protocol or type of packet you want to capture. Be sure to consult the Wireshark documentation for a full list of available filters and their syntax.

## Analyzing an Example

[http_with_jpegs.cap](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/http_with_jpegs.cap)

### Search Bar Samples

- `http.request.method == GET`
- `http.request.method == POST`
- `(http.response_number == 1) && (http.response.code == 200)` filters packets to show only those with an HTTP response code of 200 and a response number of 1.
- `http.server contains "Apache"` filters packets to show only those with an HTTP server containing the word "Apache".
- `(upper(http.server) contains "Apache")` filters packets to show only those with an HTTP server containing the word "Apache", regardless of capitalization.
- `(http.server matches "Apache")` filters packets to show only those with an HTTP server matching the regular expression "Apache".
- To capture packets that use TCP ports 80, 443, or 8080, use `tcp.port in {80, 443, 8080}` as the filter expression.

### Point

The `Prepare as filter` option allows you to create a capture filter based on a display filter. This is useful if you have already found a set of packets in your capture, and you want to create a filter to capture similar packets in the future.

The `Apply as filter` option allows you to create a display filter based on a selected packet. This is useful if you want to focus on a specific packet or set of packets in your capture, and create a filter to display only those packets.

# Protocol Details and Analysis

## Packet Counter

![Screenshot 2023-06-05 at 4.07.40 PM.png](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/Screenshot_2023-06-05_at_4.07.40_PM.png)

![Screenshot 2023-06-05 at 4.07.52 PM.png](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/Screenshot_2023-06-05_at_4.07.52_PM.png)

To view HTTP statistics in Wireshark, navigate to `Statistics > HTTP > Requests`. Here, you can see a breakdown of all HTTP requests in the capture, including the total number of requests and the percentage of HTTP traffic in the capture. This information can be useful for analyzing the HTTP traffic in a capture and identifying potential issues or areas of interest.

## Request

![Screenshot 2023-06-05 at 4.13.07 PM.png](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/Screenshot_2023-06-05_at_4.13.07_PM.png)

![Screenshot 2023-06-05 at 4.09.00 PM.png](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/Screenshot_2023-06-05_at_4.09.00_PM.png)

The **Requests** page in Wireshark provides detailed information about HTTP requests in the capture, including the total number of requests and the percentage of HTTP traffic. Unlike a packet **counter page**, which provides a generalized overview of all packet types, the Requests page focuses specifically on HTTP traffic and provides more detailed information about the types and sequences of requests made. It is a valuable tool for analyzing and troubleshooting issues related to HTTP requests.

## Request Sequences

![Screenshot 2023-06-05 at 4.10.36 PM.png](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/Screenshot_2023-06-05_at_4.10.36_PM.png)

![Screenshot 2023-06-05 at 4.10.56 PM.png](4_Filtering%20Packet%20and%20Packet%20Dissection%200e7f1c9267cc42489490fd56ce15908d/Screenshot_2023-06-05_at_4.10.56_PM.png)

To view HTTP statistics, navigate to `Statistics > HTTP > Requests Sequence`. Here, you can see a breakdown of all HTTP requests in the capture, including the number of requests, the average response time, and the response codes received. This information can be useful for identifying patterns or issues in HTTP traffic.

# Finding and Colouring Packets

# Exporting Objects