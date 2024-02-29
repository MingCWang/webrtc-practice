# webrtc-practice




## What is WebRTC?
WebRTC is a free, open-source project that provides web browsers and mobile
applications with real-time communication (RTC) via simple application programming
interfaces (APIs). It allows audio and video communication to work inside web pages by allowing
direct peer-to-peer communication, eliminating the need to install plugins or download native apps.

It is not a library or a framework, but a set of protocols and built in JavaScript APIs for the browser that enable real-time communication over the internet. WebRTC is built on three main APIs:
- MediaStream: for handling audio and video streams
- RTCPeerConnection: for handling peer-to-peer communication
- RTCDataChannel: for handling peer-to-peer data exchange



## How WebRTC works

1. **Get user media**: The first step in a WebRTC call is to get access to the user's media devices, such as the camera and microphone. This is done using the `getUserMedia` API, which prompts the user for permission to access their media devices and returns a `MediaStream` object that represents the user's audio and video streams.
2. **Peer to peer connection**: Once the user's media streams are obtained, the next step is to establish a peer-to-peer connection between the two clients. This is done using the `RTCPeerConnection` API, which handles the negotiation of the connection and the exchange of media streams between the clients.


### Signaling
In order for a WebRTC app to set up a call, its clients need to exchange the following information:
- Session-control messages used to open or close communication
- Error messages
- Media metadata, such as codecs, codec settings, bandwidth, and media types
- Key data used to establish secure connections
- Network data, such as a host's IP address and port as seen by the outside world

<details>
<summary>Signaling portocols</summary>
<br>


### UDP vs TCP
WebRTC uses UDP for media transport and TCP for signaling. UDP is preferred for media transport because it is faster and more efficient than TCP. However, UDP is not always available, especially in enterprise networks, so WebRTC needs to be able to fall back to TCP when necessary.

### NAT (Network Address Translation)
NAT is a method used by routers and firewalls to map multiple devices within a private network (like those in a home or business) to share a single public IP address for accessing the internet. While NAT helps alleviate the shortage of IPv4 addresses and provides an additional layer of security by hiding internal IP addresses, it complicates peer-to-peer (P2P) communication because endpoints on the internet cannot directly address devices behind a NAT.

### STUN (Session Traversal Utilities for NAT)
STUN is a protocol that allows clients to discover their public IP addresses and the type of NAT they are behind. It is used to find the public IP address of a peer and to determine the type of NAT that the peer is behind. STUN servers are used to obtain IP addresses and ports for the purpose of establishing peer-to-peer connections.

### TURN (Traversal Using Relays around NAT)
TURN extends STUN by setting up a relay on the public internet for devices that are unable to establish direct connections due to restrictive NAT types or firewall rules. Instead of direct P2P communication, TURN routes the traffic through the relay server, ensuring that the session can be established even in challenging NAT scenarios. TURN is used as a fallback mechanism when STUN fails to establish a direct connection.

### ICE (Interactive Connectivity Establishment)
ICE is a protocol used for NAT traversal in IP networks. It enables devices behind NATs to discover and communicate their public-facing IP addresses and ports to establish a direct connection. ICE works by gathering all possible candidates (local IP addresses, reflexive addresses discovered via STUN, and relayed addresses obtained through TURN) and then testing connectivity through these candidates in order of priority until a successful path for the media traffic is found.

### SIP (Session Initiation Protocol)
SIP is a signaling protocol used for initiating, managing, and terminating real-time sessions that involve video, voice, messaging, and other communications applications and services between two or more endpoints on IP networks. SIP is widely used in VoIP (Voice over IP) services, video conferencing, and other multimedia sessions. It utilizes the offer/answer model to exchange session descriptions, which makes it compatible with ICE for NAT traversal purposes.

Example of a SIP INVITE message of A sending an INVITE to B:
```
INVITE sip:B@example.com SIP/2.0
Via: SIP/2.0/UDP APC.example.com;branch=z9hG4bKnashds8
From: "A" <sip:A@example.com>;tag=1928301774
To: <sip:B@example.com>
Call-ID: a84b4c76e66710@APC.example.com
CSeq: 314159 INVITE
Contact: <sip:A@APC.example.com>
Content-Type: application/sdp
Content-Length: ...

(Session Description Protocol content here)
```

### How these protocols work together
![Screen Shot 2024-02-24 at 2.15.12 AM.png](..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2Fdn%2F1gqdxbz133l8yjgxnh1_mwcc0000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_0Wdif7%2FScreen%20Shot%202024-02-24%20at%202.15.12%20AM.png)




### JSEP (JavaScript Session Establishment Protocol)

JSEP avoids saving state by design, leveraging the WebRTC API and the application layer to manage the complexities of session establishment, modification, and termination.
![jsep-architecture-diagram_1920.png](..%2F..%2Fjsep-architecture-diagram_1920.png)

</details>

### The work flow of WebRTC
- Where you are
	- Getting the public IP address of your device using the STUN server to tell the other peer where you are. The STUN server will send back an ICE candidate that contains the public IP address and port of your device.
- What you are sending
	- Add tracks to the RTCPeerConnection object to tell the other peer what you are sending. The tracks can be audio, video, or data.

## Resources on WebRTC
1. [WebRTC vs WebSockets](https://stackoverflow.com/questions/18799364webrtc-vs-websocket-if-webrtc-can-do-video-audio-and-data-why-do-i-need-webs)
3. [Doc on JSEP (JavaScript Session Establishment Protocol)](https://datatracker.ietf.org/doc/html/draft-ietf-rtcweb-jsep-03#section-1.1)
4. [Official WebRTC documentation](https://webrtc.org/getting-started/media-devices#using-promises)
5. [Tutorial on WebRTC](https://www.youtube.com/watch?v=g42yNO_dxWQ&ab_channel=GoodMorningDevelopers)
