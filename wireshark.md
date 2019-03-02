# Wireshark - a boring network analyzing tool?

Labeled by Aleks as a "rather standard" tool with "not much application in hacking", we had a hard time proving the opposite. There are a few astonishing, easy to exploit weaknesses of broadcasting networks that can be made visible and it is a great tool to look for a starting point for hacking. So, let's dive into it!

## What is Wireshark?
link to wireshark website
link to a list of common filters in wireshark


## The internet is organized in layers
pictures of internet layers

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
screenshots
videos explaining *DNS*

```
ip.addr == 192.222.0.20 and dns
```







