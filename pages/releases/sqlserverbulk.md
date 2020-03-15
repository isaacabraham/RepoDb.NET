---
layout: page
title: Releases for SQL Server Bulk (RepoDb)
permalink: /releases/sqlserverbulk
---

## Releases for RepoDb.SqlServer.BulkOperations

#### RepoDb.SqlServer.BulkOperations (v1.0.4)

- Referenced the latest version of RepoDb.Core (v1.10.10).
- Fully supported the Bulk Operations (`BulkDelete`, `BulkInsert`, `BulkMerge` and `BulkUpdate`) for both System.Data.SqlClient and Microsoft.Data.SqlClient namespace.
- Auto set the options to `SqlBulkCopyOptions.KeepIdentity` for `BulkDelete`, `BulkMerge` and `BulkUpdate` (if there an identity primary/column from the DB).
- Used an underscore over dashes when composing the temporary/pseudo tables.
- Added an extensive Integration Tests for all Bulk methods (both SDS and MDS namespaces).


#### RepoDb.SqlServer.BulkOperations (v1.0.4-beta3)

- Minor updates for `BulkUpdate`. Used an underscore over dashes when composing the temporary/pseudo tables.


#### RepoDb.SqlServer.BulkOperations (v1.0.4-beta2)

- Auto set the options to `SqlBulkCopyOptions.KeepIdentity` for `BulkDelete`, `BulkMerge` and `BulkUpdate` (if there an identity primary/column from the DB).
- Used an underscore over dashes when composing the temporary/pseudo tables.


#### RepoDb.SqlServer.BulkOperations (v1.0.4-beta1)

- Initial full support to the Bulk Operations (`BulkDelete`, `BulkInsert`, `BulkMerge` and `BulkUpdate`).


#### RepoDb.SqlServer.BulkOperations (v1.0.3)

- Upgrade the references to Microsoft.Data.SqlClient (v1.1.1) and RepoDb.SqlServer (v1.0.3).


#### RepoDb.SqlServer.BulkOperations (v1.0.2)

- Resumed the support to System.Data.SqlClient namespace.


#### RepoDb.SqlServer.BulkOperations(v1.0.1)

- Initial release for RepoDb.SqlServer.BulkOperations.


#### RepoDb.SqlServer.BulkOperations (v1.0.0)

- Initial release for RepoDb.SqlServer.BulkOperations.