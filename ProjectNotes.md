


From the spring boot docker container, & mysql container:
install docker
./mvnw package && java -jar target/gs-spring-boot-docker-0.1.0.jar
install intellij official docker plugin
  run new server container /sbrct1  dw$
docker run \
    --name mesql3 \
    -p "3306:3306"\
    -e MYSQL_ROOT_PASSWORD=password \
    mysqld --default-authentication-plugin=mysql_native_password \
    -e MYSQL_DATABASE=db_example \
    -e MYSQL_USER=springuser \
    -e MYSQL_PASSWORD=ThePassword \
    mysqld --default-authentication-plugin=mysql_native_password \
    -d mysql:latest

    
  run already created:
docker start msql

  run access container $ 
docker run -it --link mesql:mysql --rm mysql sh -c 'exec mysql -h"$MYSQL_PORT_3306_TCP_ADDR" -P"$MYSQL_PORT_3306_TCP_PORT" -uroot -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"'

docker run --name mySqlDock01 -e MYSQL_ROOT_PASSWORD=password -d mysql:tag

added a DB called toot, and some tables. Closing/opening container data was retained.

in application.properties, 
Here, spring.jpa.hibernate.ddl-auto can be none, update, create, create-drop, refer to the Hibernate documentation for details.
-none This is the default for MySQL, no change to the database structure.
-update Hibernate changes the database according to the given Entity structures.
-create Creates the database every time, but don’t drop it when close.
-create-drop Creates the database then drops it when the SessionFactory closes.
-We here begin with create because we don’t have the database structure yet. After the first run, we could switch it to update or none according to program requirements. Use update when you want to make some change to the database structure.
-The default for H2 and other embedded databases is create-drop, but for others like MySQL is none
-It is good security practice that after your database is in production state, you make this none and revoke all privileges from the MySQL user connected to the Spring application, then give him only SELECT, UPDATE, INSERT, DELETE.

```plantuml
digraph Test {
A -> B
}
```

brew install graphviz for markdown diagram, no go on intellij

If you are using Maven, you can run the application using ./mvnw spring-boot:run. Or you can build the JAR file with ./mvnw clean package. Then you can run the JAR file:

java -jar target/gs-accessing-data-mysql-0.1.0.jar

Trying to access docker mySQL container with sequel pro, after lots of container ip-address confusion, received error:
Authentication plugin 'caching_sha2_password' cannot be loaded
google implies sequel pro doesn't have the correct password complexity.
2 possible fixes: Use unreleased build of sequel pro, change the mysql build to contain a password sequel pro can use.

