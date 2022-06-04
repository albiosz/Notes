# Specify its an entity 
@Entity(name = "Student")

# Specify which field is the id
@Id

# Creates sequence in database
@SequenceGenerator(
	name = <name>,
	sequenceName = <seq_name>,
	allocationSize = <size>
)

# Uses sequence from database
@GeneratedValue(
    strategy = GenerationType.SEQUENCE,
	generator = "student_sequence_generator"
)

#Specify details about a column
@Column(
    name = "email",
    nullable = false,
    columnDefinition = "TEXT",
    unique = true
)

# Repository class
package com.example.jpa.Student;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface StudentRepository extends JpaRepository<Student, Long> {
  
}


spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/jpa
    username:
    password: 
  jpa:
    hibernate:
      ddl-auto: create-drop <- it makes to drop the database after finishing the script
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
        format_sql: true
    show-sql: true



# JPA course

## Querying Data

### Query Methods
There are methods which can be added to Repository.java for which we don't have to add @Query

public Optional<Student> findByEmail(String email);
Optional<Student> - Die Email ist einzigartig/eindeutig, deswegen als der Output, wird man einen Student oder nix bekommen.

repository
    .findById(2L)
    .ifPresentOrElse(
      System.out::println,
      () -> System.out.println("Student with ID 2 not found")
  );

### Query Methods p 2
Man kann die Funktionen der Methoden bei dem Name erstellen. z. B.

repository.findByFirstNameEqualsAndAgeLessThan("Albert", 27)

interface PersonRepository extends Repository<Person, Long> {

  List<Person> findByEmailAddressAndLastname(EmailAddress emailAddress, String lastname);

  // Enables the distinct flag for the query
  List<Person> findDistinctPeopleByLastnameOrFirstname(String lastname, String firstname);
  List<Person> findPeopleDistinctByLastnameOrFirstname(String lastname, String firstname);

  // Enabling ignoring case for an individual property
  List<Person> findByLastnameIgnoreCase(String lastname);
  // Enabling ignoring case for all suitable properties
  List<Person> findByLastnameAndFirstnameAllIgnoreCase(String lastname, String firstname);

  // Enabling static ORDER BY for a query
  List<Person> findByLastnameOrderByFirstnameAsc(String lastname);
  List<Person> findByLastnameOrderByFirstnameDesc(String lastname);
}


### JPQL Query Methods
mehr darüber in Dokumentation:
https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.query-methods.query-creation

Query keywords:
https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repository-query-keywords

### @Query
Man kann auch queries mit @Query erstellen. Es wird empfohlen, als
@Query("select s from student s where s.email = ?1")
es deutlicher als
Optional<Student> findByEmail(String email) ist.

Die Attribute sollen nicht gleich wie in der Datenbank (first_name), sonder wie Attribute in der Klasse (firstName) geschrieben werden.

### Native Queries

// Native query
@Query(value = "select * from student where first_name = ?1 and age < ?2")
List<Student> findByFirstNameEqualsAndAgeLessThanNative(String name, Integer age);

Native queries habe eine große Nachteile. Sie sind die Databank System spezifisch. Deswegen wenn ich eine native Querry für Postgres habe, kann man nicht sicher sein, ob es auch mit MySql funktioneren wird.

### Named Parameters
Statt ?1 Parameter in einem Querry, kann man :name benutzen.

// Named parameters
@Query("select s from Student s where s.firstName = :name and s.age < :age")
List<Student> findByFirstNameEqualsAndAgeLessThanNamed(
	@Param("name") String name,
	@Param("age") Integer age
);

### @Modifying

Wenn wir nicht Data lesen wollen, sonder modifizieren, mussen wir mit @Query auch @Modifying und @Transactional benutzen;

// Modifying
@Transactional
@Modifying
@Query("delete from Student s where s.id = ?1")
int deleteStudentById(Long id);

Es löscht passende Rekorden in der Datenbank und gibt die Zahl gelöchten Rekorden.


## Sorting and Pagination

### Faker
https://github.com/DiUS/java-faker
Faker ist nutzlich, um die Daten zu generieren. Er generiert random Daten aus vielen Bereichen.
z. B.

Faker faker = new Faker();
for (int i = 0; i <= 20; i++) {
	String firstName = faker.name().firstName();
	String lastName = faker.name().lastName();
	String email = String.format("%s.%s@albertoscode.pl", lastName, firstName);
	Student student = new Student(
	  firstName,
	  lastName,
	  email,
	  faker.number().numberBetween(17, 55)
	);
}

### Sort
https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.sorting

Sort sort = Sort.by("age").ascending().and(Sort.by("firstName"));
repository.findAll(sort);

### Paging and Sorting
PageRequest pageRequest = PageRequest.of(
	0, <- page Nummer
	5, <- Anzahl von Rekorden auf einem  Page
	Sort.by("firstName").ascending() <- Wie die Daten sorten werden sollen.
);
Page<Student> page = repository.findAll(pageRequest);

Paging lasst man die Output zu teilen. Falls wir zu viel Rekorden haben, würden wir ehre nicht alles

## One to One Relationships

### @OneToOne and @JoinColumn
Um zwei Spalte zu verbinden, brauchen wir die zwei Anotation @OneToOne and @JoinColumn. 

@JoinColumn - zeigt welche Spalte man verbinden will
@OneToOne - zeigt wie man zwei Spalten verbinden will

@OneToOne(cascade = CascadeType.ALL)
@JoinColumn(
name = "student_id",
referencedColumnName = "id"
)
private Student student;

### Cascade Type

cascade = CascadeType.

DETACH - 

### Fetch Type
@OneToOne(
	cascade = CascadeType.ALL,
    fetch = FetchType.EAGER
)

FetchType.
EAGER - Zeigt ganzes Rekord und auch joined Rekord

### Uni Vs BiDirectional on 1 to 1 relationship

@OneToOne(mappedBy = "student")
private StudentIdCard studentIdCard;

### Orphan Removal
@OneToOne(mappedBy = "student", orphanRemoval = true)

### @ForeingKey
Wir wollen nicht züffelige Nummer als der Name der FOREIGN KEY Constraint haben. Deswegen mussen wir @ForeingKey benutzen und dort einen Name eingeben. 

@JoinColumn(
    name = "student_id",
    referencedColumnName = "id",
    foreignKey = @ForeignKey(
            name = "student_id_fk"
    )
)

## Many to Many

### @JoinTable
@JoinTable generiert eine Verbindungstabele automatisch

@ManyToMany(
        cascade = {CascadeType.PERSIST, CascadeType.REMOVE}
)
@JoinTable(
        name = "enrolment",
        joinColumns = @JoinColumn(
                name = "student_id",
                foreignKey = @ForeignKey(name = "enrolment_student_id_fk")
        ),
        inverseJoinColumns = @JoinColumn(
                name = "course_id",
                foreignKey = @ForeignKey(name = "enrolment_course_id_fk")
        )
)
private List<Course> courses = new ArrayList<>();



## Transactions

https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#transactions