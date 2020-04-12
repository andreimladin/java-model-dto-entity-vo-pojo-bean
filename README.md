# Model-related terminologies: Model vs DTO vs Entity vs Value Object vs Pojo vs Bean

The goal of this repository is to make clear the meaning of a few terminologies that created a lot of confusion in the development communitity. 
I would like to mention that this clarification will be made from a Java developer's perspective.

## Model

## DTO
The pattern which is known today as Data Transfer Object was mistakenly (see this definition) called Value Object in the first version of the Core J2EE Patterns. The name was corrected in the second edition of the Core J2EE Patterns book, but the name "Value Object" became very popular and is still used as an alias for the actual DTOs.

* A Data Transfer Object (DTO) is just as stupid data container which is used to transport data between layers and tiers.
DTOs are often java.io.Serializable (*only needed if you are going to transfer the data across JVMs.)

## Entity

## Value Object

A Value Object represents itself a fix set of data and is similar to a Java enum. A Value Object doesn't have any identity, it is entirely identified by its value and is immutable. A real world example would be Money(10.00, Currency.GBP), Color.RED, Color.BLUE, SEX.FEMALE 

## Pojo

Pojo stands for Plain Old Java Object. 
A normal Java object, not bound by any restriction other than those forced by the Java Language Specification. It's not tied to any framework. They were introduced in EJB 3.0 by Sun Microsystems.

Properties of a POJO:
* All instance variables should be private
* All access-methods should be public
* Should not have any behaviour
* Should not extend any class or implement an interface
* Should not use any annotation (@Entity)

## Bean

# Bibliography
* https://data-flair.training/blogs/pojo-class-in-java/
* http://www.adam-bien.com/roller/abien/entry/value_object_vs_data_transfer
