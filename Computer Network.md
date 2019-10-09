## Five Layer Referenced Model

- Application Layer
- Transport Layer
- Network Layer
- DataLink Layer
- Physical Layer

### Physical layer
The two devices are connected with through a physical medium. The physical medium is used to transfer an electrical or optical signal between two directly connected devices.

The types of physical mediums contains: 

- electrical cable. Information can be transmitted over different type of electrical cables.
- optical fiber. Optical fibers are usually used in public and enterprise networks when the distance between the communication devices is larger than one kilometer.
- wireless. A radio signal is used to encode the information between the communicating devices. Many types of modulation techniques are used to send information over a wireless channel. 

### Datalink layer
The datalink layer builds on the service provided by the underlying physical layer.

The datalink layer allow the two hosts that are directly connected through the physical layer to exchange information.
The unit of information exchanged between two entities in the datalink layer is frame.

### Network layer
If it is necessary to exchange information between hosts that are not attached to the same physical medium, the task of the network layer comes. The network layer is built above the datalink layer.

Network layer entities exchange packets. A packet is a finite sequence of bytes that is exchanged by the datalink layer inside one or more frames.

### Transport layer
Most realizations of network layer, including the internet, do not provide a reliable service. To ensure the reliable delivery of data produced by applications is the task of transport layer.

Transport layer entities exchange segments. A segment is a finite sequence that are transported inside one or more packets. 

There are different types of transport layers. 
- The most widely used on the internet is TCP which provides a reliable connection-oriented byte-stream transport service.
- UDP provides an unreliable connection-less transport service.

### Application layer 
The upper layer of the architecture is the Application layer . This layer includes all the mechanism and data structs that are necessary for the applications. The ADU(Application Data Unit) is used to indicate data exchanged between two entities of the Application layer.



## OSI reference model 
The OSI reference model refine the application layer in the five reference layer model into three new layers.
- Session layer.  
The session layer contains the protocols and mechanisms that are necessary to organize and to synchronize the dialogue and to manage the data exchange of presentation layer entities.  
The objective of session layer is to hide the possible failure of transport-level connections to the upper layer higher.
- Presentation layer.  
The presentation layer is designed to cope with the different ways of representing information of computers.  
To solve this problem, the representation layer provides for a common representation for the data transferred.
- Application layer.   
the Application layer that contains the mechanisms that do not fit in neither the Presentation nor the Session
layer. The OSI Application layer was itself further divided in several generic service elements.

The OSI reference model place the session and representation layers implicitly in the application layer. The main motivation of it is to simplify the upper layers.

## Application Layer
___

The application layer is the most important and most visible layer in computer networks. Application resides in this layer and human users interact via those application through the network.


There are two important models used to organize a networked application.
- The first and oldest model is the client-server model.
    - This model is highly asymmetrical: clients send requests and servers perform actions and return response.
    - Network do not exchange random messages. In order to ensure that server is able to understand the queries sent by a client and also the client understand the responses from the server. They must protect a set of syntatical and semantic rule which is called an application-level protocol.
    - There are two types of rule that define how information exchanges between two computers.
        - syntatical rules that precisely define the format of messages that are exchanged.
        - organization of the information flow. For many applications, the flow of information must be structured and there are precedence relationship between the different types of information.

- In the peer to peer model, all hosts act as both server and client and they play both roles.

- The transport service   
    There are two main types of transport services.
    - the connectionless or datagram service
    - the connection-orientated or byte-stream service.
      
    The connectionless service allows applications to exchange messages or Service Data Units. The connectionless transport service on the internet is unreliable, but it is able to detect transmission errors.

    The second transport service is the connection-orientated service and the service is always called byte-stream service on the internet. Like the datagram service, the networked application that use the byte-stream service are identified by the host on which they run and a port number.

- Application Layer Protocol
    - The Domain Name System
        - The first solution that allowed applications to use name was the hosts file. It contains the mapping between the name of each internet host and its associated IP address.
        - The hierachical naming scheme is a key component of the *Domain Name System(DNS)*. The DNS is a distributed database that contains mapping between fully qualified domain names and IP addresses.
        - A *nameserver* that is responsible for domain dom can directly answer the following queries:
            - the IP address of any host residing directly inside domain dom.
            - the nameserver that are responsible for any directly subdomain of domain dom.

        - Each root nameserver maintain a list of all the name servers that are responsible for each of the top-level domain names and their IP addresses.
        - A resolver is a server that provides the name resolution server for a set of clients.
        - The DNS protocol runs above both the datagram service and the byte-stream service.
        - DNS messages are composed of five parts that are named sections(The first three sections are mandatory and last two sections are optional)
            - The first section is *Header*. It contains the information about the type of message and the content of other sections.
            - The second section contains the *Question* sent to the name server or resolver.
            - The third section contains *Answer to Question*.
            - The fourth section, named Authority, contains information about the servers that can provide an  authoritative answer if required.
            - The last section contains the additional information.

    - Electronical mail
        - The email system that we consider in this book is composed of *four components*.
            - Message format. (It defines how the email is encoded).
            - protocol. (To allow the exchange of message between host and servers)
            - client software.
            - server software.
        - MIME(Multipurpose Internet Mail Extensions)
            - These extensions were carefully designed to allow Internet email to carry non-ASCII characters and binary files without breaking the email servers that were deployed at that time.
    - SMTP(Simple Mail Transfer Protocol)
        - The SMTP specification distinguishes between five types of processes involved in the delivery of mail message. 
    
    - Hypertext Transfer Protocol
        - A document sharing system such as world wide web is composed of three important parts.
            - A standard addressing scheme that allows a unambiguous identification of document.
            - A standard document format: the Hypertext Markup Language.
            - A standard protocol that facilitates efficient retrieval of documents stored on a server.

        - HTTP is a text-based protocol, in which the client sends a request and the server returns a response.
            - Each HTTP request contains three parts.
                - Method. It indicates the type of request, a URI, and the version of the HTTP protocol used by the client.
                - Header. It is used by the client to specify optional parameters for the request.
                - A optional MIME document attached to the request.
            
            - Response sent by the server also contains three parts.
                - A status line.
                - A header.
                - A MIME document.

        - As the web evolved to support richer documents, opening a TCP connection for each URI become a performance problem.   Forcing the client to open a TCP connection for each component of a web page has two drawbacks.
            - the client and server must to exchange packets to open and close a TCP connection.
            - A large number of established TCP connections may be a performance bottleneck on servers.
            - HTTP 1.1 solved this problem by supporting persistent TCP.
                - Connection:


## Transport Layer 
___

- There are two types of network layer services: connectionless and connection-orientated.

- Connectionless network layer service is the most widespread. The characteristics are:
    - It can only transfer SDUs of limited size
    - It may discard SDUs
    - It may corrupt SDUs
    - It may delay, reorder or even duplicate SDUs

- Three types of imperfections that must be considered by the transport layer.
    - Segments can corrupted with transmission error.
    - Segments can be lost.
    - Segments can reorder or duplicated.

- Solutions for different types of imperfection
    - To protect against the transmission error is to add a redundancy to the segment which is sent.
        - The simplest error detection scheme is the checksum. It basically an arithmetic sum of all the bytes that a segment is composed of.
        - CRC(Cyclical Redundancy Checks) are very powerful error detection schemes that are used notably on disks, by many datalink layer protocols and file formats such as zip or png.

    - The simplest solution to deal with the losses of segments is to use a retransmission timer.
        - When the sender sends a segment, the retransmission timer starts. The value of this retransmission timers is the round-trip-time. When the timer expires, the sender assumes the data segments be lost and retransmits it.
        - The sliding window is the set of consecutive sequence numbers that the sender can use when transmitting segments without being forced to wait for acknowledgement. 