---
tags:
  - azure
  - cloud
  - az-900
  - azure-cli
  - virtual-machines
---

This page lists some scripts useful for operating on [[Azure Virtual Machines]].

## How to create a VM

```bash
az vm create
  --resource-group ID-RESOURCE-GROUP
  --name VM-NAME
  --public-ip-sku Standard
  --image Ubuntu2204
  --admin-username azureuser
  --generate-ssh-keys
```

The virtual machine is not accessible from the outside.

## How to list all VMs

```bash
az vm list
```

## How to get IP addresses of a specific VM

```bash
az vm list-ip-addresses
  --resource-group ID-RESOURCE-GROUP
  --name VM-NAME
  --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress"
```

returns, for example,

```cli
[
  [
    "104.42.63.128"
  ]
]

```
