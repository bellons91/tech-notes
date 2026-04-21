---
title: "Stored Access Policies"
tags:
  - az-204
  - authentication
  - shared-access-signature
  - sas
  - microsoft-entra
  - azure-storage
---

# Stored Access Policies

A stored access policy provides an extra level of control over service-level [[Shared Access Signatures]] on the server side.

With a stored access policy, you can group SAS tokens that are bound to the policy and apply stronger or more centralized restrictions on those signatures.

You can use a stored access policy to change the start time, expiry time, or permissions for a signature, or to revoke it after it is issued.

Stored access policies are supported by [[Blob containers]], [[File shares]], [[Queues]], and [[Tables]].

To create or modify a stored access policy, call the Set ACL operation for the resource (see Set Container ACL, Set Queue ACL, Set Table ACL, or Set Share ACL) with a request body that specifies the terms of the access policy. The body of the request includes a unique signed identifier of your choosing, up to 64 characters in length, and the optional parameters of the access policy.

```cs
BlobSignedIdentifier identifier = new BlobSignedIdentifier
{
    Id = "stored access policy identifier",
    AccessPolicy = new BlobAccessPolicy
    {
        ExpiresOn = DateTimeOffset.UtcNow.AddHours(1),
        Permissions = "rw"
    }
};

blobContainer.SetAccessPolicy(permissions: new BlobSignedIdentifier[] { identifier });
```
