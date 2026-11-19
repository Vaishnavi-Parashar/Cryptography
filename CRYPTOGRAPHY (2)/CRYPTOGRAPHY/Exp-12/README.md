# Experiment 12: Identification and Analysis of Secure and Insecure Network Protocols Using Wireshark

## 1. Aim

To capture and examine network packets using Wireshark, identify secure and insecure communication protocols, and understand the security differences between them.

## 2. Introduction

Wireshark is an open-source network analysis tool that allows users to capture and inspect network packets in real time.

Different network protocols are responsible for exchanging information between devices. HTTP transfers data without encryption, whereas HTTPS uses TLS to encrypt communication and protect information from unauthorized access.

In this experiment, HTTP and HTTPS traffic are captured and examined using Wireshark to understand how encryption affects network communication and security.

## 3. Software Requirements

- Wireshark
- Windows or Linux operating system
- Active internet connection
- Web browser
- Command Prompt (CMD)

## 4. Theory

### A. HTTP (Hypertext Transfer Protocol)

HTTP is an application-layer protocol that enables communication between web browsers and web servers.

**Characteristics:**
- Default Port: 80
- Data Transmission: Unencrypted
- Security: Insecure
- Vulnerabilities: Data interception and modification

### B. HTTPS (Hypertext Transfer Protocol Secure)

HTTPS is an enhanced version of HTTP that uses TLS encryption to secure the exchange of information between a client and a server.

**Characteristics:**
- Default Port: 443
- Data Transmission: Encrypted
- Security: Secure when properly configured
- Protection: Confidentiality, integrity, and server authentication

### C. TLS (Transport Layer Security)

TLS is a security protocol designed to establish protected communication between devices over a network.

It uses a handshake mechanism to negotiate the cryptographic settings and establish keys before encrypted application data is exchanged.

Important TLS handshake messages include:

1. **Client Hello:** The client starts the handshake by sending its supported TLS versions and cipher suites.
2. **Server Hello:** The server responds by selecting the TLS parameters that will be used for communication.
3. **Application Data:** After the handshake establishes the necessary keys, application information is transmitted in encrypted form.

## 5. Procedure

### Step 1: Launch Wireshark

1. Open Wireshark on your system.
2. Choose the currently active Wi-Fi or Ethernet interface.
3. Click Start Capture to begin recording network packets.

### Step 2: Generate and Capture HTTP Traffic

Open Command Prompt and execute the following command:

```cmd
curl.exe -v http://neverssl.com/
```

After executing the command, return to Wireshark and apply this display filter:

```text
http
```

Examine the captured HTTP request and response packets.

### Step 3: Inspect HTTP Packets

1. Select an HTTP GET request from the captured packets.
2. Expand the Hypertext Transfer Protocol section.
3. Examine the request method, host name, and request URI.
4. Right-click the selected packet and choose **Follow → HTTP Stream**.
5. Observe the readable request and response information.

**Observation:** HTTP sends application data without encryption. Therefore, the transmitted request and response information can generally be viewed directly in the packet capture.

### Step 4: Capture HTTPS Traffic

Stop the existing capture and begin a new capture using the active network interface.

Open Command Prompt and run:

```cmd
curl.exe -v --http1.1 https://example.com/
```

Return to Wireshark and enter the following filter:

```text
tls
```

Examine the TLS packets generated during the HTTPS connection.

### Step 5: Examine the TLS Client Hello Message

Apply the following display filter:

```text
tls.handshake.type == 1
```

Select a Client Hello packet and expand these sections:

- Transport Layer Security
- TLS Record Layer
- Handshake Protocol: Client Hello

Observe the supported TLS versions and the cipher suites offered by the client.

Examples of modern cipher suites include:

```text
TLS_AES_128_GCM_SHA256
TLS_AES_256_GCM_SHA384
TLS_CHACHA20_POLY1305_SHA256
```

### Step 6: Examine the TLS Server Hello Message

Apply the following display filter:

```text
tls.handshake.type == 2
```

Select a Server Hello packet and inspect the following details:

- Negotiated TLS version
- Selected cipher suite
- Server handshake parameters

These details indicate the cryptographic settings selected for securing the connection.

### Step 7: Inspect Encrypted Application Data

Enter the following display filter:

```text
tls.record.content_type == 23
```

Examine the TLS Application Data records.

Unlike HTTP, HTTPS protects application content through encryption. Therefore, the original application data cannot normally be read directly from captured TLS packets without the appropriate decryption keys.

### Step 8: Save the Packet Captures

1. Stop the packet capture.
2. Open the **File → Save As** option.
3. Save the captured files using the following names:

```text
HTTP_Capture.pcapng
HTTPS_Capture.pcapng
```

## 6. Comparison of Secure and Insecure Protocols

| Feature | HTTP | HTTPS |
|---|---|---|
| Full Form | Hypertext Transfer Protocol | Hypertext Transfer Protocol Secure |
| Default Port | 80 | 443 |
| Encryption | Not Used | Uses TLS |
| Data Visibility | Readable plaintext | Encrypted application content |
| Data Confidentiality | Not Provided | Provided |
| Data Integrity | No cryptographic protection | Protected by TLS |
| Authentication | No built-in server authentication | Certificate-based server authentication |
| Security | Insecure | Secure when properly configured |

## 7. Wireshark Display Filters

| Filter | Purpose |
|---|---|
| `http` | Displays HTTP packets |
| `tls` | Displays TLS packets |
| `tcp.port == 80` | Shows TCP traffic using port 80 |
| `tcp.port == 443` | Shows TCP traffic using port 443 |
| `tls.handshake.type == 1` | Identifies TLS Client Hello messages |
| `tls.handshake.type == 2` | Identifies TLS Server Hello messages |
| `tls.record.content_type == 23` | Displays TLS Application Data records |
| `dns` | Displays DNS packets |

## 8. Security Implications

### A. Risks of Insecure Communication

- HTTP transfers application data without encryption.
- Network attackers may intercept and read transmitted information.
- Sensitive data can be exposed during transmission.
- Unencrypted communication can be modified by attackers.

### B. Advantages of Secure Communication

- HTTPS uses TLS encryption to protect application data.
- TLS provides confidentiality and cryptographic integrity.
- Digital certificates help verify the identity of servers.
- Secure cipher suites protect communication against passive eavesdropping.
- Proper TLS configuration helps reduce the risk of man-in-the-middle attacks.

## 9. Observations

During the experiment, HTTP packets were successfully captured using Wireshark.

The captured HTTP communication contained readable information such as:

```text
GET / HTTP/1.1
HTTP/1.1 200 OK
```

The HTTP request was transmitted using TCP destination port 80, and its contents could be inspected through the packet details.

For HTTPS communication, TLS packets were examined to identify the Client Hello, Server Hello, and encrypted Application Data records. These observations demonstrated how TLS establishes secure communication and protects application information.

## 10. Result

HTTP and HTTPS network traffic were captured and examined using Wireshark. The HTTP packet analysis demonstrated that application data is transmitted in readable form without encryption.

The HTTPS analysis demonstrated how TLS negotiates cryptographic parameters and protects application data through encryption.

The experiment successfully highlighted the security benefits of HTTPS compared with HTTP.

## 11. Conclusion

This experiment demonstrated the use of Wireshark for capturing and analyzing network traffic to distinguish between secure and insecure communication protocols.

The analysis showed that HTTP transmits application data without encryption, making it vulnerable to interception and modification. In contrast, HTTPS uses TLS to establish an encrypted connection through handshake messages and cryptographic parameter negotiation.

Thus, the experiment helped develop an understanding of the importance of secure protocols in maintaining data confidentiality, integrity, and server authentication during network communication.