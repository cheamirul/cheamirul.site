---
date: '2025-06-01T11:44:53+08:00'
draft: false
tags: ["learning", "foundation", "email"]
title: 'Under the Hood: How Your Emails Get Delivered'
---

## Introduction: The Magic of Instant Communication

These days, sending an email feels almost effortless. We sign up for an account with Gmail, ProtonMail or another provider type out a message, hit "Send" and within seconds it lands in someone else's inbox.

But what actually happens after you click "Send" is much more complex. There’s an entire system working behind the scenes to move your message across servers, networks, and protocols before it reaches its destination. Email doesn’t travel the same way as regular web traffic and understanding how it works can be pretty fascinating.

<p style="text-align: center;">
  <img src="/images/Mailflow.png" alt="Basic mail flow" style="display: block; margin-left: auto; margin-right: auto; max-width: 100%;" />
  <em>Diagram 1: Basic Mail flow</em>
</p>

---

## Email Key Players

Several components are involved in sending and receiving emails:

- **Email Client (MUA - Mail User Agent)**  
  _Examples: Outlook, Thunderbird_  
  **What it does**: It let users compose, send, and receive emails. It connects to mail servers for sending (SMTP) and retrieving (IMAP/POP3) messages.

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

  <p style="text-align: center;">
  <img src="/images/DNS.png" alt="MXquery" style="display: block; margin-left: auto; margin-right: auto; max-width: 100%;" />
  <em>Diagram 2: DNS Query</em>
</p>

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

This basic mail flow doesn't even include security appliances like Cisco Secure Email Gateway (SEG) which are critical in real-world scenarios. Standard email protocols are vulnerable to threats such as phishing, spoofing, and malware.

Understanding how email works under the hood helps explain why security tools like Cisco SEG (formerly ESA) are still important today. Despite being a decades-old technology, email continues to evolve—and so must our understanding and protection of it.