# csvsql
A command line utility to query one or more csv files using SQL.


## Motivation

Sometimes the data one seeks span across multiple csv files.  Such scenario is
common in databases where seeking data that span across multiple tables is done
using SQL queries.  This utility lets one accomplish a similar task by issuing
SQL queries on csv files.


## Basic Usage

Given the following csv files `names.csv` and `emails.csv`,
```csv
ID,FIRST_NAME,LAST_NAME
1001,John,Doe
1002,Jane,Smith
```
```csv
ID,EMAIL
1001,"jdoe@email.com"
1002,"jsmith@email.com"
```

csvsql can join the two csv files as below:
```sh
$ csvsql names.csv emails.csv -c "select * from names, emails where names.ID=emails.ID"
ID,FIRST_NAME,LAST_NAME,ID,EMAIL
1001,John,Doe,1001,jdoe@email.com
1002,Jane,Smith,1002,jsmith@email.com
```

and filter them:
```sh
$ csvsql names.csv emails.csv -c "select * from names, emails where names.ID=emails.ID and LAST_NAME='Doe'"
ID,FIRST_NAME,LAST_NAME,ID,EMAIL
1001,John,Doe,1001,jdoe@email.com
```

See the man page for other `csvsql` options and information.


# Interactive Mode

If the `-c` command is omitted, `csvsql` enter into an interactive mode where
one SQL command may be issued per line.

The interactive mode also supported a few other convenience commands.  Type
`help` on the interactive prompt for more information.


# SQL Syntax

`csvsql` uses [SQLite] to handle SQL commands.  See the its webpage for
the full list of supported SQL commands.


[SQLite]: https://www.sqlite.org/lang.html
