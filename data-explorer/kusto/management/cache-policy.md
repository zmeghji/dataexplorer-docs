---
title: Cache policy - Azure Data Explorer | Microsoft Docs
description: This article describes Cache policy in Azure Data Explorer.
services: data-explorer
author: orspod
ms.author: orspodek
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
ms.date: 02/19/2020
---
# cache policy command

This article describes commands used for creation and altering [cache policy](cachepolicy.md) 

## Displaying the cache policy

The policy can be set on a database, a table or a [materialized view](materialized-views/materialized-view-overview.md), and is displayed by using one of the following
commands:

* `.show` `database` *DatabaseName* `policy` `caching`
* `.show` `table` *TableName* `policy` `caching`
* `.show` `materialized-view` *MaterializedViewName* `policy` `caching`

## Altering the cache policy

```kusto
.alter <entity_type> <database_or_table_or_materialized-view_name> policy caching hot = <timespan>
```

Altering cache policy for multiple tables (in the same database context):

```kusto
.alter tables (table_name [, ...]) policy caching hot = <timespan>
```

Cache policy:

```kusto
{
  "DataHotSpan": {
    "Value": "3.00:00:00"
  },
  "IndexHotSpan": {
    "Value": "3.00:00:00"
  }
}
```

* `entity_type` : table, materialized view, database, or cluster
* `database_or_table_or_materialized-view`: if entity is table or database, its name should be specified in the command as follows - 
  - `database_name` or 
  - `database_name.table_name` or 
  - `table_name` (when running in the specific database's context)

## Deleting the cache policy

```kusto
.delete <entity_type> <database_or_table_name> policy caching
```

**Examples**

Show cache policy for table `MyTable` in database `MyDatabase`:

```kusto
.show table MyDatabase.MyTable policy caching 
```

Setting cache policy of table `MyTable` (in database context) to 3 days:

```kusto
.alter table MyTable policy caching hot = 3d
.alter materialized-view MyMaterializedView policy caching hot = 3d
```

Setting policy for multiple tables (in database context), to 3 days:

```kusto
.alter tables (MyTable1, MyTable2, MyTable3) policy caching hot = 3d
```

Deleting a policy set on a table:

```kusto
.delete table MyTable policy caching
```

Deleting a policy set on a materialized view:

```kusto
.delete materialized-view MyMaterializedView policy caching
```

Deleting a policy set on a database:

```kusto
.delete database MyDatabase policy caching
```
