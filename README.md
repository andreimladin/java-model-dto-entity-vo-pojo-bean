# Model-related terminologies: Model vs DTO vs Entity vs Value Object vs Pojo vs Bean

The goal of this repository is to make clear the meaning of a few terminologies that created a lot of confusion in the development communitity. 
I would like to mention that this clarification will be made from a Java developer's perspective.

## Model

## DTO
The pattern which is known today as Data Transfer Object was mistakenly called Value Object in the first version of the Core J2EE Patterns. The name was corrected in the second edition of the Core J2EE Patterns book, but the name "Value Object" became very popular and is still used as an alias for the actual DTOs.

Properties of a DTO:
* it is used at the highest layer in an application (like into a MVC or a Rest controller)  
* it is just as data container which is used to transport data between layers and tiers.
* they could aggregate more entities or could have partial information from an entity
* DTOs are often java.io.Serializable (*only needed if you are going to transfer the data across JVMs.)

## Entity

### Sample of an entity

```java
@Entity
public class Author {
 
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Column(name = "id", updatable = false, nullable = false)
    private Long id;
 
    @Version
    private int version;
 
    private String firstName;
 
    private String lastName;
     
    @OneToMany(mappedBy = "author")
    private List bookList = new ArrayList();
 
    ...
}
```

## Value Object

A Value Object represents itself a fix set of data and is similar to a Java enum. A Value Object doesn't have any identity, it is entirely identified by its value and is immutable. A real world example would be Money(10.00, Currency.GBP), Color.RED, Color.BLUE, SEX.FEMALE 

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
