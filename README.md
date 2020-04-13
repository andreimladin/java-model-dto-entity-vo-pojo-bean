# Model-related terminologies: Model vs DTO vs Entity vs Value Object vs Pojo vs Bean

The goal of this repository is to make clear the meaning of a few terminologies that created a lot of confusion in the development communitity. 
I would like to mention that this clarification will be made from a Java developer's perspective.

## Model

## DTO
The pattern which is known today as Data Transfer Object was mistakenly called Value Object in the first version of the Core J2EE Patterns. The name was corrected in the second edition of the Core J2EE Patterns book, but the name "Value Object" became very popular and is still used as an alias for the actual DTOs.

### Properties of a DTO:
* it is used at the highest layer in an application (like into a MVC or a Rest controller)  
* it is just a data container which is used to transport data between layers and tiers.
* they could aggregate more entities or could have partial information from an entity
* DTOs are often java.io.Serializable (*only needed if you are going to transfer the data across JVMs.)

### Sample of a DTO

```java
public class UserCreationDTO {

    @Email
    private String email;

    @NotNull
    @Size(min=8, max=20)
    private String password;

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

## Entity
An entity is a lightweight persistence domain object. Typically, an entity represents a table in a relational database, and each entity instance corresponds to a row in that table.

### Properties of an entity
* The class must be annotated with the javax.persistence.Entity annotation.
* The class must have a public or protected, no-argument constructor. The class may have other constructors.
* The class must not be declared final. No methods or persistent instance variables must be declared final.

### Sample of an entity

```java
@Entity
@Table(name = "user")
public class User {

    @Id
    private UUID id;

    private String email;

    private String password;

    private String firstName;

    private String lastName;

    private Long status;

    public UUID getId() {
        return id;
    }

    public void setId(UUID id) {
        this.id = id;
    }
    
    //  additional getters/setters
    
}
```

## Value Object

A Value Object represents itself a fix set of data and is similar to a Java enum. 
Sample of value object in a real world would be Money, Color.RED, SEX.FEMALE, a 2D coordinate(x, y), a date range [startDate, endDate], a Date(year, month, and day), and so on.

### Properties of a ValueObject
* A Value Object doesn't have any identity
* It is entirely identified by its value and is immutable

### Sample of a ValueObject
```java
public class Money {

    private final double amount;

    private final String currency;

    public Money(double amount, String currency) {
        this.amount = amount;
        this.currency = currency;
    }

    public double getAmount() {
        return amount;
    }

    public String getCurrency() {
        return currency;
    }
}
```

## Pojo

Pojo stands for Plain Old Java Object. 
A normal Java object, not bound by any restriction other than those forced by the Java Language Specification. It's not tied to any framework. They were introduced in EJB 3.0 by Sun Microsystems.

### Properties of a POJO:
* All instance variables should be private
* All access-methods should be public
* Should not have any behaviour
* Should not extend any class or implement an interface
* Should not use any annotation (@Entity)

### Sample of POJO
```java
public class EmployeePojo {
 
    public String firstName;
    public String lastName;
    private LocalDate startDate;
 
    public EmployeePojo(String firstName, String lastName, LocalDate startDate) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.startDate = startDate;
    }
 
    public String name() {
        return this.firstName + " " + this.lastName;
    }
 
    public LocalDate getStart() {
        return this.startDate;
    }
}
```

## JavaBean

A JavaBean is still a POJO, but introduces a strict set of rules around how we implement it

### Properties of a JavaBean:
* Access levels – our properties are private and we expose getters and setters
* Method names – our getters and setters follow the getX and setX convention (in the case of a boolean, isX can be used for a getter)
* Default Constructor – a no-argument constructor must be present so an instance can be created without providing arguments, for example during deserialization
* Serializable – implementing the Serializable interface allows us to store the state

### Sample of JavaBean
```java
public class EmployeeBean implements Serializable {
 
    private static final long serialVersionUID = -3760445487636086034L;
    private String firstName;
    private String lastName;
    private LocalDate startDate;
 
    public EmployeeBean() {
    }
 
    public EmployeeBean(String firstName, String lastName, LocalDate startDate) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.startDate = startDate;
    }
 
    public String getFirstName() {
        return firstName;
    }
 
    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }
 
    //  additional getters/setters
 
}
```

# Bibliography
* https://data-flair.training/blogs/pojo-class-in-java/
* http://www.adam-bien.com/roller/abien/entry/value_object_vs_data_transfer
* https://www.baeldung.com/java-pojo-class
* https://docs.oracle.com/javaee/6/tutorial/doc/bnbqa.html
* https://martinfowler.com/bliki/ValueObject.html
