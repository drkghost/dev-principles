# The common dev principles

## SOLID
- [S] Single-responsiblity principle

every module or class should have responsibility for a single part of the functionality provided by the software and that responsibility should be entirely encapsulated by the class;

**BAD**
```csharp 
public class Animal
{
	public Animal() { }
	public string GetAnimalName() { }
	public SaveAnimal(Animal a) {}
}
```

**GOOD**
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

- [O] Open-closed principle

software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification

**BAD**
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

**GOOD**
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


- [L] Liskov substitution principle
- [I] Interface segregation principle
- D Dependency Inversion Principle

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
