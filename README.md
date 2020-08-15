# The common dev principles

## SOLID
- [S] Single-responsiblity principle

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

- [O] Open-closed principle

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

- [L] Liskov substitution principle

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

- [I] Interface segregation principle

<details>
<summary><b>BAD</b></summary>
<p>

```csharp
```

</p>
</details>
<details>
<summary><b>GOOD</b></summary>
<p>

```csharp
```

</p>
</details>

- [D] Dependency Inversion Principle

<details>
<summary><b>BAD</b></summary>
<p>

```csharp
```

</p>
</details>
<details>
<summary><b>GOOD</b></summary>
<p>

```csharp
```

</p>
</details>

## DRY - Don't Repeat Yourself

## KISS - Keep It Simple, Stupid

## YAGNI - You Aren't Gonna Need It 

## SLAP - Single Level of Abstraction Principle

## GRASP - General Responsibility Assignment Software Patterns

## BDUF – Big Design Up Front

## SOC – Separation of Concerns

## TDA - Tell don’t ask

## WET - We enjoy typing

## Accountability without authority

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




## Links: 
https://www.idginsiderpro.com/article/3233866/12-essential-software-development-principles-and-concepts.html
https://dev.to/luminousmen/what-are-the-best-software-engineering-principles--3p8n
https://medium.com/webbdev/solid-4ffc018077da
