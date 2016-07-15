# LogAnalyzer

This tool generates HTML reports about queries run against PostgreSQL.

You may want to take a look at [pgBadger](http://dalibo.github.io/pgbadger/) too.

## Requirements

* Java 8
* PostgreSQL

## Installation

* Compile LogAnalyzer

### Compile QueryAnalyzer

```bash
cd /path/to/work_area
/path/to/javac -classpath LogAnalyzer.java
```

## Usage

### Configure PostgreSQL

Configure PostgreSQL with the following settings in ```postgresql.conf```

```
log_destination = 'stderr'
log_directory = 'pg_log'
log_filename = 'postgresql.log'
log_rotation_age = 0
log_min_duration_statement = 0
log_line_prefix = '%p [%t] [%x] '
```

and do a run of the SQL statement that you want to analyze.

### Run

```bash
cd /path/to/work_area
/path/to/java LogAnalyzer postgresql.log
```

## Report

The report is located in the ```/path/to/work_area/report``` directory. The main report is ```index.html```

The report shows

* The distribution of ```SELECT```, ```UPDATE```, ```INSERT``` and ```DELETE```
* The times spent in ```PARSE```, ```BIND``` and ```EXECUTE``` phase
* The number of executed queries, and the query itself
* The interaction of each backend