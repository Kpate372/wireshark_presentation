# Wireshark - a boring network analyzing tool?

Labeled by Aleks as a "rather standard" tool with "not much application in hacking", we had a hard time proving the opposite. There are a few astonishing, easy to exploit weaknesses of broadcasting networks that can be made visible and it is a great tool to look for a starting point for hacking. So, let's dive into it!

## What is Wireshark?

Wireshark is a complete package filled with network analysis tools. Wireshark is not only a packet sniffer but also a packet analyzer, password hacker, and a firewall. It can also detect any denial of service attack on your network and can identify possible hacker. Wireshark is also used sometimes as a tool to detect if anyone is spying on you. 

#### Capturing packets
By selecting the name of interface on the opening window we can see the packets captured on screen and packets captured by wireshark are in real time.The packets are captured as shown ![image](https://linuxsecurityblog.files.wordpress.com/2016/08/wireshark-packets-2.png?w=569&h=337&zoom=2)

#### Filtering packets
Filtering is used to identify a specific packet. For example, you can filter a traffic received by your browser or from an application. You can also filter packets going through protocols such as DNS, HTTP or TCP. How the packets can be filtered is shown. ![Filter](https://linuxsecurityblog.files.wordpress.com/2016/08/packrts-filter.png?w=569&h=396&zoom=2). By clicking on packets and selecting follow stream will automatically add a filter of that packet and Wireshark will show all the packets related to it.

#### Inspecting packets
Inspecting a packet helps you to analyze its details. This will let you know the origin of the packet and other details. To do so, click on a packet to select it and its details will be shown. ![](https://linuxsecurityblog.files.wordpress.com/2016/08/analyzing-packets1.png?w=569&zoom=2). Right-click on any packet and select filter. This will show all the related packets that have been captured.

## The internet is organized in layers
The OSI model (Open System Interconnection) model defines a computer networking framework to implement protocols in seven layers. A protocol in the networking terms is a kind of negotiation and rule in between two networking entities. The OSI model uses layers to help give a visual description of what is going on with a networking system. OSI model helps to narrow down problems in network, for instance it can show whether it is physical issue or something with the application.  

#### Physical layer

The Physical layer is also called as the Layer 1. Here are the basic functionalities of the Physical layer:

1. Responsible for electrical signals, light signal, radio signals etc.
2. Hardware layer of the OSI layer.
3. Devices like repeater, hub, cables, ethernet work on this layer.
4. Protocols like RS232, ATM, FDDI, Ethernet work on this layer.

#### Data Link layer

The data link layer is also called as the Layer 2 of the OSI model. Here are the basic functionalities of the data link layer:

1. Responsible for encoding and decoding of the electrical signals into bits.
2. Covers electrical signals into frames
3. The data link layer is divided into two sub-layers
     - The Media Access Control (MAC) layer
     - Logical Link Control LLC layer.
4. The MAC sub layer controls how a computer on the network gains access to the data and permission to transmit it.
5. The LLC layer controls frame synchronization, flow control and error checking.
6. Devices like ethernet work at this layer

#### Network Layer

The Network layer is also called as the layer 3 of the OSI model. Here are the basic functionalities of the network layer:

1. Switching and routing technologies work here.
2. Creates logical paths between two hosts across the world wide web called as virtual circuits.
3. Routes the data packet to destination.
4. Internet working, error handling, congestion control and packet sequencing work at this layer.
5. Different network protocols like IP, IPX, AppleTalk work at this layer.

#### Transport layer

The Transport  layer is also called as the layer 4 of the OSI model. Here are the basic functionalities of the Transport layer:

1. Responsible for the transparent transfer of data between end systems
2. Responsible for end-to-end error recovery and flow control
3. Responsible for complete data transfer.
4. Protocols like SPX, TCP, UDP work here.

#### Session layer

The Session  layer is also called as the layer 5 of the OSI model. Here are the basic functionalities of the Session layer:

1. Responsible for establishment, management and termination of connections between applications.
2. The session layer sets up, coordinates, and terminates conversations, exchanges, and dialogues between the applications at each end.
3. It deals with session and connection coordination.
4. Protocols like NFS, NetBios names, RPC, SQL work at this layer.

#### Presentation layer

The Presentation layer is also called as the layer 6 of the OSI model. Here are the basic functionalities of the presentation layer:

1. Responsible for data representation on your screen
2. Encryption and decryption of the data.
3. Data semantics and syntax.
4. Layer 6 Presentation examples include encryption, ASCII, EBCDIC, TIFF, GIF, PICT, JPEG, MPEG, MIDI.

#### Application Layer

The Application layer is also called as the layer 7 of the OSI model. Here are the basic functionalities of the Application layer:

1. Application layer supports application, apps, and end-user processes.
2. Quality of service.
3. This layer is responsible for application services for file transfers, e-mail, and other network software services.
4. Protocols like Telnet, FTP, HTTP work on this layer.


![imagecantbefound](https://github.com/sbleh/wireshark_presentation/blob/master/layersInWirehark.JPG?raw=true)



## Wireshark in the context of HACKING
Since Wireshark is basically a tool making package traffic in a network visible it is perfectly suitable for exploiting some weaknesses of broadcasting networks like *WiFi*. As you remember: Using *WiFi* is nothing more than just shouting out loud the information you want to share and hoping that the *WiFi router* understands it. For us as hackers this means that we can also just listen and maybe gain some valuable insight. A great starting point for that are unencrypted protocols. In the following two interesting and widely used protocols will be examined.

### issue #1: unencrypted *HTTP*
The *HyperText Transfer Protocol (HTTP)* is a application layer protocol for any data exchange in a client-server communication. It furthermore is a connectionless protocol based on the transport layer protocol *TCP (Transmission Control Protocol)* (often Port 80) and is therefore not encrypted. Information is exchanged in a stateless request and response cycle. Important request methods are `GET`, `POST` and `PUT` while for example `200 OK` is the most common response message. If you want to refresh your knowledge on *HTTP* you can find a great and short explanation in this [video](https://www.youtube.com/watch?v=eesqK59rhGA).

The broadcast property of *WiFi* and the unencrypted content of *HTTP* allow hackers to gain confidential data from tracking the sent packages with *Wireshark*. The application of some filters to the packages allows her or him to look for interesting *HTTP* packages. In the following an example is explained in more detail.

#### Tutorial for getting confidential login data from a user of *way2sms.com*

Given a user of *way2sms.com* in your *WiFi* network trying to log in to his account and the hacker simultaneously tracking the traffic of the network allows her or him to read out the user's name and password.

Therefore, the hacker must select the respective network in *Wireshark* and start tracking by pressing the *shark button* in the top left corner. After the victim logged in to *way2sms.com* the hacker can apply some filters to the tracked packages. For example, filtering for the victims *IP adress* (if known) and for all *HTTP* packages will reduce the number of displayed packages. Instead, filtering for the *TCP* port 80 might also help.

```
ip.addr == 192.222.0.20 and http
tcp.port == 80
```

Given all the remaining packages the hacker can check them manually or look for promising packages. In the example of *way2sms.com* a *POST* request can be found. Displaying the package, the user name and password can be extracted easily. 

![imagecantbefound](https://github.com/sbleh/wireshark_presentation/blob/master/httpPOST.JPG?raw=true)

For demonstration purposes the attacker and victim can be simulated on one computer, but it also works for two different agents in the same network.

This is shocking! Without any fancy tools login data can be seen all over the network. So never login somewhere if you are in a public *WiFi*! Never? No. Help is on the way and it is called *HTTP**S***, where the s stands for **security**. It is basically *HTTP* over *SSL (Secure Socket Layer)* and therefore encrypted. The protocol uses a public and private key encryption and is therefore dependent on a *certificate authority*. If you want to understand the idea of *HTTPS* and *SSL* this short [video](https://www.youtube.com/watch?v=4nGrOpo0Cuc) is a great resource.

Today most web services offer a communication over *HTTPS*. *Google* even started marking *HTTP requests* as **NOT SECURE** in its browser *Chrome* ([blog post](https://www.blog.google/products/chrome/milestone-chrome-security-marking-http-not-secure/)). And the trend is clear: More and more services caring about encrypting confidential data and change to *HTTPS* (see on [searchenginewatch.com](https://searchenginewatch.com/2018/04/11/the-state-of-https-in-2018-why-should-you-migrate/)).

### issue #2: unencrypted *DNS*
The *Domain Name System (DNS)* is a protocol within the set of standards for how computers exchange data on the Internet and on many private networks. DNS resolves domain names to *Internet Protocol (IP)* addresses. When a URL is entered into the web browser, the DNS server uses its resources to resolve the domain name into the IP address for the appropriate web server and retrieves the web page. If you want to check out how the *DNS* server works you can find great and quick explanation in this [video](https://www.youtube.com/watch?v=mpQZVYPuDGU).

Most people's DNS queries remain unencrypted while flowing over the internet. The broadcast property of *Wi-Fi* and unencrypted nature of *DNS* allows hackers to get access over the network behaviour and can easily track different users browsing different websites by tracking the sent packages from *WireShark*. The application of some filters to the packages allows hackers to look for interesting observations in *DNS* packages. In the following, an example is expalined in more detail.

![imagecantbefound](https://github.com/sbleh/wireshark_presentation/blob/master/DNSpackets.JPG?raw=true)

```
ip.addr == 192.222.0.20 and dns
```







