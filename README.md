![The superpower nobody uses - FileMaker 2026 and SQL](media/super_power_2026.png)

# FileMaker 2026 SQL CRUD

Runnable FileMaker examples showing that SQL through ODBC can create and alter
FileMaker schema, create relationships, and perform CRUD operations.

Created by [Dimitris Kokoutsidis](https://github.com/DimitrisKok).

Companion repository for:
[The Forgotten Superpower of FileMaker 2026: SQL CRUD](https://axelar.eu/the-forgotten-superpower-of-filemaker-2026-sql-crud/)

## Open the FileMaker Files

Both supplied `.fmp12` files use these FileMaker credentials:

- **Account Name:** `Admin`
- **Password:** `admin`

These credentials are for the local demonstration files only. Do not reuse
them in production.

## What This Demonstrates

The examples use FileMaker's `Execute SQL` script step, the `ExecuteSQL()`
calculation function, FileMaker's ODBC driver, and MariaDB to demonstrate:

- creating a FileMaker table, fields, defaults, and a relationship with SQL
- inserting, reading, updating, and deleting records
- creating and dropping a field index
- adding and removing fields with `ALTER TABLE`
- generating SQL at runtime with `Calculated SQL Text`
- preserving apostrophes safely in calculated SQL values
- removing a test table with `DROP TABLE`
- the credential-model difference between FileMaker 2025 and 2026

These are working FileMaker examples, not pseudocode.

## Repository Contents

### FileMaker files

- `filemaker/Execute_SQL_Example_2025_v1_0.fmp12`
- `filemaker/Execute_SQL_Example_2026_v1_0.fmp12`

### Scripts

| Example | Demonstration |
|---|---|
| 1 | `CREATE TABLE`, fields, defaults, containers, and a relationship |
| 2 | `INSERT` ten records |
| 3 | `UPDATE` one record by primary key |
| 4 | `DELETE` one record by primary key |
| 5 | `CREATE INDEX` |
| 6 | `DROP INDEX` |
| 7 | `ALTER TABLE ADD COLUMN` |
| 8 | `ALTER TABLE DROP COLUMN` |
| 9 | Read with the `ExecuteSQL()` calculation function |
| 10 | Calculated SQL `INSERT` into MariaDB |
| 11 | Calculated SQL `UPDATE` in MariaDB |
| 12 | `DROP TABLE` cleanup |

`examples/Execute_SQL_Example_1_2025.fmscript` contains the FileMaker 2025
version of Example 1.

### MariaDB fixture

`fixtures/gemini_mariadb_fixture.sql` creates:

- the `gemini` database
- the `persons` table
- four seed records
- the restricted local demonstration account used by Examples 10 and 11

The account can only select, insert, and update `gemini.persons`. It cannot
delete records or alter schema.

## Setup

### FileMaker self-ODBC examples

1. Install the matching FileMaker ODBC driver.
2. Open the supplied FileMaker file.
3. Enable ODBC/JDBC sharing for the file.
4. Create a 64-bit System DSN:
   - `odbcSelf2026` for the 2026 file
   - `odbcSelf2025` for the 2025 file
5. Point the DSN to the corresponding open FileMaker file.
6. Run the examples in numerical order.

Example 1 creates the table used by the later examples. Example 12 removes it
after the sequence is complete.

### MariaDB calculated-SQL examples

1. Run `fixtures/gemini_mariadb_fixture.sql` as a MariaDB administrator.
2. Create a 64-bit System DSN named `gemini` that points to the local `gemini`
   database.
3. Run Example 10, then Example 11, in the same FileMaker session.

Example 10 stores its generated email in a global FileMaker variable. Example
11 uses that value to update exactly the row Example 10 inserted.

## Security

These files are demonstrations for a local development environment.

- They contain intentionally weak demonstration credentials such as
  `Admin` / `admin` and `ai2fm_example` / `ai2fm-demo-only`.
- Never reuse these credentials in production or expose the sample services to
  an untrusted network.
- Use a copy of the FileMaker files while learning.
- Examples 4, 8, and 12 are destructive. Read them before running them.
- The MariaDB fixture does not contain an administrator password.

SHA-256 hashes for all published artifacts are in `CHECKSUMS.sha256`.

## File Format

The `.fmscript` files use the human-readable syntax developed for
[fmscript.org](https://fmscript.org/). They can be inspected and versioned as
ordinary text.

## Licensing

No reuse license is granted by this repository at this time. Public access does
not waive the author's copyright. Contact Dimitris Kokoutsidis before
redistribution or commercial use.
