---
title: "Understanding the OSI Model: A Beginner's Guide with WhatsApp Examples 📱💬"
seoTitle: "OSI Model Explained with WhatsApp Examples"
seoDescription: "Beginner’s guide to the OSI model using WhatsApp examples, covering layers and protocols for better network communication understanding"
datePublished: Sun Jul 07 2024 17:27:43 GMT+0000 (Coordinated Universal Time)
cuid: clybttlra00010am5dgr209rt
slug: understanding-the-osi-model-a-beginners-guide-with-whatsapp-examples
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720373195956/b6eb5cd7-ce12-486a-9bdf-4bca66d5d410.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720373225933/bdf03108-d062-407b-8173-ea5963e221d1.png
tags: computer-science, devops, networking, 90daysofdevops, trainwithshubham

---

## • What is OSI model ?

The OSI (Open Systems Interconnection) model is a way to understand how different parts of a computer network communicate with each other. It breaks down the communication process into seven layers, each with a specific role.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720372489516/2c3f054b-9dec-4f53-8156-ac4e6d17fb90.png align="center")

1. **Application Layer**: Anand types his message in the WhatsApp application and hits send. The message is then displayed in Riya's WhatsApp application. This layer is responsible for the actual user interface and the protocols that allow the app to function.
    
2. **Presentation Layer**: The message is encrypted on Anand's phone to ensure privacy and then decrypted on Riya's phone. This layer ensures that the data is in a readable format for both users.
    
3. Session Layer: WhatsApp establishes a session between Anand and Riya. This session keeps track of the ongoing conversation, ensuring that messages are exchanged in a synchronized manner. You can observe this in WhatsApp when both users are online, indicating that a session has been created.
    
4. Transport Layer: This layer ensures that the message is delivered reliably and in the correct order. If any packets are lost or corrupted during transmission, this layer will request retransmission. It is the heart of ensuring data integrity and proper sequencing.
    
5. **Network Layer**: The message from Anand's phone is broken into packets and routed through various network devices like routers and switches to reach Riya's phone. This layer ensures that the packets take the best path to reach their destination.
    
6. **Data Link Layer**: When Anand sends a message, his phone's network interface card (NIC) ensures that the data is correctly formatted and error-free before it is sent over the network. Similarly, Riya's phone does the same when receiving the message.
    

**Physical Layer**: Anand and Riya both have smartphones connected to the internet via Wi-Fi or mobile data. The physical layer includes the actual hardware like their phones, Wi-Fi routers, and network cables.

## • What is TCP ?

TCP (Transmission Control Protocol) is a key protocol in the Transport Layer of the OSI model. It ensures that data sent over a network is delivered reliably and in the correct order.

Imagine you want to send a long letter to a friend, but you can only send it in small pieces (like postcards). TCP works like a system that numbers each postcard and keeps track of which ones have been sent and received. If any postcard gets lost or damaged, TCP will notice and ask for it to be sent again. Once all the postcards are received, TCP puts them back together in the correct order to form the complete letter.

**Example**:

Anand wants to send a large photo to Riya via WhatsApp. Here’s how TCP helps:

1. **Breaking Down Data**: TCP breaks the photo into smaller packets.
    
2. **Numbering Packets**: Each packet is numbered so they can be reassembled in the correct order.
    
3. **Sending Packets**: The packets are sent over the network to Riya.
    
4. **Checking Delivery**: TCP checks if all packets have been received. If any are missing or corrupted, it requests those specific packets to be resent.
    
5. **Reassembling Data**: Once all packets are received, TCP puts them back together to form the complete photo, which Riya can then view.
    

This process ensures that the photo is delivered accurately and completely, even if some packets encounter issues during transmission.

## • What is UDP ?

UDP (User Datagram Protocol) is another key protocol in the Transport Layer of the OSI model. Unlike TCP, UDP is simpler and faster but does not guarantee reliable delivery or the correct order of data packets.

Imagine you are throwing a series of paper airplanes with messages to a friend across a field. You throw them as quickly as possible without checking if your friend catches each one or if they arrive in the correct order. Some airplanes might get lost or arrive out of order, but the process is very fast.

**Example**:

Anand wants to stream a live video to Riya. Here’s how UDP helps:

1. **Sending Data Quickly**: UDP sends video data packets from Anand’s phone to Riya’s phone as quickly as possible.
    
2. **No Numbering or Checking**: Unlike TCP, UDP does not number the packets or check if they are received correctly. It just keeps sending the data.
    
3. **Handling Loss**: If some packets are lost or arrive out of order, the video might have small glitches, but the stream continues without delay.
    

This process is ideal for applications like live video streaming or online gaming, where speed is more important than perfect accuracy.