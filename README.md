# dokku Neo4j plugin

Neo4j plugin for dokku. Currently defaults to installing Neo4j 2.3.0

Project: https://github.com/progrium/dokku

Fork of https://github.com/dokku/dokku-redis

## installation
```
cd /var/lib/dokku/plugins
git clone https://github.com/creativecodingos/dokku-neo4j-plugin.git neo4j
dokku plugins-install
```


## commands
```
neo4j:alias <name> <alias>       Set an alias for the docker link
neo4j:create <name>              Create a Neo4j Community service
neo4j:create-enterprise <name>   Create a Neo4j Enterprise service
neo4j:destroy <name>             Delete the Neo4j service and stop its container if there are no links left
neo4j:link <name> <app>          Link the Neo4j service to the app
neo4j:unlink <name> <app>        Unlink the Neo4j service from the app
neo4j:backup <name>              Executes a backup of the Neo4j service database.
neo4j:s3config <name>            Provide coordinates to store the backup files on Amazon S3
neo4j:export <name> > <file>     Export a dump of the Neo4j service database
neo4j:import <name> < <file>     Import a dump into the Neo4j service database
neo4j:connect <name>             Connect via neo4j-shell to a Neo4j service
neo4j:logs <name> [-t]           Print the most recent log(s) for this service
neo4j:restart <name>             Graceful shutdown and restart of the Neo4j service container
neo4j:info <name>                Print the connection information
neo4j:list                       List all Neo4j services
neo4j:clone <name> <new-name>    Create container <new-name> then copy data from <name> into <new-name>
neo4j:expose <name>              Expose a Neo4j service on random ports
neo4j:unexpose <name>            Unexpose a previously exposed Neo4j service
neo4j:start <name>               Start a previously stopped Neo4j service
neo4j:stop <name>                Stop a running Neo4j service
```

# usage
```bash
# create a neo4j community edition service named graph
dokku neo4j:create graph            # Server side
ssh dokku@server neo4j:create graph # Client side

# create a neo4j enterprise edition service named enterprise-graph
dokku neo4j:create enterprise-graph

# you can also specify the Neo4j version, back to 2.2.1
export NEO4J_IMAGE_VERSION="2.2.3"
dokku neo4j:create graph

# get service information as follows
dokku neo4j:info graph

# lets assume the ip of our neo4j service is 172.17.0.1

# a neo4j service can be linked to a
# container this will use native docker
# links via the docker-options plugin
# here we link it to our 'playground' app
# NOTE: this will restart your app
dokku neo4j:link graph playground

# the above will expose the following environment variables
#
#   NEO4J_URL=http://172.17.0.1:7474
#   NEO4J_NAME=/graph/DATABASE
#   NEO4J_PORT=tcp://172.17.0.1:7474
#   NEO4J_PORT_7474_TCP=tcp://172.17.0.1:7474
#   NEO4J_PORT_7474_TCP_PROTO=tcp
#   NEO4J_PORT_7474_TCP_PORT=7474
#   NEO4J_PORT_7474_TCP_ADDR=172.17.0.1

# you can customize the environment
# variables through a custom docker link alias
dokku neo4j:alias graph NEO4J_DATABASE

# you can also unlink a neo4j service
# NOTE: this will restart your app
dokku neo4j:unlink graph playground

# you can tail logs for a particular service
dokku neo4j:logs graph
dokku neo4j:logs graph -t # to tail

# you can dump the database
# (no service restarting with enterprise edition)
dokku neo4j:export graph > backup.tar.gz

# you can import a dump
# (restarts the service)
dokku neo4j:import graph < backup.tar.gz

# you can execute a backup
# (no service restarting with enterprise edition)
dokku neo4j:backup graph

# and you can have your backup files automatically stored on AWS S3
# providing S3 coordinates via:
dokku neo4j:s3config graph

# you can clone an existing database to a new one
dokku neo4j:clone graph new_graph

# finally, you can destroy the container
dokku neo4j:destroy graph
```
