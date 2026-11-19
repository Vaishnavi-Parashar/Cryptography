# Experiment 11: Capturing and Analyzing Encrypted VPN Traffic and Comparing It with Unencrypted Network Communication

## 1. Aim

To capture and analyze encrypted VPN traffic using Wireshark and compare it with unencrypted network communication to understand how VPN encryption protects data during transmission.

## 2. Objectives

- Capture network packets before and after establishing a VPN connection.
- Analyze encrypted VPN traffic using Wireshark.
- Observe the differences between encrypted and unencrypted communication.
- Understand how VPN technology protects transmitted data.
- Identify the visibility of packet information in both communication methods.

## 3. Technologies Used

- Network Analyzer: Wireshark
- VPN Software: OpenVPN or WireGuard
- Operating System: Windows or Linux
- Network Connection: Internet or local network

## 4. Software Requirements

- Wireshark installed on the system.
- A configured VPN client.
- Active network connection.
- Permission to capture traffic on the selected network interface.

## 5. Concepts Used

### A. VPN (Virtual Private Network)

A VPN creates an encrypted connection, commonly called a tunnel, between a device and a VPN server. It protects network traffic from being easily read by other parties while it travels through the network.

**Key Features:**
- Encrypts network communication.
- Protects transmitted information.
- Helps maintain data confidentiality.
- Creates a secure tunnel between connected endpoints.

### B. Unencrypted Network Communication

In unencrypted communication, information is transmitted without encryption at the application or protocol level. Depending on the protocol, captured packets may expose readable data.

**Key Features:**
- Data may be visible in packet captures.
- Does not provide encryption by itself.
- Sensitive information may be exposed.
- Easier to inspect using network analysis tools.

## 6. Implementation

### Step 1: Open Wireshark

1. Launch Wireshark.
2. Select the active network interface, such as Wi-Fi or Ethernet.
3. Start capturing network packets.

### Step 2: Capture Unencrypted Network Traffic

1. Keep the VPN disconnected.
2. Generate network traffic by visiting an HTTP test website or communicating with a permitted test server.
3. Allow Wireshark to capture the packets.
4. Stop the capture and save it for comparison.

### Step 3: Connect to the VPN

1. Open the configured VPN client.
2. Connect to the VPN server.
3. Confirm that the VPN connection is active.
4. Identify the network interface carrying the VPN tunnel traffic.

### Step 4: Capture Encrypted VPN Traffic

1. Open Wireshark again.
2. Select the physical network interface used by the VPN connection.
3. Start capturing packets.
4. Generate network traffic by browsing websites or accessing a test server.
5. Stop the capture after a few seconds.

### Step 5: Analyze VPN Traffic

Apply the following filters to examine the captured packets:

```text
udp
```

For OpenVPN, if it is configured to use UDP, use:

```text
udp.port == 1194
```

For WireGuard, use:

```text
udp.port == 51820
```

These are common default ports; the actual port may differ depending on the VPN configuration.

### Step 6: Compare Both Captures

Examine the two packet captures and compare:

- Visibility of transmitted data.
- Protocol information.
- Source and destination addresses.
- Packet structure.
- Whether application data can be read directly.

## 7. Wireshark Filters

| Filter | Purpose |
|---|---|
| `ip` | Displays IPv4 packets |
| `tcp` | Displays TCP traffic |
| `udp` | Displays UDP traffic |
| `http` | Displays HTTP traffic |
| `tls` | Displays TLS traffic |
| `udp.port == 1194` | Filters common OpenVPN UDP traffic |
| `udp.port == 51820` | Filters common WireGuard traffic |

## 8. Expected Observations

### A. Unencrypted Communication

- Some application-level information may appear in readable form.
- Packet details can reveal protocol information.
- Data sent through unencrypted protocols may be exposed.

### B. Encrypted VPN Communication

- Traffic between the device and VPN server appears as encrypted tunnel traffic on the physical network interface.
- The original application data is generally not readable directly from the encrypted tunnel packets.
- Source and destination network information and packet sizes may still be visible.
- The VPN protects the contents of the transmitted data through encryption.

## 9. Comparison Between Encrypted and Unencrypted Communication

| Feature | Unencrypted Communication | Encrypted VPN Communication |
|---|---|---|
| Data Protection | No VPN encryption | Encrypted tunnel |
| Data Visibility | May be readable | Tunnel contents are encrypted |
| Confidentiality | Low | Improved |
| Packet Analysis | Application data may be visible | Outer tunnel packets are visible |
| Security | Less protected | Better protected by encryption |

## 10. Results and Observations

1. Network traffic was captured successfully using Wireshark.
2. Unencrypted communication showed that some transmitted information could be inspected directly.
3. VPN traffic appeared as encrypted tunnel communication on the physical network interface.
4. The contents of the VPN tunnel were not directly readable in the ordinary packet capture.
5. The comparison demonstrated how VPN encryption improves the confidentiality of network communication.

## 11. Conclusion

In this experiment, encrypted VPN traffic and unencrypted network communication were captured and analyzed using Wireshark. The packet captures demonstrated the differences in data visibility between the two communication methods.

The experiment showed that VPN technology uses encryption to protect transmitted information and provides a more secure method of communicating over networks.