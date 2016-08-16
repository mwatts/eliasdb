EliasDB
=======
EliasDB is a graph based database which aims to provide a lightweight solution for projects which want to store their data as graph.


Features
--------
- Build on top of a fast key-value store which supports transactions and memory-only storage.
- Data is stored in nodes (key-value objects) which are connected via edges.
- Stored graphs can be separated via partitions.
- Stored graphs support cascading deletions - delete one node and all its "children".
- All stored data is indexed and can be quickly searched via a full text phrase search.
- For more complex queries EliasDB has an own query language called EQL with an sql-like syntax.
- Written in Go from scratch. No third party libraries were used apart from Go's standard library.
- The database can be embedded or used as a standalone application.
- When used as a standalone application it comes with an internal HTTPS webserver which
  provides a REST API and a basic file server.
- When used as an embedded database it supports transactions with rollbacks, iteration of data
  and rule based consistency management.


Getting Started (standalone application)
----------------------------------------
You can download a precompiled package for Win64 [here](https://raw.githubusercontent.com/krotik/eliasdb/master/res/eliasdb_v0_8.zip).

Extract it and execute the executable. The executable should automatically create 3 subfolders and a configuration file. It should start an HTTPS server on port 9090. To see a terminal point your webbrowser to:
```
https://localhost:9090/db/term.html
```
After accepting the self-signed certificate from the server you should see a web terminal. EliasDB can be stopped with a simple CTRL+C or by overwriting the content in eliasdb.lck with a single character.

### REST API:

The terminal uses a REST API to communicate with the backend. The REST API can be browsed using a dynamically generated swagger.json definition (https://localhost:9090/db/swagger.json). You can browse the API of EliasDB's latest version [here](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/krotik/eliasdb/master/doc/swagger.json#/default).

### Configuration
EliasDB uses a single configuration file called eliasdb.config.json. After starting EliasDB for the first time it should create a default configuration file. Available configurations are:

| Configuration Option | Description |
| --- | --- |
| EnableWebFolder | Flag if the files in the webfolder /web should be served up by the webserver. If false only the REST API is accessible. |
| EnableWebTerminal | Flag if the web terminal file /web/db/term.html should be created. |
| HTTPSCertificate | Name of the webserver certificate which should be used. A new one is created if it does not exist. |
| HTTPSHost | Hostname the webserver should listen to. This host is also used in the dynamically generated swagger definition. |
| HTTPSKey | Name of the webserver private key which should be used. A new one is created if it does not exist. |
| HTTPSPort | Pot the webserver should listen on. |
| LocationDatastore | Directory for datastore files. |
| LocationHTTPS | Directory for the webserver's SSL related files. |
| LocationWebFolder | Directory of the webserver's webfolder. |
| LockFile | Lockfile for the webserver which will be watched duing runtime. Replacing the content of this file with a single character will shutdown the webserver gracefully. |
| MemoryOnlyStorage | Flag if the datastore should only be kept in memory. |
| ResultCacheMaxAgeSeconds | EQL queries create result sets which are cached. The value describes the amount of time a result is kept in the cache. |
| ResultCacheMaxSize | EQL queries create result sets which are cached. The value describes the amount results which can be kept in the cache. |

Note: It is not (and will never be) possible to access the REST API via HTTP.

Further Reading
---------------
- A design document which describes the different components of the graph database. [Link](/doc/elias_db_design.md)
- A reference for the EliasDB query language EQL. [Link](/doc/eql.md)

License
-------
EliasDB source code is available under the [Mozilla Public License](/LICENSE).