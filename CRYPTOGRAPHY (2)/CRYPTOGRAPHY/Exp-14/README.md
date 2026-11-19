# Experiment 14: Generation of SSH/RSA Key Pairs and Configuration of Passwordless Authentication Between Linux Systems

## 1. Aim

To create SSH/RSA public and private key pairs and establish passwordless authentication between two Linux systems using the SSH protocol.

## 2. Introduction

SSH (Secure Shell) is a network protocol that enables secure remote access and communication between computers. It uses encryption to protect information exchanged between a client and a remote server.

One of the important features of SSH is public-key authentication, which allows users to access remote systems without repeatedly entering their account passwords.

In this experiment, an RSA key pair is created on the client machine. The public key is then transferred to the remote Linux system and stored in its authorized keys file. Once configured, the client can establish an SSH connection using key-based authentication.

## 3. Requirements

- Two Linux systems (Kali Linux or Ubuntu)
- SSH client
- OpenSSH server
- Network connectivity between both systems
- Terminal access

## 4. Theory

### A. SSH (Secure Shell)

SSH is a secure communication protocol used to access and control remote computers over a network. It provides encrypted communication and supports remote login, command execution, and file transfers.

### B. RSA Key Pair

RSA is an asymmetric cryptographic algorithm that uses a pair of mathematically related keys for secure authentication and communication.

The key pair consists of:

- **Public Key:** Shared with the remote system and stored for authentication.
- **Private Key:** Stored securely on the client machine and must never be shared.

During SSH authentication, the remote system verifies that the client possesses the private key corresponding to the registered public key.

### C. Passwordless SSH Authentication

Passwordless authentication allows a client to log in to a remote Linux system using SSH keys instead of repeatedly entering the remote account password.

The server checks the client's cryptographic proof against the public key stored in its authorized keys file. If the authentication succeeds, access is granted.

## 5. Procedure

### Step 1: Verify SSH Installation

Check whether the SSH client is available on the Linux system.

```bash
ssh -V
```

This command displays the installed SSH version.

### Step 2: Install OpenSSH Packages

If the required SSH packages are not installed, execute:

```bash
sudo apt update
sudo apt install openssh-client openssh-server -y
```

This installs the SSH client and server components.

### Step 3: Start and Enable the SSH Service

On the remote Linux system, start the SSH service using:

```bash
sudo systemctl start ssh
```

Enable the service to start automatically when the system boots:

```bash
sudo systemctl enable ssh
```

Check whether the service is running:

```bash
sudo systemctl status ssh
```

### Step 4: Generate an RSA Key Pair

On the client Linux machine, execute the following command to generate an RSA key pair:

```bash
ssh-keygen -t rsa -b 4096
```

Press Enter to accept the default location for storing the key files. A passphrase can also be provided to add protection to the private key.

The generated files are:

- `~/.ssh/id_rsa` – Private key
- `~/.ssh/id_rsa.pub` – Public key

The private key remains on the client system, while the public key is shared with the remote system.

### Step 5: Transfer the Public Key to the Remote System

Use the following command to copy the public key to the remote Linux machine:

```bash
ssh-copy-id username@remote_ip
```

Replace `username` with the remote system's account username and `remote_ip` with its IP address.

Enter the remote account password when prompted during the initial key installation.

The public key will be added to the remote user's `authorized_keys` file.

### Step 6: Verify the Generated SSH Keys

List the contents of the SSH directory on the client system:

```bash
ls -l ~/.ssh/
```

Display the public key:

```bash
cat ~/.ssh/id_rsa.pub
```

This confirms that the public key has been generated. The private key should remain confidential.

### Step 7: Test Passwordless SSH Authentication

Execute the following command from the client machine:

```bash
ssh username@remote_ip
```

If the configuration is correct, the client will authenticate using its SSH key without requiring the remote account password.

If a passphrase was configured for the private key, the SSH client may still request that passphrase unless an SSH agent is being used.

### Step 8: Verify the Remote Connection

After successfully logging in, execute:

```bash
hostname
```

This command displays the hostname of the remote Linux machine and confirms that the connection is established.

To terminate the remote session, execute:

```bash
exit
```

## 6. Observations

During the experiment, an RSA public-private key pair was generated on the client Linux system.

The public key was transferred to the remote system and added to its authorized keys file. After configuring the keys, an SSH connection was successfully established using key-based authentication.

The remote system allowed access without requesting the account password, demonstrating the successful implementation of passwordless SSH authentication.

## 7. Advantages of SSH Key-Based Authentication

- Provides secure authentication through public-key cryptography.
- Eliminates the need to repeatedly enter remote account passwords.
- Reduces exposure to password-guessing attacks.
- Supports secure remote system administration.
- Makes automated tasks and server management easier.
- Provides a convenient method for accessing multiple Linux systems.

## 8. Security Precautions

- Never disclose or share the private SSH key.
- Protect private keys using a strong passphrase whenever possible.
- Maintain appropriate permissions for SSH directories and key files.
- Use sufficiently strong cryptographic keys.
- Disable password-based SSH login only after verifying that key-based access works and an alternative recovery method is available.

## 9. Result

An RSA public-private key pair was successfully generated, and SSH key-based authentication was configured between two Linux systems.

The passwordless login mechanism was tested, and a remote connection was established using the corresponding public and private keys.

## 10. Conclusion

This experiment demonstrated the generation of RSA key pairs and the configuration of passwordless SSH authentication between Linux systems.

The implementation showed how public-key cryptography can be used to authenticate remote users securely without repeatedly entering account passwords.

SSH key-based authentication provides a reliable and convenient approach to remote login and is widely used in Linux administration, server management, and automated system operations.