# Wireshark - a boring network analyzing tool?

Labeled by Aleks as a "rather standard" tool with "not much application in hacking", we had a hard time proving the opposite. There are a few astonishing easy to exploit weeknessess of broadcasting networks that can be made visible and it is a great tool to look for a starting point for hacking. So let's dive into it!

## What is Wireshark?
link to wireshark website
link to a list of common filters in wireshark


## The internet is organized in layers
pictures of internet layers

## Wireshark in the context of HACKING
Since Wireshark is basically a tool making package traffic in a network visibile it is perfectly suitable for exploiting some weaknessess of broadcasting networks like WiFi. As you might remember: Using WiFi is nothing more than just shouting out loud the information you want to share and hoping that the WiFi router understands it. For us as hackers this means that we can also just listen and maybe gain some valuable insight. A great starting point for gaining something are unencrypted protocols. In the following two intersting widely used protocols will be examined.

### issue #1: unencrypted *HTTP*
The *HyperText Transfer Protocol (HTTP)* is a widely used application layer protocol for any data exchange in a client-server communication. It furthermore is a connectionless protocol based on the transport layer protocol *TCP* (on Port 80) and is therefore not encrypted. Information is exchanged in a stateless request and response cycle. Important request methods are `GET`, `POST` and `PUT` while for example `200 OK` is the most common response message. If you want to refresh your knowledge on *HTTP* you can find a great and short explaination in this [video](https://www.youtube.com/watch?v=eesqK59rhGA).

The broadcast property of *WiFi* and the unencrypted content of *HTTP* allow hackers to gain confidential data from tracking the sent packages with wireshark. The application of some filters to the packages allows her or him to look for intersting http packages. In the following an example is explained in more detail.

#### Tutorial for getting confidential login data from a user of *way2sms.com*

Given a user of *way2sms.com* in your *WiFi* network trying to log in to his account and the hacker tracking the traffic of the network allows her or him to read out the user's name and password.

Therefore the hacker must select the respective network in wireshark and start tracking by pressing the *shark button* in the top left corner. After the victim logged in to *way2sms.com* the hacker can apply some filters to the tracked packages. For example filtering for the victims *IP adress* (if known) and for all *HTTP* packages. Filtering for the *TCP* port 80 might also help:

```
ip.addr == 192.222.0.20 and http
tcp.port == 80
```

Given all the remaining packages the hacker can check them manually or look for promising packages. In the example of *way2sms.com* a *POST* request can be found. Displaying the package the user name and password can be extracted easily. 

![imagecantbefound](https://github.com/sbleh/wireshark_presentation/blob/master/httpPOST.JPG?raw=true)

For demonstration purposes the attacker and victim can be simulated on one computer but it also works for two different agents in the same network.


way2sms.com exploit, screenshot (khushali)

https (explain, video)
current news and trends


#### tutorial on the exploit (way2sms)



### issue #2: unencrypted dns
screenshots
videos explaining dns

```
ip.addr == 192.222.0.20 and dns
```



[link to google](www.google.com)

![hello](https://github.com/sbleh/wireshark_presentation/blob/master/Capture.JPG?raw=true)






