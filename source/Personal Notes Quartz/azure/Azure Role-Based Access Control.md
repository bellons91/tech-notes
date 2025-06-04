---
tags:
  - azure
  - cloud
  - az-900
  - authentication
  - authorization
  - RBAC
aliases:
  - Azure RBAC
---

It allows the implementation of the [[Principle of Least Privilege]] by defining roles that can be assigned to users.

Each role has a set of access permissions to resources.

Using roles allows you to:

- add (and remove) permissions to users by assigning them a specific role;
- updating permissions to a set of users by updating the role's permissions.

Role-based access control is applied to a **scope**, which is a resource or set of resources that this access applies to.

**Azure RBAC is hierarchical**in that when you grant access at a parent scope, those permissions are inherited by all child scopes.
