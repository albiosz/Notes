#command

##java
java -version
java -jar \*.jar - to run a jar
java -jar \*.jar --server.port=<port_number>

##maven
mvn install - install dependencies

mvn spring-boot:run - run spring application
mvn install - create jar in target folder

##postgres
.\psql.exe -U postgres > password: 0000 - command use to login
create database <name>; 

\du - users
\l - databases
\d - relations
\d student - see details of chosen relation
\c <db_name> - connect to database
\x - expand display


GRANT ALL PRIVILEGES ON DATABASE <db_name> TO postgres;

##LOMBOK - dependency which generates basic code like constructors, setters and getters
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>1.18.22</version>
	<scope>provided</scope>
</dependency>

@AllArgsConstructor
@Getter
@Setter
@ToString


##trick
ctrl + . - you can add new function to a class which was not previously declared

ctrl + shift + space - show required parameters

##application.properties
spring.output.ansi.enabled=always - colorful logs in console everywhere


