# Experiment 10: Capturing HTTPS Traffic and Identifying TLS Handshake, Certificates, and Cipher Suites

## Aim
To capture HTTPS network traffic using Wireshark and examine the TLS handshake process, digital certificates, and cipher suites used to establish secure communication.

## Objective
- Capture HTTPS packets using Wireshark.
- Identify the different stages of the TLS handshake.
- Examine the digital certificate presented by the server.
- Identify the cipher suite selected for secure communication.
- Understand how TLS protects data transmitted over HTTPS.

## Tools and Technologies Required
- Wireshark
- Web browser (Google Chrome, Firefox, or Microsoft Edge)
- Internet connection
- Operating System: Windows or Linux

## Introduction
HTTPS (Hypertext Transfer Protocol Secure) is a secure version of HTTP that uses TLS (Transport Layer Security) to protect communication between a web browser and a web server.

TLS provides encryption, authentication, and data integrity. Before exchanging application data, the browser and server perform a TLS handshake to establish the security parameters required for communication.

Wireshark is a network protocol analyzer that captures and displays network packets. It helps examine the TLS handshake messages, server certificates, and cipher suites.

## Procedure

### Step 1: Open Wireshark
1. Launch Wireshark on your computer.
2. Select the active network interface, such as Wi-Fi or Ethernet.
3. Start capturing packets.

### Step 2: Generate HTTPS Traffic
1. Open a web browser.
2. Visit an HTTPS website, such as `https://www.google.com`.
3. Browse the website for a few seconds.
4. Return to Wireshark and stop the packet capture.

### Step 3: Apply the TLS Display Filter
Enter the following filter in Wireshark:

```text
tls
```

This displays packets identified as TLS traffic.

To examine handshake messages specifically, use:

```text
tls.handshake
```

### Step 4: Identify the TLS Handshake
Examine the captured packets and identify the following handshake messages:

- Client Hello: The client sends supported TLS versions, cipher suites, and other parameters.
- Server Hello: The server selects the TLS version and cipher suite for the connection.
- Certificate: The server provides its digital certificate for authentication, when applicable.
- Finished: The communicating parties confirm that the handshake has been completed successfully.

### Step 5: Examine the Server Certificate
1. Select a TLS packet containing a Certificate message, if visible.
2. Expand the TLS section in the packet details.
3. Examine the certificate information, including:
   - Issuer
   - Subject
   - Validity period
   - Public key information

### Step 6: Identify the Cipher Suite
1. Select the Server Hello packet.
2. Expand the TLS handshake details.
3. Locate the selected cipher suite.
4. Note the cipher suite displayed in the packet details.

## Wireshark Filters

| Filter | Purpose |
|---|---|
| `tls` | Displays TLS traffic |
| `tls.handshake` | Displays TLS handshake messages |
| `tls.handshake.type == 1` | Displays Client Hello messages |
| `tls.handshake.type == 2` | Displays Server Hello messages |
| `tls.handshake.type == 11` | Displays Certificate messages, when visible |

## Expected Observations

1. Wireshark captures packets exchanged during HTTPS communication.
2. The Client Hello message contains the client's supported TLS parameters.
3. The Server Hello message identifies the TLS version and selected cipher suite.
4. The server certificate provides information used for authentication.
5. After the handshake, application data is transmitted in encrypted form.

## Result
HTTPS traffic was successfully captured and analyzed using Wireshark. The TLS handshake messages, certificate information, and negotiated cipher suite were examined to understand how TLS establishes secure communication between a client and a server.

## Conclusion
This experiment demonstrated how Wireshark can be used to analyze HTTPS communication and inspect the TLS handshake process. It helped identify the role of digital certificates, cipher suite negotiation, and encryption in securing network communication.