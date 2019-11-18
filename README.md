# Forward Pagination in a Stateless REST service
Working on a backend REST service that handles access to Cassandra while passing results back to a web front-end for display? You've come to the right place if you have any paging functionality in that web application. This example shows how to page the results returned by Cassandra in a web application via a backend REST service.  


Contributor(s): [Tomasz Lelek](https://github.com/tomekl007), [Carlos Diaz](https://github.com/crdiaz324)

## Objectives
* Demonstrate how to use the paging state returned by Cassandra and encode it in HTTP URLs for a REST application.
* Pagination is "forward-only", which means "give me X results, and then the next X results, and then the next X results ..."


## Project Layout
*  [ForwardPagingRestUi.java](/src/main/java/com/datastax/examples/ForwardPagingRestUi.java) - The main application which creates and populates a schema and starts the rest service.


## How this Sample Works
This application creates a table called `forward_paging_rest_ui` in the `examples` keyspace.  It then populates the table with 3 users and 49 videos for each user. It then starts a REST service for that data, accessible via the following endpoint.

`http://localhost:8080/users` 

To explore the paging functionality, use the following and walk from there:

`curl -i http://localhost:8080/users/1/videos`

## Setup and Running

### Prerequisites
* Java 8
* A Cassandra, DDAC, DSE cluster or Apollo database ( docker is a nice option for local install - [see docs](https://docs.datastax.com/en/docker/doc/docker/dockerQuickStart.html) )

### Running
This first step in the process is to build and package the application.  This can be done using the following command from within the root directory of this repo:

`mvn package`

This will compile the code and package it as a fat JAR file (located in `target/forward-paging-rest-ui-1.0-SNAPSHOT-jar-with-dependencies.jar), 
which contains all the dependencies needed to run the application.

Once you have compiled the application, you can run it with:

`java -jar target/forward-paging-rest-ui-1.0-SNAPSHOT-jar-with-dependencies.jar`

By default, it will try to your cluster at 127.0.0.1:9042, however you can change the contact points by adding a file called application.conf to your class path with the following contents:

```
datastax-java-driver {
   basic {
     contact-points = [ "1.2.3.4:9042", "5.6.7.8:9042" ]
     load-balancing-policy.local-datacenter = datacenter1
   }
 }
 ```

If you would like to connect to an Apollo cluster instead, simply follow the [Switch connection between on-prem and cloud example](https://github.com/DataStax-Examples/switch-connection-java)
