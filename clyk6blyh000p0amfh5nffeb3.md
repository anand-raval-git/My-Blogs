---
title: "Exploring the TCP/IP Model, ARP, and RARP 🌐📡"
seoTitle: "TCP/IP Model: ARP and RARP Explained"
seoDescription: "Overview of TCP/IP model, ARP, and RARP with relatable examples for easier understanding of network communication processes"
datePublished: Sat Jul 13 2024 13:39:48 GMT+0000 (Coordinated Universal Time)
cuid: clyk6blyh000p0amfh5nffeb3
slug: exploring-the-tcpip-model-arp-and-rarp
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720806059812/c1688a0c-3706-481c-a45d-119a1d1d9a47.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720806094976/cb7dcd76-9506-491f-b909-3c92a64506fe.png
tags: devops, tcp, computernetwork, 90daysofdevops, trainwithshubham

---

## • What is tcp/ip model ?

The TCP/IP model is a framework used to understand how data is transmitted over the internet. It consists of four layers: the Network Access Layer, the Internet Layer, the Transport Layer, and the Application Layer. To make this concept more relatable, let's use an example involving Anand and Riya chatting on WhatsApp.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720805461071/c0216bce-d8ba-48ae-87c8-2e2611a3b66d.avif align="center")

### 1\. Network Access Layer

Imagine Anand wants to send a message to Riya. The Network Access Layer is like the physical delivery system. It ensures that the data (message) can travel over the physical network, whether it's through Wi-Fi, Ethernet, or mobile data. Think of it as the postal service that picks up the letter from Anand's house.

### 2\. Internet Layer

Next, the Internet Layer is responsible for routing the message from Anand's phone to Riya's phone. It assigns IP addresses to both devices and determines the best path for the message to travel. This is similar to the postal service sorting the letter and deciding the best route to deliver it to Riya's address.

### 3\. Transport Layer

The Transport Layer ensures that the message is delivered reliably and in the correct order. It breaks the message into smaller packets, sends them, and ensures they are reassembled correctly on Riya's phone. This is like the postal service ensuring that if the letter is too big, it is divided into smaller envelopes, sent separately, and then reassembled correctly at Riya's end.

### 4\. Application Layer

Finally, the Application Layer is where Anand and Riya interact with the WhatsApp application. This layer handles the actual communication between the WhatsApp apps on both phones, ensuring that Anand's message appears correctly in Riya's chat window. It's like Riya opening the letter and reading the message from Anand.

By breaking down the process into these layers, the TCP/IP model ensures that data can be transmitted efficiently and reliably across different types of networks.

## • What is ARP ?

The Address Resolution Protocol (ARP) is like a phone book for computers on a local network. Imagine you want to send a letter to your friend, but you only know their name, not their address. You need to look up their address in a phone book to send the letter.

In a similar way, when one computer wants to send data to another computer on the same network, it needs to know the physical address (like a home address) of the other computer. This physical address is called a MAC address. However, the computer only knows the IP address (like knowing just the name).

ARP helps by asking all the computers on the network, "Who has this IP address?" The computer with that IP address responds with its MAC address. Now, the first computer can send the data to the correct physical address.

So, ARP is a simple way for computers to find out each other's physical addresses so they can communicate on the same network.

## • What is RARP ?

The Reverse Address Resolution Protocol (RARP) is like a reverse phone book for computers on a local network. Imagine you have a letter with an address but you don't know the name of the person who lives there. You need to find out the name to know who the letter is for.

In a similar way, when a computer knows its own physical address (MAC address) but doesn't know its IP address, it uses RARP to find out. The computer sends a request to a special server on the network, asking, "What is my IP address?" The server looks up the MAC address and responds with the corresponding IP address.

So, RARP helps computers find out their own IP addresses when they only know their physical addresses, allowing them to communicate on the network.

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>