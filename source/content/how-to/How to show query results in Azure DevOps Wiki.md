---
tags:
  - azure-devops
  - documentation
---

On Azure DevOps it is possible to create queries on the work items. You can even show the query result directly in the Wiki.

First of all, you have to create a Shared (so, public) wiki:



![[Pasted image 20250625093926.png]]

Take the ID from the URL, and use it like this in a Wiki page

```plaintext
::: query-table 88d84a5a-4242-4c6a-b823-7dcbceddb8c7
:::
```

Now you'll be able to see the result of the query directly in the Wiki, like this:

![[Pasted image 20250625094227.png]]