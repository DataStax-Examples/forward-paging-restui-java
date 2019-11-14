# Forward Pagination in a Stateless REST service
This example application shows how to paginate the results returned by Cassandra in a REST UI.  


Contributors: [Tomasz Lelek](https://github.com/tomekl007), [Carlos Diaz](https://github.com/crdiaz324)

## Objectives
* To demonstrate how to paginate over the paging state returned by Cassandra, and encode it in HTTP URLs for a REST application.
* Pagination will be forward-only   


## Project Layout
*  [ForwardPagingRestUi.java](/src/main/java/com/datastax/examples/ForwardPagingRestUi.java) - The main application which will create and populate a schema and start the rest service.


## How this Sample Works
This appication will create a table called forward_paging_rest_ui in the examples keyspace.  It will then populate the table with 3 users and 49 videos each.  Then it will start a
rest service on http://localhost:8080/users.  

To explore this example, start with the following request and walk from there:
curl -i http://localhost:8080/users/1/videos

## Setup and Running

### Prerequisites
* Java 8
* A DSE/DDAC/C* cluster or an Apollo database to connect to with the appropriate connection information

### Running
This first step in the process is to build and package the application.  This can be done using the following command from within the root directory of this repo:

`mvn package`

This will compile the code and package it as a fat JAR file (located in `target/forward-paging-rest-ui-1.0-SNAPSHOT-jar-with-dependencies.jar), 
which contains all the dependencies needed to run the application.

Once you have compiled the application, you can run it with:

`java -jar target/forward-paging-rest-ui-1.0-SNAPSHOT-jar-with-dependencies.jar`

By default, it will try to your cluster at 127.0.0.1:9042, however you can change the contact points by adding a file called application.conf 
to your class path with the following contents:

`datastax-java-driver {
   basic {
     contact-points = [ "1.2.3.4:9042", "5.6.7.8:9042" ]
     load-balancing-policy.local-datacenter = datacenter1
   }
 }`

If you would like to connect to an Apollo cluster instead, simply follow the [switching-connection-configurations-java-driver](https://github.com/DataStax-Examples/switching-connection-configurations-java-driver-oss-v3)
