---
title: "Server Message Block"
tags:
  - file-system
  - protocol
  - networking
  - smb
aliases:
  - SMB protocol
---

The **Server Message Block (SMB)** protocol is a **network file sharing** protocol: clients read and write files and request remote services over a LAN or WAN.

The SMB protocol **can be used on top of its TCP/IP** protocol or other network protocols.

Using the SMB protocol, an application (or the user of an application) can access files or other resources at a remote server. This allows applications to read, create, and update files on the remote server. SMB can also communicate with any server program that is set up to receive an SMB client request.

Examples of usage are:

- File storage for virtualization (Hyper-V™ over SMB). Hyper-V can store virtual machine files, such as configuration, Virtual hard disk (VHD) files, and snapshots, in file shares over the SMB 3.0 protocol.
- Microsoft SQL Server over SMB. SQL Server can store user database files on SMB file shares. Currently, this is supported with SQL Server 2008 R2 for stand-alone SQL servers. Upcoming versions of SQL Server will add support for clustered SQL servers and system databases.
- Traditional storage for end-user data.
