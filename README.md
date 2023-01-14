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
1. **What is perfect forward secrecy? What is the problem if the protocol does not have it? Show an example of implementation.** [2022/01/27 - 2022/04/07 - 2021/01/xx - 2021/09/xx]

2. **TLS client authentication? How it works? Advantages and disadvantages?** [2021/02/xx]

## SSH
1. **What are available types of peer authentication in SSH and which techniques do they use?** [2022/01/27 - 2021/02/xx - 2021/09/xx]

## X.509 Certificates
1. **When I receive a document digitally signed with a certificate and its certificate chain, what are all the steps to check if it is a valid document? How can I assess information about certificate status without any external knowledge?** [2022/01/27 - 2022/04/07 - 2021/01/xx]

2. **What is secure *time-stamping*? What is possible to say about when a document was created, signed, timestamped?** [2022/01/27 - 2022/04/07 - 2021/02/xx - 2021/09/xx]

3. **SubjectAltName: what is? Purpose? Make an example.** [2021/01/xx]

4. **What are possible attacks on OCSP protocol?** [2021/02/xx - 2021/09/xx]

## XML Digital Signatures
1. **What is PEP and PDP? Make an example of real implementation** [2022/01/27 - 2021/01/xx]

2. **Three possible types of XML Digital Signatures.** [2022/04/07]

## Wi-Fi Security
1. **Define EAP-TLS, EAP-TTLS and PEAP.** [2022/04/07]

## Electronic identity (eIDAS and SPID)
1. **Delegated authentication model? Describe 2 possible scenarios. Describe the problems.** [2021/02/xx - 2021/09/xx]

## Forensic Analysis
1. **What is slack space? Why is relevant in forensic analysis?** [2021/01/xx - 2021/09/xx]

## Trusted Computing
1. **What is remote attestation in trusted computing environment?** [2022/01/27 - 2022/04/07 - 2021/01/xx]

2. **What is the sealing operation in trusted computing environment?** [2021/01/xx - 2021/09/xx] \
In Trusted Computing, one of the features of a *Trusted Platform Module* (*TPM*) is the capability *to seal* specific data to the hardware and software environment. *Sealing* is an operation that encrypts data based not only on the data itself, but also on the configuration of the hardware modules and the active softwares in that specific time (named *state*). In this way, the *unsealing* reverse operation (decryption) can be performed if and only if the *state* of the computer at decryption time is the same at encryption time. Therefore, a malicious software running will prevent the unsealing operation due to the fact that the state is different than the one at encryption time.

## Privacy (GDPR)
1. **GDPR: Data minimization, data accuracy, storage limitation.** [2021/02/xx] \
General Data Protection Regulations (GDPR, a 2018 personal data regulation in the European Union (EU)) specifies that:
    - *data minimization*: data shall be adequate, relevant and limited to what is necessary to the purposes for which they are processed. Moreover, if specific data are collected, it should be able to demonstrate that those data are necessary and fundamental for the offered service. As a guideline: do not exceed in data collection.
    - *data accuracy*: data shall be accurate and, if necessary, kept up to date. This is definitely not easy. As an example, if the home address of a user changes, do we have the right to keep stored the old address? There should be a way to keep data up to date once collected.
    - *storage limitation*: here limitation refers to limitation in time. Data should be kept in a form which permits identification of subjects for no longer than it is necessary. As an example, if data are collected after buying a flight ticket, do we have the right to keep stored that personal information after the flight has ended? Data should be labelled with an expiration data and an automatic procedure should be implemented to remove old data. 