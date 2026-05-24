# spring boot interview questions
 1- what is spring boot?
 ```text
 spring boot is a framework of java that is build on top of spring framework
 ```

2- why spring boot?
``` text
spring boot is used for rapid application development moore than spring because:
 - no configuration needed
 - embedded server tomcat
 - auto-configuration
 - starter dependencies
 - easy for development
 - no xml configuration
```

2- what is DI (Dependency Injection) ?
```text
it's a spring container that is responsible for creating objects and managing them life cycle and injecting them into components instead of creating them ourself
```
``` java
 Service service = new Service();
 Controller c = new Controller(service);

 // with DI
  @Autowired
  Service service;
  or @ReuiqredAllArgsConstructor 
  or @NoArgConstructor + @Autowired on the constructor
```

3- what is Bean ?
```text
it's an object that is created and managed by spring container
```

4- what is the diff between @RequestMapping vs @GetMapping ?
```text
@RequestMapping is a general annotation that can be used for both HTTP methods and URL mapping
@GetMapping is a specific annotation that is used for GET HTTP method only
```

5- Singleton vs Prototype Bean?
```text
Singleton Bean is the default scope in spring and it's create only one object in the container at the start up of the app
```

```java
 @Scope("prototype")
@Service
class UserService {}
```
A- why spring use singleton scope?
```text
 to save memory
 better performance 
```

B-  why spring use AOP ?
```text
AOP is used for cross-cutting concerns such as logging, security, transaction management, etc. 
```

# # 6- What is Dependency Injection?

Dependency Injection is a design pattern used by Spring where the Spring container creates objects (beans) and injects their dependencies automatically instead of creating them manually using new keyword.
Benefits:
Loose coupling
Better testing
Cleaner architecture

# # 7- Why Constructor Injection is preferred?
Constructor injection is preferred because it makes dependencies mandatory, improves testability, supports immutability using final fields, and helps detect errors at compile time.
Example:
```java
@Service
class UserService {

    private final UserRepository repo;

    public UserService(UserRepository repo) {
        this.repo = repo;
    }
}
```

# #8- @Component vs @Service vs @Repository
All of them create Spring beans and are based on @Component annotation.
Differences:
@Component → generic bean
@Service → business logic layer
@Repository → database layer + exception translation
Example:
```java
@Service
class UserService {}

@Repository
class UserRepository {}
```

# #9- @Component vs @Bean
@Component is used for automatic bean detection using component scanning, while @Bean is used for manual bean creation inside configuration classes.
@Component Example:
```java
@Component
class UserService {}
```
@Bean Example:
```java
@Configuration
class AppConfig {

    @Bean
    public UserService userService() {
        return new UserService();
    }
}
```

# #10- Singleton vs Prototype Bean?
Singleton Bean is the default scope in Spring and Spring creates only one object shared across the application lifecycle.
Prototype Bean:
Prototype scope creates a new object every time the bean is requested or injected.
Example:
```java
@Scope("prototype")
@Service
class UserService {}
```

# #11- Why Spring uses Singleton by default?
Spring uses singleton scope by default to reduce memory usage, improve performance, and avoid creating unnecessary objects repeatedly.

# #12- What does @Transactional do?
@Transactional manages database transactions in Spring.
If all operations succeed → commit.
If an exception happens → rollback.
Example:
```java
@Transactional
public void transferMoney() {
    withdraw();
    deposit();
}
```

# #13- save() vs flush()
save() stores data inside the persistence context (memory),
while flush() synchronizes the persistence context with the database immediately.

# #14- JPA vs Hibernate
JPA is a specification for ORM in Java, while Hibernate is the most common implementation of JPA.

# #15- Lazy vs Eager Loading
Lazy loading loads data only when needed,
while eager loading loads related data immediately.
Default:
ManyToOne → EAGER
OneToMany → LAZY

# #16- 🔥 equals() vs ==
== compares primitive values or object references,
while equals() compares object content or logical equality.

# #17- 🔥 Why override equals() and hashCode() together?
HashMap uses hashCode() to determine the bucket and equals() to identify the correct object inside that bucket.
If two objects are equal, they must return the same hashCode().

# #18- 🔥 Why String is good HashMap key?
String is immutable, so its hashCode never changes after creation, making retrieval from HashMap reliable.
Why StringBuilder is bad?
StringBuilder is mutable, so modifying it may change its hashCode and make the key unreachable in the HashMap.

# #19- String vs string builder vs string buffer
- string builder: mutable -Not thread safe
- string buffer: mutable - thread-safe
- string: immutable - thread safe

# #20 - Monolithic vs Microservices
```text
## Monolithic Architecture

- Structure: Built and deployed as a single unit.
- Codebase: All modules and layers are tightly connected within one codebase.
- Advantages: Simpler to develop and debug for small to medium-sized applications.

## Microservices Architecture

- Structure: Divided into independent services, each handling a specific business capability.
- Deployment: Each service can be deployed and scaled independently.
- Communication: Services interact via REST APIs, messaging systems (like Kafka), or other protocols.
- Advantages: Offers better scalability, fault isolation, and flexibility for large distributed systems.
- Disadvantages: Increases operational complexity.
```

# #21 - what is Api Gateway?
```text
- API Gateway acts as a single entry point for all client requests.
- It routes requests to the appropriate microservice.
- Handles cross-cutting concerns like authentication, rate limiting, logging.
- Decouples clients from internal service architecture.
```
# #22- what is Kafka?
```text
- Kafka is a distributed message broker used for asynchronous communication between microservices.

- Instead of services calling each other directly, services can publish events to Kafka topics, and other services consume those events independently.

```
# #23- what happened if service fails?
```text
if service failed it can  impact other services, to avoid this we use "Circuit Breaker" with library like "resilience4j"
The circuit breaker has 3 states:
1 - CLOSE: if request normal
2 - OPEN: if request failed 
3 - HALF-OPEN: limited requests allowed to check if the service is working or not
```
# #23- what is Circuit Breaker?
```text
- Circuit Breaker is a pattern used in microservices to prevent a cascading failure when one service is down or slow. 

- It acts as a protective shield that stops requests from going to a failing service, preventing the failure from spreading to other services.
```

# #24- what is Service Discovery?
```text
- Service Discovery is a mechanism that allows services to find each other in a microservices architecture. It is used to locate and communicate with services dynamically.


```
# #25- what is reactive programming?
```text
Reactive programming is a programming paradigm that deals with asynchronous data streams and the propagation of change.


```
# #26- what is heap and stack in java?
```text
Stack: Stores method calls, local variables, and execution flow (LIFO).
Heap: Stores objects, arrays, and dynamic memory allocation (used by GC).
```
# #27 - what is thread
```text
Thread is lightweight unit of execution of a java program process 
```
```java
public class MyThread extends Thread
or use Runnable interface
public class MyThread implements Runnable{
    public void run (){
        System.out.println("thread name:"+Thread.currentThread().getName());
    }
}
Thread t = new Thread(new MyThread())
t.start();
```

# # 28- what is race condition?
```text
Race condition is a condition that occurs when two or more threads access and modify a shared . that lead to unexpected results
example: i have var =0 and i increment it by 1 in 2 threads so expected result is 2 but the actual result is 1 because of the race condition 
```

# #29 - how to solve race condition?
```text
we use atomic variable like AtomicInteger which is thread safe 
```

so "incapuslation" is hiding the data from externall access or exposing and there is three types: it's called access modifiers 
public: accessible form anywhre
private: accessible oonly in the same class
protected: accessible in the same class and subclasses
default: accessible in the same class and package
so defualt it's like package level access

"inheritance": it's a way to create a new class subclass from anothe exising class blueprint 

"polymorphism":it's the ability of an object to take many forms

"Abstraction": it's a way to hide the implementation details and show only the essential features 


# Technic questions:

## A -two sum
``` text
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
```
``` java
public int[] twoSum(int[] nums, int target) {

    Map<Integer, Integer> map = new HashMap<>();

    for(int i = 0; i < nums.length; i++) {

        int complement = target - nums[i];

        if(map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }

        map.put(nums[i], i);
    }

    return new int[] {};
}

```

# # B - Sliding Window
```text
Sliding window is used to find the maximum or minimum or longest or shortest subarray or substring and we use two pointers left and right
``` 
# # b- Big-O notation 
```text
Big-o notation is used to measure the time or space complexity of algorithems as input size increase 
it's helps us to evaluate the algo performance and scalability.
```
# # C - Valid Parentheses
```text
Valid parentheses is used to check if the parentheses are balanced
``` 




















---

# 📅 Today Study Plan (Starting 11:00 AM)

## 🕚 11:00 → 12:30
### ☕ Java Core Deep Understanding
- OOP concepts
- Abstract class vs Interface
- Composition vs Inheritance
- Casting
- Marker interface
- Static block

---

## ☕ 12:30 → 1:00
### Break / Lunch

---

## 🕐 1:00 → 2:30
### 🔥 Spring Boot Important Topics
- Bean lifecycle
- ApplicationContext
- Singleton vs Prototype
- @Bean vs @Component
- Request lifecycle

---

## 🕝 2:30 → 3:00
### Break

---

## 🕒 3:00 → 4:30
### 🧠 Coding Patterns Practice
- Two Sum
- Sliding Window
- Valid Parentheses
- Merge Intervals

Focus:
- explain out loud
- complexity
- edge cases

---

## 🕟 4:30 → 5:00
### Break / Walk

---

## 🕔 5:00 → 6:30
### 🔥 Mock Interview Practice
- answer questions loudly
- explain HashMap
- explain Spring flow
- explain transactions
- explain DI

---

## 🕡 6:30 → 7:00
### Dinner / Rest

---

## 🕖 7:00 → 8:30
### 🧠 Microservices Basics
- API Gateway
- Service Discovery
- Circuit Breaker
- Kafka basics

---

## 🕣 8:30 → 9:00
### Break

---

## 🕘 9:00 → 10:30
### 🚀 Final Revision
- Read notes
- Speak answers loudly
- Solve 1 coding problem without help
