# Introduction
Welcome to the System Design repository, your go-to resource for in-depth articles and resources on software system design. This repository serves as a centralized hub for sharing knowledge, best practices, and insights into the intricate world of designing scalable, reliable, and maintainable systems. I hope reading this article is useful for you. (**Sanjay**)

- [Introduction](https://github.com/sanjay111999/system_design?tab=readme-ov-file#introduction)
- [SOLID Principles](https://github.com/sanjay111999/system_design?tab=readme-ov-file#solid-principles)

## SOLID Principles
> What are these principles?
>> Set of rules to be followed to design a better software.

To keep our systems to be easily readable, understandable, extensible, easy to debug and easy to test we adhere to few basic principles. The SOLID principles are a set of design principles that help in creating maintainable, scalable, and flexible software systems. SOLID is an acronym for a set of design principles in object-oriented programming. The five principles of SOLID are

### Single Responsibility Principle (SRP):

The Single Responsibility Principle (SRP) states that every class or module in a software system should have only one responsibility, i.e., only one reason to change. This means that a class or module should have a well-defined and narrow purpose, and it should not be responsible for multiple unrelated tasks.

**Example 1:**
Suppose you are building a banking application, and you need to create a class to handle customer transactions. The class could be named TransactionHandler.

A good way to apply SRP to this class would be to give it only one responsibility: handling transactions. Here's an example implementation:
```
 public class TransactionHandler {
     public void handleTransaction(Transaction transaction) {
         // handle the transaction here
} }
```
 }
In this example, the TransactionHandler class has a single responsibility, which is to handle transactions. This means that if you need to modify the transaction handling logic, you only need to change the handleTransaction method, and not any other parts of the class.
However, suppose you also need to send an email confirmation to the customer after a transaction is processed. You could be tempted to add this functionality to the TransactionHandler class, but that would violate SRP. Instead, you should create a separate class to handle email confirmation, like this:
```
 public class EmailSender {
     public void sendEmail(String recipient, String subject, String body) {
         // send the email here
} }
```
Then, you could modify the TransactionHandler class to use the EmailSender class to send the email confirmation:
```
 public class TransactionHandler {
     private EmailSender emailSender;
public TransactionHandler(EmailSender emailSender) {
         this.emailSender = emailSender;
     }
     public void handleTransaction(Transaction transaction) {
         // handle the transaction here
         // send email confirmation to the customer
         emailSender.sendEmail(transaction.getCustomerEmail(), "Transaction
 confirmation", "Your transaction has been processed successfully.");
} }
```
In this updated implementation, the TransactionHandler class still has a single responsibility, which is to handle transactions. The email confirmation logic has been delegated to the EmailSender class, which has its own responsibility for sending emails. This adheres to the Single Responsibility Principle and makes the code easier to understand, maintain, and test.

### Open Close Principle:

The open-Closed Principle is a design principle in object-oriented programming that states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This means that you should be able to add new functionality to a class or module without changing its existing code. To put this in naive terms, for adding a new feature in our system it shouldn't require any changes in existing code blocks.

> Why OCP is important?
>> If we do not follow the OCP principle in our code patterns, it would need us to do end to end regression testing for all the exisitng features for a adding a small new feature upon them.

**Example 1:**
Let's say we have a Shape class with different subclasses such as Circle and Rectangle. Instead of modifying the Shape class every time we want to add a new shape, we can use inheritance and polymorphism to extend the functionality:


```
class Shape:
    def area(self):
        raise NotImplementedError()

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius * self.radius

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height
```
