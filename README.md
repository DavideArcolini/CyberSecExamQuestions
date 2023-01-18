# Cybersecurity - a collection of questions for the exam

1. [TLS](#tls)
2. [SSH](#ssh)
3. [X.509 Certificates](#x509-certificates)
4. [XML Digital Signatures](#xml-digital-signatures)
5. [Wi-Fi Security](#wi-fi-security)
6. [Electronic identity (eIDAS and SPID)](#electronic-identity-eidas-and-spid)
7. [Forensic Analysis](#forensic-analysis)
8. [Trusted Computing](#trusted-computing)
9. [Privacy (GDPR)](#privacy-gdpr)

## TLS
1. **What is perfect forward secrecy? What is the problem if the protocol does not have it? Show an example of implementation.** [2022/01/27 - 2022/04/07 - 2021/01/xx - 2021/09/xx] \
Perfect Forward Secrecy (PFS) is a feature of a Key Agreement Protocol that assures that the compromise of long-term secrets does not compromise past exchanged session-keys. For instance, in TLS, the compromise of the server private key (i.e., the long-term secret) does not allow an attacker to decrypt any recorded past sessions. In TLS, this is typically performed through Ephemeral Diffie-Hellman (EDH) exchange: whereas the key-pairs of the two peers are uniquely used for authentication, a new ephemeral key is generated for each connection. 

2. **TLS client authentication? How it works? Advantages and disadvantages?** [2021/02/xx] \
Eventually, in a TLS handshake, the server may require the client to provide a certificate for authentication, by sending a `Client Certificate Request`. This message, sent by the server after the `Server Hello` and the Server certificates, depending on the implementations, may contain a list of allowed certificate types and a list of trusted CAs. The client will the provide its certification chain, an explicit signature over all the handshake will be verified and then the communication continues as normal. Client authentication provides strong security and a reduced attack surface, moreover, it can be used to restrict access to a particular service. On the other hand, it adds complexity to the TLS Handshake process, increasing latency. It is typically not that feasible for the client, which is required to have a Certificate.

## SSH
1. **What are available types of peer authentication in SSH and which techniques do they use?** [2022/01/27 - 2021/02/xx - 2021/09/xx] \
In SSH, server authentication and client authentication are performed through two different protocols:
    - *Server authentication* is performed by the Transport Layer Protocol which runs directly on top of TCP. In this protocol, Diffie-Hellman (DH) is used to exchange keys. The Diffie-Hellman (DH) key exchange provides a shared secret that cannot be determined by either party alone. The key exchange is combined with a *signature* with the host key to provide *server authentication*. There is no PKI so the client locally stores the public keys of the servers; typically each user stores them in its home directory `~/.ssh/known_host` where there are couples server name and public key. 
    - *Client authentication* is performed by the User Authentication Protocol, which runs on top of the Transport Layer Protocol. The two main methods of client authentications are:
        - *Password Authentication Method*: compulsory at minimum with username and password (unlike TLS). Note that even though the cleartext password is transmitted in the packet, the entire packet is encrypted by the transport layer.
        - *Public Key Authentication Method*: optionally it is possible to use asymmetric challenge-response; the problem again is that there are no certificates, so the public key of the authorized client is stored by the server in a file `~/local_user/.ssh/authorized_keys`.

## X.509 Certificates
1. **When I receive a document digitally signed with a certificate and its certificate chain, what are all the steps to check if it is a valid document? How can I assess information about certificate status without any external knowledge?** [2022/01/27 - 2022/04/07 - 2021/01/xx]

2. **What is secure *time-stamping*? What is possible to say about when a document was created, signed, timestamped?** [2022/01/27 - 2022/04/07 - 2021/02/xx - 2021/09/xx]

3. **SubjectAltName: what is? Purpose? Make an example.** [2021/01/xx]

4. **What are possible attacks on OCSP protocol?** [2021/02/xx - 2021/09/xx]

5. **What is PEP and PDP? Make an example of real implementation** [2022/01/27 - 2021/01/xx]

## XML and JSON Digital Signatures and Encryption
1. **Three possible types of XML Digital Signatures.** [2022/04/07] \
XML Signature Syntax and Processing defines an XML syntax for digital signatures. There are three possible type of signatures:
    - *Detached signature*: it is used to sign a resource outside its containing XML document. In this case, the `signedInfo` fields of the XML document presents an external URI (e.g. `reference=http://domain.com/external_resource.data`) in the `reference` field.
    - *Enveloping signature*: it contains the signed data within itself. In this case, the `signedInfo` fields of the XML document presents a self referenced URI (`reference=#id`) in the `reference` field.
    - *Enveloped signature*: it is used to sign some part of its containing document. In this case, the `signedInfo` fields of the XML document presents a null URI (`reference=''`) in the `reference` field.

## Wi-Fi Security
1. **Define EAP-TLS, EAP-TTLS and PEAP.** [2022/04/07] \
In 802.11i, the initial authentication is performed either using a Pre-Shared Key (PSK) or by following a EAP exchange through 802.1X (known as EAPOL, which requires the presence of an authentication server). Extensible Authentication Protocol (EAP) is an authentication framework (not an authentication mechanism) widely adopted in Wireless LAN. Three of a long list of possible methods are:
    - *EAP-TLS*: it is the original, standard wireless LAN EAP authentication protocol. It uses TLS to perform mutual authentication between the Authentication Server (AS) and the station (STA), which means that the device trying to connect to the Access Point (AP) must have a X.509 Certificate (i.e. a key-pair). For this reasons, although it is one of the strongest method, it is not so common.
    - *EAP-TTLS*: in EAP-Tunneled TLS, the client can (but does not have to) be authenticated via a CA-signed PKI certificate to the server. This greatly simplifies the setup procedure since a certificate is not needed on every client. The AP acts as a pass-through device and a TLS channel is created between the STA and the AS. After the server is securely authenticated to the client via its CA certificate and optionally the client to the server, the server can then use the established secure connection ("tunnel") to authenticate the client with various type of STA authentication (EAP or others).
    - *PEAP*: exactly like EAP-TTLS, but in this case, once the tunnel has been crated, only EAP methods of client authentication are valid.


## Electronic identity (eIDAS and SPID)
1. **Delegated authentication model? Describe 2 possible scenarios. Describe the problems.** [2021/02/xx - 2021/09/xx]

## Forensic Analysis
1. **What is slack space? Why is relevant in forensic analysis?** [2021/01/xx - 2021/09/xx] \
Slack space is a term used to describe the unused or available space within a computer's file system. It occurs when a file is smaller than the smallest allocation unit (such as a cluster or block) used by the file system, which means that the file does not fill the entire allocation unit. The remaining space in the allocation unit is considered slack space. Slack space is important for a Forensic Analyst since it can be analyzed to recover deleted files (e.g., by using tools like `foremost`).

## Trusted Computing
1. **What is remote attestation in trusted computing environment?** [2022/01/27 - 2022/04/07 - 2021/01/xx] \
In Trusted Computing, *Remote Attestation* is a key feature that allows a remote verifier to evaluate the trustworthiness of a specific computer. In that computer, a TPM is storing the measured hash value (1st stage boot loader, BIOS/UEFI, OS, apps, etc...) in the PCRs. Eventually, the remote verifier will sent a challenge (i.e. a nonce) to the targeted computer, which will responds with the list of PCRs value, digitally signed with *TPM DevID* (*device identifier*). The verifier will performs two operations:
    - it will check that the signature is valid, so that the values have not been tampered with;
    - it will check that the measured PCRs values are valid, compared with the so-called *Golden Values* (pre-computed values which are known to be valid).

2. **What is the sealing operation in trusted computing environment?** [2021/01/xx - 2021/09/xx] \
In Trusted Computing, one of the features of a *Trusted Platform Module* (*TPM*) is the capability *to seal* specific data to the hardware and software environment. *Sealing* is an operation that encrypts data based not only on the data itself, but also on the configuration of the hardware modules and the active softwares in that specific time (named *state*). In this way, the *unsealing* reverse operation (decryption) can be performed if and only if the *state* of the computer at decryption time is the same at encryption time. Therefore, a malicious software running will prevent the unsealing operation due to the fact that the state is different than the one at encryption time.

## Privacy (GDPR)
1. **GDPR: Data minimization, data accuracy, storage limitation.** [2021/02/xx] \
General Data Protection Regulations (GDPR, a 2018 personal data regulation in the European Union (EU)) specifies that:
    - *data minimization*: data shall be adequate, relevant and limited to what is necessary to the purposes for which they are processed. Moreover, if specific data are collected, it should be able to demonstrate that those data are necessary and fundamental for the offered service. As a guideline: do not exceed in data collection.
    - *data accuracy*: data shall be accurate and, if necessary, kept up to date. This is definitely not easy. As an example, if the home address of a user changes, do we have the right to keep stored the old address? There should be a way to keep data up to date once collected.
    - *storage limitation*: here limitation refers to limitation in time. Data should be kept in a form which permits identification of subjects for no longer than it is necessary. As an example, if data are collected after buying a flight ticket, do we have the right to keep stored that personal information after the flight has ended? Data should be labelled with an expiration data and an automatic procedure should be implemented to remove old data. 