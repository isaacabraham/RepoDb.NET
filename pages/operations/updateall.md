---
layout: navpage
sidebar: operations
title: "UpdateAll"
permalink: /operation/updateall
tags: [repodb, tutorial, updateall, orm, hybrid-orm, sqlserver, sqlite, mysql, postgresql]
---

# UpdateAll

This method is used to update the existing multiple rows in the table.

#### Use Case

If you are updating multiple rows in the database, do not ever "iterate and merge it in atomic way". This method solves that problem by creating a multi-packed SQL statements and pass it all in one-go.

The performance of this not comparable to the atomic way of updating. It is more performant and efficient.

You can adjust the size of the batch on how much rows you want to process per batch. This scenario applies depends on your situation (i.e.: *No of Columns*, *Network Latency*, etc).

The execution is ACID as the transaction object will be created if not given.

> Be aware that if you are managing the size of your batch, it may collide on the number of maximum allowable parameters of ADO.NET. The max parameters are `2100`.

#### Code Snippets

Let us you have a method that returns a list of `Person` models.

```csharp
private IEnumerable<Person> GetPeople()
{
	var people = new List<Person>();
	people.Add(new Person
	{
		Id = 10045,
		Name = "John Doe",
		Address = "New York",
		DateOfBirth = DateTime.Parse("2020-01-01"),
		IsActive = true,
		DateInsertedUtc = DateTime.UtcNow
	});
	people.Add(new Person
	{
		...
	});
	people.Add(new Person
	{
		...
	});
	return people;
}
```

Below is a sample code to update a list of `Person` into the `[dbo].[Person]` table.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var people = GetPeople();
	var updatedRows = connection.UpdateAll(people);
}
```

By default, it uses the primary (or identity) field as the qualifier. You can override by simply passing the list of fields in the `qualifiers` argument.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var people = GetPeople();
	var updatedRows = connection.UpdateAll(people,
        qualifiers: (p => new { p.Name, p.DateOfBirth }));
}
```

#### Targeting a Table

You can also target a specific table by passing the literal table like below.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var people = GetPeople();
	var updatedRows = connection.UpdateAll<Person>("[dbo].[Person]",
		entities: people);
}
```

Or via dynamics.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var people = GetPeople();
	var updatedRows = connection.UpdateAll("[dbo].[Person]",
		entities: people);
}
```

#### Specific Columns

You can also target a specific columns to be updated by passing the list of fields to be included in the `fields` argument.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var people = GetPeople();
    var fields = Field.Parse<Person>(e => new
    {
        e.Id,
        e.Name,
        e.DateInsertedUtc
    });
	var updatedRows = connection.UpdateAll<Person>(entities: people,
		fields: fields);
}
```

Or via dynamics.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var people = GetPeople();
	var updatedRows = connection.UpdateAll("[dbo].[Person]",
		entities: people,
		fields: Field.From("Id", "Name", "DateInsertedUtc"));
}
```

#### Batch Size

You can adjust the size of your batch by simply passing the value at the `batchSize` argument. By default, the value is `10` (found at `Constant.DefaultBatchOperationSize`).

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var people = GetPeople();
	var updatedRows = connection.UpdateAll(people,
		batchSize: 30);
}
```

#### Table Hints

To pass a hint, simply write the table-hints and pass it in the `hints` argument.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var updatedRows = connection.UpdateAll<Person>(person,
		hints: "WITH (TABLOCK)");
}
```

Or, you can use the [SqlServerTableHints](/class/sqlservertablehints) class.

```csharp
using (var connection = new SqlConnection(connectionString).EnsureOpen())
{
	var updatedRows = connection.UpdateAll<Person>(person,
		hints: SqlServerTableHints.TabLock);
}
```
