---
date: '2025-06-01T11:44:53+08:00'
draft: false
tags: ["learning", "foundation", "email"]
title: 'Under the Hood: How Your Emails Get Delivered'
---

## Introduction: The Magic of Instant Communication

Email is a technology we often take for granted. These days, we can easily create an email address using providers like Gmail or ProtonMail, and start sending and receiving messages instantly.

However, behind the scenes, there’s much more going on. The journey of an email involves various servers, protocols, and checks. In fact, email delivery works quite differently from regular web traffic, with each component playing a specific role in making sure your message gets delivered reliably.

---

## Email Key Players

Several components are involved in sending and receiving emails:

- **Email Client (MUA - Mail User Agent)**  
  _Examples: Outlook, Thunderbird_  
  **What it does**: Lets users compose, send, and receive emails. It connects to mail servers for sending (SMTP) and retrieving (IMAP/POP3) messages.

- **Mail Servers (The Post Offices & Mail Carriers)**  
  - **SMTP Server (Simple Mail Transfer Protocol)**  
    **Role**: Sends emails to the recipient's mail server. Think of it as the mail carrier.  
    **Job**: Routes outgoing messages and receives incoming mail from other SMTP servers.
    
  - **POP3/IMAP Server**  
    **Role**: Handles incoming messages for users.  
    **Job**: Stores received mail and allows clients to fetch or sync messages.

- **DNS (Domain Name System – The Address Book)**  
  **Role**: Translates domain names into IP addresses.  
  **Job**: Helps the sending SMTP server find the recipient’s mail server by querying DNS MX (Mail Exchange) records.

---

## The Journey: How an Email Is Sent (Step-by-Step)

1. **You hit "Send" in your email client (MUA)**  
   - Your email client connects to the configured **outgoing SMTP server**.

2. **SMTP server processes the message**  
   - The SMTP server receives the email.  
   - It performs a **DNS lookup** to find the MX record for the recipient's domain.

3. **Server-to-server communication begins (SMTP protocol)**  
   - The sender’s SMTP server connects to the recipient’s SMTP server (usually on port 25).  
   - They communicate using SMTP protocol, negotiating delivery.  
   - The message is transferred to the recipient’s server.

4. **Recipient’s server receives and stores the email**  
   - The email may be checked for spam, malware, or policy violations.  
   - If everything is okay, the email is accepted and stored on the server.

---

## The Journey: How an Email Is Received (Step-by-Step)

1. **Recipient opens their email client**  
   - The client is configured to connect to a **POP3 or IMAP server**.

2. **Email is fetched**  
   - The email client connects and authenticates.  
   - The mail is then downloaded (POP3) or synced (IMAP).  
   - The user can now read the message.

---

## Conclusion: More Than Just Magic

This basic mail flow doesn't even include security appliances like Cisco Secure Email Gateway (SEG), which are critical in real-world scenarios. Standard email protocols are vulnerable to threats such as phishing, spoofing, and malware.

Understanding how email works under the hood helps explain why security tools like Cisco SEG (formerly ESA) are still important today. Despite being a decades-old technology, email continues to evolve—and so must our understanding and protection of it.