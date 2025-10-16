---
date: "2025-10-16T19:44:25+08:00"
draft: false
tags: ["lab", "network", "learning", "SCOR"]
title: "Eveng Network Simulator - GCP setup"
---

When learning networking for any reason, such as for professional certificates like CCNA or for upskilling, we cannot avoid using one of the popular tools, which is EVE-NG.

This is my first post about EVE-NG as I want to pursue the Cisco SCOR certification, and I find it more interesting to learn through labbing rather than just memorizing facts.

## What is EVE-NG?

It is a software used for network simulation with various devices across vendors, as long as we have the image files needed for those devices. EVE-NG can be deployed using VirtualBox (Type 2 hypervisor), ESXi (Type 1 hypervisor), on bare metal servers, or on the cloud using providers that allow nested virtualization, such as GCP.

All installation steps can be referred to through the official community cookbook at the following site:
[EVE-NG Community Cookbook](https://www.eve-ng.net/wp-content/uploads/2025/04/EVE-CE-BOOK-6.3-2024.pdf)
