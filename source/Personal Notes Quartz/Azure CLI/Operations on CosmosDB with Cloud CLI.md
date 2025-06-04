---
tags:
  - azure
  - cloud
  - az-900
  - azure-cli
  - cosmosdb
---

This page lists some scripts useful for operating on [[Azure Cosmos DB]].

## Create a CosmosDB account

The name must be:

- lowercase
- with only numbers, letters, hyphens
- between 3 and 31 char long

```bash
az cosmosdb create
    --name <myCosmosDBacct>
    --resource-group <resource-group-name>
```

This command returns several info, such as the `documentEndpoint`.

## Get the primary key

```bash
az cosmosdb keys list
    --name <myCosmosDBacct>
    --resource-group <resource-group-name>
```
