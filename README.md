# Design Specifications

## Purpose
---
The core purpose of **Knightstar** is to provide a secure means of communication over the internet. While there are numerous chat applications available, many of them are owned by large corporations like Meta and Google. Unfortunately, the source code for these apps is not publicly available, and they have not been audited by third parties.

One notable exception is **Signal**, an open-source application that has undergone third-party audits. Even WhatsApp uses Signal’s encryption algorithm. However, Signal is backed by a US-based company, which may raise concerns for some users. (This is a personal opinion.)

## Encryption
---
The purpose here is to provide secure end-to-end communication over the internet. We achieve this by using the well-established RSA algorithm for encryption. While some concerns exist regarding quantum computers breaking RSA encryption with smaller key sizes (e.g., 1024-bit keys), larger key sizes (such as 4096 bits) remain highly resistant to attacks.

### Why RSA?
1. **Securing Email Communication (Encrypted Emails):** RSA encryption ensures that email content remains confidential during transmission.

2. **Digital Signature and Document Verification:** RSA signatures verify the authenticity and integrity of digital documents.

3. **Digital Certificates in Websites (SSL/TLS):** RSA certificates secure HTTPS connections, protecting user data.

4. **Secure Remote Access (VPN & SSH):** RSA keys authenticate users and establish secure connections.

5. **Encrypted Messaging Apps:** Many messaging apps rely on RSA for secure communication.

In summary, RSA is battle-tested, widely used, reliable and most importantly **Simple** .

## Technology Stack
---

### Frontend
**Knightstar** is a chat application that needs to be accessible across mobile devices, desktops, and the web. Initially, We considered using **React Native** for its cross-platform capabilities. However, We encountered performance issues with React Native, and managing state became challenging, especially for those unfamiliar with React.

Subsequently, We explored **Flutter**, a cross-platform framework developed by Google. After spending time learning and testing it on both desktop and mobile devices, We concluded that Flutter was the optimal choice. Its speed and cross-platform support make it ideal for the application.

Additionally, we’ve decided to use **Riverpod** for state management.

### Backend

Initially, We opted for **Node.js** as the backend server. While it served its purpose, We encountered some limitations. JavaScript, being an interpreted language, posed challenges. Additionally, when it came to **Web Sockets**, We found that **Go** outperformed Node.js significantly.

Given Go’s reputation and our curiosity, We decided to use it as our backend language.

### Database

We initially selected **MongoDB** as our database. However, after considering long-term requirements, we decided to switch to **Postgres**.

## Authentication
---
We’ve chosen to implement a simple email-based OTP (One-Time Password) system for user authentication. Unlike cellphone-based OTPs, which can be challenging due to fake numbers, email-based OTPs offer several advantages:

1. **Anonymity**: Users can maintain their privacy by using use and throw email addresses.
2. **Unique Identifiers**: Email addresses act as unique identifiers for each user to send and receive messages .
3. **Ease of Use**: Users receive OTPs directly in their email inbox.

## Encryption Key Generation
---
When a user logs into the app, the system will generate encryption and decryption keys. The public key will be stored on the server. It’s important to note that there won’t be a logout feature; users can either delete their account or reset the app.

If the user logs in from another device, a new one-time password (OTP) will be sent. Additionally,  If the account doesn't exist than a new set of key pairs will be generated, and the public key will be updated on the server. If it does exist than there will be secure key transfer happen between devices If the old device is still active and all users will receive notifications that the key for that user has changed.

Furthermore, any users who have communicated with the affected user will update their local databases with the new public key.

## Goal
---
Current Goal is to have a simple working version of the application where use can send each other messages. Encryption and Data persistence will be added in upcoming versions.