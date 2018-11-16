# SQLLoadGenerator

This tool generates an OLTP workload to be used with Replay.

## Requirements

* Java 8

## Installation

* Compile SQLLoadGenerator

### Compile SQLLoadGenerator

```bash
cd /path/to/work_area
/path/to/javac SQLLoadGenerator.java
```

## Usage

### Run

```bash
cd /path/to/work_area
/path/to/java SQLLoadGenerator
```

## Configuration

The configuration of SQLLoadGenerator is done in the ```sqlloadgenerator.properties``` file, which supports the following
options.

Alternative, SQLLoadGenerator can be configured through another properties file and executed with

```bash
cd /path/to/work_area
/path/to/java SQLLoadGenerator -c myprops.properties
```

### clients

The number of clients that should be generated. Default is ```10```.

### rows

The global number of rows in each table. Default is ```1000```.

### statements

The number of statements for each client. Default is ```10000```.

### mspt

The maximum of statements per transaction. Default is ```5```.

### mix.select

The mix for ```SELECT``` statements.  Default is ```70```.

### mix.update

The mix for ```UPDATE``` statements.  Default is ```15```.

### mix.insert

The mix for ```INSERT``` statements.  Default is ```10```.

### mix.delete

The mix for ```DELETE``` statements.  Default is ```5```.

### commit

The mix for ```COMMIT``` transactions.  Default is ```100```.

### rollback

The mix for ```ROLLBACK``` transactions.  Default is ```0```.

### table.X

Define a table called X. Example

```
table.test=This is test table
```

### X.col.Y

Define a column number Y for table X. Example

```
test.col.1=a
```

### X.col.Y.type

Define the column type for column number Y in table X. Example

```
test.col.1.type=text
```

Default data type is ```int```.

### X.col.Y.description

Define the column description for column number Y in table X. Example

```
test.col.1.description=This is my column
```

### X.rows

The number of rows for table X. Example

```
test.rows=1000000
```

### index.X.Y

Define an index for table X. Example

```
index.test.1=a, b
```

## Workload

The workload is located in the ```/path/to/work_area/sqlloadgenerator``` directory, or in the directory
named after the specified property file name.

The workload can then be executed using [Replay](https://github.com/jesperpedersen/postgres-tools/tree/master/Replay).

In order to setup the DDL and data for the workload execute:

```
createuser -P username
createdb -E UTF8 -O username test
psql -U username -f sqlloadgenerator/ddl.sql test
psql -U username -f sqlloadgenerator/data.sql test
```

and then proceed with the [Replay](https://github.com/jesperpedersen/postgres-tools/tree/master/Replay) setup.