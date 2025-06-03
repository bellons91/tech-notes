---
tags:
  - azure
  - cloud
  - az-900
  - storage
  - AzCopy
  - azure-storage-explorer
---

There are several tools to migrate data.

You can use [[Azure Data Box]] and [[Azure Migrate]].

There are other ways to migrate smaller files.

## AzCopy

AzCopy is a **command-line utility** that you can use to copy blobs or files to or from your storage account.

With AzCopy, you can upload files, download files, copy files between storage accounts, and even synchronize files.

## Azure Storage Explorer

Azure Storage Explorer is a **standalone UI** to manage files and blobs in your Azure Storage Account.

On the backend, it uses AzCopy.

## Azure File Sync

Azure File Sync is a tool that lets you centralize your file shares in Azure Files and keep the flexibility, performance, and compatibility of a Windows file server.

Once you install Azure File Sync on your local Windows server, it will automatically stay **bi-directionally synced** with your files in Azure.
