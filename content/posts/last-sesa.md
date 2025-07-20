---
date: '2025-07-20T11:51:36+08:00'
draft: false
title: 'Final Reflections on Email Security Before Taking Cisco SESA'
---

In my previous post, I shared how the basic flow of an email works before it reaches our inbox. Then, I introduced Cisco’s solution for email security, which is Cisco SEG, previously known as Cisco Secure Email Appliance (ESA). This post will also wrap up my current learning about Cisco ESA before I attempt the concentration exam in the CCNP Security track related to email security — the Cisco SESA exam.

📄 [Under the Hood: How Your Emails Get Delivered](https://cheamirul.site/posts/emailbegin/)  
🔐 [Introducing the Cisco Secure Email Gateway (SEG/ESA): The Digital Gatekeeper](https://cheamirul.site/posts/sesa-intro/)

---

## What I’ve Learned Since Then

As I went deeper into learning about Cisco ESA and email security in general, a few things became clearer:

- **Understanding Mail Flow**: It’s not just about blocking spam emails. It involves a combination of several policies such as incoming, outgoing, anti-spam, antivirus, filters, and more. When configuring these, we need to be careful so that no misconfiguration occurs, otherwise, malicious emails might slip through, or legitimate emails could get stuck or dropped.

- **Message Tracking**: Before learning about Cisco ESA, I worked with several other devices that mostly focus on device logs. However, message tracking in ESA provides more features when troubleshooting email delivery.

- **Talos Integration**: The true power of Cisco ESA comes from its integration with Talos. Talos provides real-time updates on what to filter, which enhances the ESA’s various filters significantly.

- **Spam Is Evolving**: Even though Talos filters are updated daily, spam emails are still increasing and evolving. This highlights how cybersecurity is not a "set and forget" field, it requires continuous adaptation and improvement.

---

## Hands-on Practice

Almost every time I learn something about Cisco ESA, I try to get hands-on with the device to familiarize myself with all its features. That includes:

- Reviewing AsyncOS CLI and GUI features  
- Reading Cisco’s official documentation on configuration  
- Understanding how companies apply content filters in the real world

Some scenarios are tough to simulate, like email bouncing due to sending to over 100 recipients, but even just analyzing logs has taught me a lot.

---

## Challenges Along the Way

One thing I didn’t expect was how certain features behave in lab environments. For example, when I tried simulating email bounces by sending emails to 100+ recipients repeatedly, Cisco ESA flagged the sender as spam, even in a test environment. This shows that Cisco ESA treats such patterns seriously, just like it would in production.

---

## What’s Next?

I’m planning to take the SESA exam soon, not because it’s required for my current job, but as part of my personal learning roadmap. It aligns with my goal in cybersecurity. After that, I may pursue the Cisco SCOR exam, and if possible, I’d like to challenge myself with the CCIE Security exam. Hopefully, I can continue to grow in this fast-changing cybersecurity field.

---

## Final Note

Thanks to everyone who read my earlier posts and this one until the end. I write mainly to document my journey in the cybersecurity field. This email security series has been a small but important step for me in understanding how security works in real environments, not just theory. If you’re also learning about this topic, feel free to reach out or share your experience.