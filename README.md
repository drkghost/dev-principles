# The common dev principles

## SOLID
#### [S] Single-responsibility principle

every module or class should have responsibility for a single part of the functionality provided by the software and that responsibility should be entirely encapsulated by the class;

<details>
<summary><b>BAD</b></summary>
<p>		

```csharp 
public class Animal
{
  public Animal() { }
  public string GetAnimalName() { }
  public SaveAnimal(Animal a) {}
}
```

</p>
</details>
<details>
<summary><b>GOOD</b></summary>
<p>
	
```csharp 
public class Animal
{
  public Animal() { }
  public string GetAnimalName() { }
}
public class AnimalRepository
{
  public Animal GetAnimal(string name) { }
  public Animal SaveAnimal(Animal a) { }
}
```

</p>
</details>

#### [O] Open-closed principle

software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification

<details>
<summary><b>BAD</b></summary>
<p>

```csharp 
public class Animal
{
  public Animal(string name) { }
  public string GetAnimalName() { }
}
var animals = new List<Animal>() 
{
  new Animal("lion"),
  new Animal("mouse")
}
public string AnimalSound(List<Animal> animals)
{
  foreach(var a in animals)		
  {
    if(a.GetAnimalName() == "lion")
      return "roar";
    if (a.GetAnimalName() == "mouse")
      return "squeak";
  }
}
```

</p>
</details>
<details>
<summary><b>GOOD</b></summary>
<p>

```csharp 
public class Animal
{
  public Animal(string name) { }
  public string GetAnimalName() { }
  public virtual string MakeSound() {}
}
public class Lion : Animal
{
  public new string MakeSound() => "roar";
}
public class Squirrel : Animal
{
  public new string MakeSound() => "squeak";
}
public class Snake : Animal
{
  public new string MakeSound() => "hiss";
}
public string AnimalSound(List<Animal> animals)
{
  foreach (var a in animals)
  {
    a.MakeSound();
  }
}
```

</p>
</details>

#### [L] Liskov substitution principle

the inherited class should complement, not replace, the behavior of the base class;

in general, should be possible to replace parent class with child class without affecting of program execution

<details>
<summary><b>BAD</b></summary>
<p>

```csharp
public abstract class Employee
{
  public virtual string GetWorkDetails(int id) => "Base Work"
  public virtual string GetEmployeeDetails(int id) => "Base Employee";        
}
public class SeniorEmployee : Employee
{
  public override string GetWorkDetails(int id) => "Senior Work";
  public override string GetEmployeeDetails(int id) => "Senior Employee";
}
public class JuniorEmployee : Employee
{
  public override string GetWorkDetails(int id)
  {
    throw new NotImplementedException();        
  }
  public override string GetEmployeeDetails(int id) => "Junior Employee";
}
...
List<Employee> list = new List<Employee>();
list.Add(new JuniorEmployee());
list.Add(new SeniorEmployee());
foreach (Employee emp in list)
{
  emp.GetWorkDetails(985);
}
```

</p>
</details>
<details>
<summary><b>GOOD</b></summary>
<p>

```csharp
public interface IEmployee
{
  string GetEmployeeDetails(int employeeId);
}
public interface IWork
{
  string GetWorkDetails(int employeeId);
}
public class SeniorEmployee : IWork, IEmployee
{
  public string GetWorkDetails(int employeeId) => "Senior Work";
  public string GetEmployeeDetails(int employeeId) => "Senior Employee";
}
public class JuniorEmployee : IEmployee
{
  public string GetEmployeeDetails(int employeeId) => "Junior Employee";	
}
```

</p>
</details>

#### [I] Interface segregation principle

no client should be forced to depend on methods it does not use

<details>
<summary><b>BAD</b></summary>
<p>

```csharp
interface IMessage
{
  void Send();
  string Text { get; set;}
  string Subject { get; set;}
  string ToAddress { get; set; }
  string FromAddress { get; set; }
}
class EmailMessage : IMessage
{
  public string Subject { get; set; }
  public string Text { get; set; }
  public string FromAddress { get; set; }
  public string ToAddress { get; set; }
 
  public void Send()
  {
    Console.WriteLine("Send email message: {0}", Text);
  }
}
class SmsMessage : IMessage
{
  public string Text { get; set; }
  public string FromAddress { get; set; }
  public string ToAddress { get; set; }
        
  public string Subject
  {
    get
    {
      throw new NotImplementedException();
    } 
    set
    {
      throw new NotImplementedException();
    }
  }
 
  public void Send()
  {
    Console.WriteLine("Send sms message: {0}", Text);
  }
}
```

</p>
</details>
<details>
<summary><b>GOOD</b></summary>
<p>

```csharp
interface IMessage
{
  void Send();
  string ToAddress { get; set; }
  string FromAddress { get; set; }
}
interface ITextMessage : IMessage
{
  string Text { get; set; }
}
interface IEmailMessage : ITextMessage
{
  string Subject { get; set; }
}
class EmailMessage : IEmailMessage
{
  public string Text { get; set; }
  public string Subject { get; set; }
  public string FromAddress { get; set; }
  public string ToAddress { get; set; }

  public void Send()
  {
    Console.WriteLine("Send email message: {0}", Text);
  }
}
class SmsMessage : ITextMessage
{
  public string Text { get; set; }
  public string FromAddress { get; set; }
  public string ToAddress { get; set; }
  public void Send()
  {
    Console.WriteLine("Send sms message: {0}", Text);
  }
}
```

</p>
</details>

#### [D] Dependency Inversion Principle

programmer should work at the interface level and not at the implementation level

High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g. interfaces)

Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions

<details>
<summary><b>BAD</b></summary>
<p>

```csharp
class Book
{
  public string Text { get; set; }
  public ConsolePrinter Printer { get; set; } 
  public void Print()
  {
    Printer.Print(Text);
  }
} 
class ConsolePrinter
{
  public void Print(string text)
  {
    Console.WriteLine(text);
  }
}
```

</p>
</details>
<details>
<summary><b>GOOD</b></summary>
<p>

```csharp
interface IPrinter
{
  void Print(string text);
} 
class Book
{
  public string Text { get; set; }
  public IPrinter Printer { get; set; } 
  public Book(IPrinter printer)
  {
    this.Printer = printer;
  } 
  public void Print()
  {
    Printer.Print(Text);
  }
} 
class ConsolePrinter : IPrinter
{
  public void Print(string text)
  {
    Console.WriteLine("Print to console");
  }
} 
class HtmlPrinter : IPrinter
{
  public void Print(string text)
  {
    Console.WriteLine("Print to html");
  }
}
```

</p>
</details>

## DRY - Don't Repeat Yourself

aimed at reducing repetition of software patterns, replacing it with abstractions or using data normalization to avoid redundancy

Every piece of knowledge must have a single, unambiguous, authoritative representation within a system

if you find that you're cutting and pasting a block of code into multiple places, your design is flawed and you should fix that first.

## KISS - Keep It Simple, Stupid

most systems work best if they are kept simple rather than made complicated; therefore, simplicity should be a key goal in design, and unnecessary complexity should be avoided

## YAGNI - You Aren't Gonna Need It 

a programmer should not add functionality until deemed necessary

Always implement things when you actually need them, never when you just foresee that you need them.

## CQS, CQRS - Command Query Responsibility Segregation 

separates read and update operations for a data store

TBA

## SLAP - Single Level of Abstraction Principle

you should organize your code (functions to be specific) to keep it maintainable

Long and complex functions are hard to live with. They're difficult to understand for others, are hard to test and often require scrolling to see all of their content

Functions should do just one thing, and they should do it well. Robert Martin

Example: a function that reads the user input, shouldn't also process it

## BDUF – Big Design Up Front

the program's design is to be completed and perfected before that program's implementation is started

often associated with the waterfall model of software development

## SOC – Separation of Concerns

don’t write your program as one solid block, instead, break up the code into chunks that are finalized tiny pieces of the system each able to complete a simple distinct job

## TDA - Tell don’t ask

we should not ask object about their state, make decision and only then tell them what to do. Rather we should send commands

## WET - We enjoy typing

anti-pattern, against to DRY. "write every time", "write everything twice", "we enjoy typing" or "waste everyone's time"

## MVP - Minimum viable product

a version of a product with just enough features to satisfy early customers and provide feedback for future product development.

## POC - proof-of-concept

a realization of a certain method or idea in order to demonstrate its feasibility

## An inch wide and a mile deep

The more a product or company tries to do, the less it does really well and the greater cost and complexity it assumes in doing it

## Conway's Law

Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure.

you can't change the fundamental structure of your software without changing the fundamental structure of your team (which is often more difficult).

## Fail fast

don't handle all errors, your software should crash boldly and horribly if an error occurs.

better to crash application than allow it continue to work in case of critical exception has been thrown

## TIMTOWTDI - There's more than one way to do it

a Perl programming motto

In contrast, part of the Zen of Python is, "There should be one — and preferably only one — obvious way to do it."

## Links: 

https://www.idginsiderpro.com/article/3233866/12-essential-software-development-principles-and-concepts.html

https://dev.to/luminousmen/what-are-the-best-software-engineering-principles--3p8n

https://medium.com/webbdev/solid-4ffc018077da

https://metanit.com/

https://bool.dev/blog/detail/grasp-printsipy#expert

https://nalexn.github.io/separation-of-concerns/

http://rubyblog.pro/2016/09/tell-dont-ask-principle
