---
layout: navpage
sidebar: operations
title: "MinAll"
permalink: /operation/minall
tags: [repodb, tutorial, minall, orm, hybrid-orm, sqlserver, sqlite, mysql, postgresql]
---

# MinAll

This method is used to computes the min value of the target field.

#### Code Snippets

Below is a sample code that returns the minimum value of the column `Value` from a `[dbo].[Sales]` table.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var expenses = connection.MinAll<Sales>(e => e.Value);
}
```

#### Targeting a Table

You can also target a specific table by passing the literal table and field name like below.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var expenses = connection.MinAll("[dbo].[Sales]",
		Field.From("Value"));
}
```

#### Table Hints

To pass a hint, simply write the table-hints and pass it in the `hints` argument.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var expenses = connection.MinAll<Sales>(e => e.Value,
		hints: "WITH (NOLOCK)");
}
```

Or, you can use the [SqlServerTableHints](/class/sqlservertablehints) class.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var expenses = connection.MinAll<Sales>(e => e.Value,
		hints: SqlServerTableHints.NoLock);
}
```
