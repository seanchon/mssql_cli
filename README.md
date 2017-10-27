# mssql_cli
A way to run queries and execute commands against an MSSQL database.


## Important Update - October 24, 2017
PyPI releases beyond 0.3 may not be backwards compatible with features from this project.

In the spirit of open source, the ownership of the PyPI package mssql_cli has been handed over to a Microsoft SQL Server team with plans to create a new package using the same name to be released under the https://github.com/dbcli project. See https://github.com/seanchon/mssql_cli/issues/1 for conversation details.

We have decided that the least impactful way to go about this is to leave the existing PyPI package releases that relate to this repository in place (releases 0.1, 0.2, and 0.3) so that any users currently using this package can continue to use these releases. Any new development will be added to a new major release and beyond (ex. 1.x.x) and may not be backwards compatible.

In order to install the PyPI packages linked to this repository, please be sure to download the correct version or link your requirements to the correct version.

Example:
```
pip install mssql_cli==0.3
```


## Code Example
```python
import datetime  # used for an example below
from mssql_cli import DBRead, DBWrite

read_connection = DBRead(host='some_host', user='some_user', password='some_password', database='some_database')
write_connection = DBWrite(host='some_host', user='some_user', password='some_password', database='some_database')

results = read_connection.query("SELECT * FROM some_table")
more_results = write_connection.query("SELECT * FROM some_table")

write_connection.execute("INSERT INTO [some_table] ([name], [phone_number], [time]) VALUES ('Prince', '111-111-1111', '1999-12-31 23:59:59')")

# insert_results() will create an insert statement based off of a table name and kwargs and execute the resulting statement.
write_connection.insert_results(table='some_table', name='Prince', phone_number='111-111-1111', time=datetime.datetime.utcnow().strftime('%Y-%m-%d %H:%M:%S'))

read_connection.close()
write_connection.close()
```

## Motivation
This library exists to run queries and execute commands against an MSSQL database.

## Installation
This package requires pymssql, which has a dependency on FreeTDS. Instructions on installing FreeTDS can be found here: http://pymssql.org/en/latest/freetds.html.

pip install mssql_cli

## License
MIT
