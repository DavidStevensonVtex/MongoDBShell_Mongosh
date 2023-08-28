# [MongoDB Shell (mongosh)](https://www.mongodb.com/docs/mongodb-shell/) 

```
$ENV:PATH += ";C:\Program Files\mongosh"
mongosh
# mongosh "mongodb://127.0.0.1:27017/"
# mongosh --port 27017
```

## Specify Connection Options

### Connect With Authentication

```mongosh "mongodb://mongodb0.example.com:28015" --username alice --authenticationDatabase admin```

To provide a password as part of the connection command instead of using the prompt, use the --password option. 

### Connect with OpenID Connect

To connect to a deployment using OpenID Connect, use the --authenticationMechanism option and set it to MONGODB-OIDC. mongosh redirects you to a browser where you enter your identity provider's log-in information.

```mongosh "mongodb://localhost/" --authenticationMechanism MONGODB-OIDC```

### Connect with LDAP

* Set --username to a username that respects the security.ldap.authz.queryTemplate, or any configured security.ldap.userToDNMapping  template.

* Set --password to the appropriate password. If you do not specify the password to the --password command-line option, mongosh prompts you for the password.

* Set --authenticationDatabase to $external. The $external argument must be placed in single quotes, not double quotes, to prevent the shell from interpreting $external as a variable.

* Set --authenticationMechanism to PLAIN.

Include the --host and --port of the MongoDB deployment, along with any other options relevant to your deployment.

For example, the following operation authenticates to a MongoDB deployment running with LDAP authentication and authorization:

```mongosh --username alice@dba.example.com --password  --authenticationDatabase '$external' --authenticationMechanism "PLAIN"  --host "mongodb.example.com" --port 27017```

### Connect to a Replica Set

To connect to a replica set, you can either:

* Use the DNS Seedlist Connection Format.
* Explicitly specify the replica set name and members in the connection string.

Option 1: DNS Seedlist Format
To use the DNS seedlist connection format, include the +srv modifier in your connection string.

For example, to connect to a replica set on server.example.com, run the following command:

```mongosh "mongodb+srv://server.example.com/"```

Option 2: Specify Members in Connection String

You can specify individual replica set members in the 
connection string.

For example, to connect to a three-member replica set named replA, run the following command:

```mongosh "mongodb://mongodb0.example.com.local:27017,mongodb1.example.com.local:27017,mongodb2.example.com.local:27017/?replicaSet=replA"```


### Connect Using TLS

To connect to a deployment using TLS, you can either:

*Use the DNS Seedlist Connection Format. The +srv connection string modifier automatically sets the tls option to true for the connection.

For example, to connect to a DNS seedlist-defined replica set with tls enabled, run the following command:

```mongosh "mongodb+srv://server.example.com/"```

* Set the --tls option to true in the connection string.

For example, to enable tls with a connection string option, run the following command:

```mongosh "mongodb://mongodb0.example.com:28015/?tls=true"```

* Specify the --tls command-line option.

For example, to connect to a remote host with tls enabled, run the following command:

```mongosh "mongodb://mongodb0.example.com:28015" --tls```

### Connect to a Specific Database

To connect to a specific database, specify a database in your connection string URI path . If you do not specify a database in your URI path, you connect to the test database.

For example, to connect to a database called qa on localhost, run the following command:

```mongosh "mongodb://localhost:27017/qa"```

## Connect to a Different Deployment

If you are already connected to a deployment in the MongoDB Shell, you can use the [Mongo()](https://www.mongodb.com/docs/manual/reference/method/Mongo/#mongodb-method-Mongo)  or [connect()](https://www.mongodb.com/docs/manual/reference/method/connect/)  method to connect to a different deployment from within the MongoDB Shell.

To learn how to connect to a different deployment using these methods, see [Open a New Connection](https://www.mongodb.com/docs/mongodb-shell/write-scripts/#std-label-mdb-shell-open-new-connections-in-shell).

## Verify Current Connection

To verify your current database connection, use the [db.getMongo()](https://www.mongodb.com/docs/manual/reference/method/db.getMongo/#mongodb-method-db.getMongo)  method.

The method returns the [connection string URI](https://www.mongodb.com/docs/manual/reference/connection-string/)  for your current connection.

## Disconnect from a Deployment
To disconnect from a deployment and exit mongosh, perform one of the following actions:
* Type .exit, exit, or exit().
* Type quit or quit().
* Press Ctrl + D.
* Press Ctrl + C twice.

## Non-genuine Deployments
The shell displays a warning message when you connect to non-genuine MongoDB instances. Non-genuine instances may behave differently from the official MongoDB instances due to missing, inconsistent, or incomplete features.