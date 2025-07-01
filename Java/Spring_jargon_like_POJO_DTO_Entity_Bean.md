Java/Spring jargon like POJO, DTO, Entity, Bean, Repository?
Let’s understand these terms:

# 1. POJO (Plain Old Java Object)
- Just a regular Java class
- No annotations, no frameworks
- Only fields, constructors, and getters/setters
- Think of it as the most basic data structure

# 2. Bean
- A POJO that Spring manages
- Must follow JavaBean rules (like having a no-arg constructor)
- Registered in Spring via annotations like @ Component, @ Service, or @ Repository
- All Beans are POJOs but Spring is in charge of creating and injecting them.

# 3. DTO (Data Transfer Object)
- A POJO specifically used to carry data between layers
- Contains only data - no logic, no annotations required
- Commonly used between Controller and Service layers
- Every DTO is a POJO, but not every POJO is a DTO.

# 4. Entity
- A POJO that represents a database row
- Annotated with @ Entity and used with JPA/Hibernate
- Maps class fields to database table columns

# 5. DAO (Data Access Object)
- A class that manually handles database operations
- Typically uses JDBC or Hibernate to write queries

# 6. Repository
- Spring's modern replacement for DAO
- Uses @ Repository and Spring Data JPA
- No need to write queries , Spring can auto-generate them
- Cleaner, more maintainable way to access data

# 7. Service
- Contains the business logic of your application
- Where decisions, calculations, and rules are applied
- Annotated with @ Service

# 8. Controller
- Handles HTTP requests and responses
- Acts as the entry point for web APIs
- Annotated with @ Controller or @ RestController

# 9. Component
- The base annotation for any Spring-managed class
- @Service, @Repository, and others are specialized versions of it
- Used to register general-purpose Spring beans

# 10. Configuration
A class that defines how beans are wired together
Annotated with @ Configuration
Often contains methods that create beans for the Spring context
