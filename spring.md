# Section 2

## Spring Initializer

### Initializr
https://start.spring.io/
https://github.com/spring-io/initializr


https://github.com/spring-projects/spring-boot/tree/main/spring-boot-project/spring-boot-starters

## Github Workflow
Add branches from different repo
git remote add <alias> https://github.com/springframeworkguru/spring5webapp


## JPA Entities
POJO - Plain old Java object

## H2 databes console

spring.h2.console.enabled=true <- enable database console in a browser
spring.datasource.url=jdbc:h2:mem:mydb <- set url to database

output.ansi.enabled: ALWAYS <- turn on spring colors in console

## Spring mvc

MVC is a common design pattern for GUI and Web Applications.
M = Model
V = View
C = Controller

## Thymeleaf
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Spring Framework Guru</title>
</head>
<body>
<h1>Book List</h1>
<table>
    <tr th:each="book : ${books}">
        <td th:text="${book.id}"></td>
        <td th:text="${book.title}"></td>
        <td th:text="${book.publisher.name}"></td>
    </tr>
</table>
</body>
</html>

# Section 3 - Dependency Injection

## The Spring Context
ApplicationContext - primary job of the ApplicationContext is to manage beans

Wenn wir die App ausführen mit SpringApplication, wird ApplicationContext Objekt zurückgegeben.
ApplicationContext ctx = SpringApplication.run(SpringDiApplication.class, args)

## Dependency Injection (DI)
- is the concept in which objects get other required objects from outside
- es gibt 3 Arte von DI:
	- property injected (die Schlechteste) - der Benutzer ordnet die Implementation zu eine Property zu
		@Autowired
		public GreetingService greetingService;
	    public String getGreeting() {
	        return greetingService.sayGreeting();
	    }

    - setter injected - der Benutzer ordnet die Implementation mit einem Setter zu
    	private GreetingService greetingService;
    	@Autwired
	    public void setGreetingService(GreetingService greetingService) {
	        this.greetingService = greetingService;
	    }
	    public String getGreeting() {
	        return greetingService.sayGreeting();
	    }

    - constructor injected (die Beste) - der Benutzer ordnet die Implementation am Anfang mit Construcotr zu
    	private final GreetingService greetingService;
    	@Autowired <- **hier ist die Annt Optional, weil es keine andere Weg gibt, um die Dependency zu injekten.**
	    public ConstructorInjectedController(GreetingService greetingService) {
	        this.greetingService = greetingService;
	    }
	    public String getGreeting() {
	        return greetingService.sayGreeting();
	    }



## IoC (Inversion of Controll)
- is the runtime environment (or framework) which injects dependencies,
- is in control of the injection of dependencies

## Profiles
Mann darf viel Services mit gleichem Namen aber z. B. mit anderen Sprachen haben. Dann um korrekt/aktiv Service zu erkennen, brauchen wir ein Hinweis im application.properties.

ein englishes Service
@Service("I18nService")
@Profile("EN")

ein spanisches Service
@Service("I18nService")
@Profile("ES")


spring.profiles.active=ES

Man kann auch mehr als ein aktive Profile haben
spring.profiles.active=**ES, dog**

## Default Service
@Service("I18nService")
**@Profile({"ES", "default"})** <- das Profil ist ES und default

## Multi-Module Maven Builds
Wenn das Module nicht Ausfuhrbar ist, mussen wir da Property setzen, damit spring kein main Class sucht.
<properties>
    <spring-boot.repackage.skip>true</spring-boot.repackage.skip>
</properties>

**./mvnw** <- This allows you to run the Maven project without having Maven installed and present on the path. It downloads the correct Maven version if it's not found (as far as I know by default in your user home directory).

Wir stellen das <build> tag nur in dem Module, wo main sich befindet.
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>

mvn spring-boot:run -pl <module_with_main_method>


## Implement Base Entity
Es ist empfohlen, um die boxed Typen zu benutzen, weil sie null gleichen dürfen.


# Section 3
## Adding maven dependencies
Leere Ordner werden nicht bei Git gemarkt.

## Custom Banner
<!--
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
-->

Um die Banner zu wechseln, erstellen wir eine Datei in der Ordner resources mit dem Name banner.txt.

https://devops.datenkollektiv.de/banner.txt/index.html <- Banner Generator

Man kann auch ein jpg zu ASCII convertieren. Man muss einen Eintrag in application.properties einfügen
spring.banner.image.location=image.jpg

# Section 5

## Component Scan
Spring Framework sucht die Beans in der Package, wo die @SpringBootApplication ist und daruntern. Also wenn der Package guru.springframweork.sfgd benannt ist, Beans in guru.albert werden nicht gefunden.

@ComponentScan(basePackages = {"guru.springframework.sfgdi", "com.springframework.pets"}) - Mach Spring auch in anderen Paketen zu suchen


## Java Configuration example
Statt @Service oder @Controller benutzen, um einen Bean zu erstellen, können wir die Beans manuell in einer @Configuration class erstellen.

<!--
@Configuration
public class GreetingServiceConfig {

    @Bean
    ConstructorGreetingService constructorGreetingService() {
        return new ConstructorGreetingService();
    }

    @Bean
    PropertyInjectedGreetingService propertyInjectedGreetingService() {
        return new PropertyInjectedGreetingService();
    }
}
-->

## Primary Beans and profiles
In @Configuration module, stellt man mit @Bean auch @Primary.

<!-- 
@Bean("i18nService")
@Profile({"ES", "default"})
 -->

## DI in Java Configuration
Man kann auch Beans in Configuration erstellen, die später zu einem anderen Bean bentuzt werden.
<!-- 
@Bean
EnglishGreetingRepository englishGreetingRepository() {
    return new EnglishGreetingRepositoryImpl();
}

@Bean("i18nService")
@Profile("EN")
I18nEnglishGreetingService i18nEnglishGreetingService(EnglishGreetingRepository englishGreetingRepository) {
    return new I18nEnglishGreetingService(englishGreetingRepository);
}
 -->

## Using factory beans
Ein Beispiel mit factory class
<!-- 
public class PetServiceFactory {

    public PetService getPetService(String petType) {
        switch (petType) {
            case "dog":
                return new DogPetService();
            case "cat":
                return new CatPetService();
            default:
                return new DogPetService();
        }
    }
}
 -->

## xml configuration
<!-- 
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean name="constructorGreetingService" class="guru.springframework.sfgdi.services.ConstructorGreetingService"/>
</beans>
 -->
@ImportResource("classpath:sfgdi-config.xml")

## Spring Bean Scope
Wir können nur ein Bean von einem Art erstellen oder für jede Nutzung, eine neue neue Bean erstellen. Es ist gut in der Präzentation erklärt.

Prototype Scope
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)

Singleton Scope Beans werden am Anfang erstellt, Prototpe Beans, wenn wir Sie benutzen.



# Pre Course 
## annotations

@Autowired - To wire the application parts together, use the @Autowired on the fields, constructors, or methods in a component. Spring's dependency injection mechanism wires appropriate beans into the class members marked with @Autowired.

@Transient - make a field not being saved to database

@Transactional - allows to make changes in objects found by id

@Component - Another way to declare a bean is to mark a class with a @Component annotation. Doing this turns the class into a Spring bean at the auto-scan time.

@Bean - A method-level annotation to specify a returned bean to be managed by Spring context. The returned bean has the same name as the factory method.

@Bean
String getBeanek() {
	return "Siema, jestem beanek";
}
ApplicationContext ctx = SpringApplication.run(JpaApplication.class, args);
String beanek = (String) ctx.getBean("getBeanek"); <- es gibt genau die gleiche Sache wie return von @Bean Fuktion aus.

Wahl die 
@Qualifier - indicates which bean should be injected 
@Autowired
@Qualifier("constructorGreetingService")

@Primary - used to decide which bean to inject when ambiguity is present regarding dependency injection

