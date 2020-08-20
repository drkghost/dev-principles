## GRASP - General Responsibility Assignment Software Patterns

group of patterns for assigning responsibility to classes and objects in object-oriented design

object oriented design with responsibilities. 



### Information Expert

you should assign a responsibility to the class which has the information necessary to fulfill that responsibility.

<details>
<summary><b>Example</b></summary>
<p>		

```csharp 
public class Customer
{
  private readonly List<Order> _orders = new List<Order>();
 
  public decimal GetTotalAmount(Guid orderId)
  {
    return this._orders.Sum(x => x.Amount);
  }
}
```

</p>
</details>

### Creator

Assign class B the responsibility to create an instance of class A if one of these is true (the more the better):
- B “contains” or compositely aggregates A.
- B records A.
- B closely uses A.
- B has the initializing data for A that will be passed to A when it is created. Thus B is an Expert with respect to creating A.

<details>
<summary><b>Example</b></summary>
<p>		

```csharp 
public class Customer
{
  private readonly List<Order> _orders = new List<Order>();

  public void AddOrder(List<OrderProduct> orderProducts)
  {
    var order = new Order(orderProducts);  // creator
    _orders.Add(order);
  }
}
```

</p>
</details>

### Controller

Assign the responsibility to a class representing one of the following choices:

- Represents the overall “system”, a “root object”, a device that the software is running within, or a major subsystem — these are all variations of a facade controller.
- Represents a use case scenario within which the system operation occurs, often named <UseCaseName>[Handler|Coordinator|Session] (use case or session controller).

A UI enables users to perform system operations. A Controller is the first object after the UI layer that handles the system operations requests, and then delegates the responsibility to the underlying domain objects.

### Low Coupling

Coupling is a measure of how strongly one element is connected to, has knowledge of, or relies on other elements. Low coupling is an evaluative pattern that dictates how to assign responsibilities for the following benefits:

- lower dependency between the classes,
- change in one class having a lower impact on other classes,
- higher reuse potential.

### High Cohesion

keep objects appropriately focused, manageable and understandable

the responsibilities of a given element are strongly related and highly focused (SRP)

### Pure Fabrication

problem: the domain model for a banking system contains classes like Account, Branch, Cash, Check, Transaction, etc. Need to store information about the customers

solution: to introduce another class which does not represent any domain concept, “PersistenceProvider.”

### Indirection

Problem: Where to assign responsibility, to avoid direct coupling between two (or more) things? How to de-couple objects so that low coupling is supported and reuse potential remains higher?

Solution: Assign the responsibility to an intermediate object to mediate between other components or services so that they are not directly coupled. 

### Polymorphism

restricts the use of run-time type identification (RTTI)

### Protected Variations

How to design objects, subsystems, and systems so that the variations or instability in these elements does not have an undesirable impact on other elements?

Identify points of predicted variation or instability; assign responsibilities to create a stable interface around them.

protects elements from the variations on other elements (objects, systems, subsystems) by wrapping the focus of instability with an interface and using polymorphism to create various implementations of this interface





## Links

https://en.wikipedia.org/wiki/GRASP_(object-oriented_design)

https://dzone.com/articles/solid-grasp-and-other-basic-principles-of-object-o

https://bool.dev/blog/detail/grasp-printsipy

https://medium.com/@k.d.kwiecinski/grasp-design-principles-de98cae2196c

