Neo4j plugin for Dokku
----------------------

WIP....
----------------------

Project: https://github.com/progrium/dokku

Installation
------------
```
cd /var/lib/dokku/plugins
git clone https://github.com/creativecodingos/dokku-neo4j-plugin.git neo4j
dokku plugins-install
```


Commands
--------
```
$ dokku help
      neo4j:create <n4j>             Create a Neo4j Community container
      neo4j:create:enterprise <n4j>  Create a Neo4j Enterprise container
      neo4j:delete <n4j>             Delete specified Neo4j container
      neo4j:info <n4j>               Display container information
      neo4j:link <app> <n4j>         Link an app to a Neo4j container
      neo4j:expose <n4j> <domain>    Exposes a Neo4j database trough Nginx
      neo4j:hide <n4j>               Hides a Neo4j database from external access
      neo4j:backup <n4j>             Backup a Neo4j database
```

Simple usage
------------

Create a new Container:
```
$ dokku neo4j:create mygraph            # Server side
$ ssh dokku@server neo4j:create mygraph # Client side

-----> Neo4j Community container created: neo4j/mygraph

       Host: 172.16.0.104
       Rest port: 7474
```

Environment Variables
---------------------
```
NEO4J_URL
```