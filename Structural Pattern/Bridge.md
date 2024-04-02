# Bridge Structural Pattern
Bridge is a structural design pattern that lets you split a large class or a set of closely related classes into two separate hierarchies — abstraction and implementation—which can be developed independently of each other.

# Design Mechanism
This is a design mechanism that encapsulates an implementation class inside of an interface class.  
- The bridge pattern allows the Abstraction and the Implementation to be developed independently and the client code can access only the Abstraction part without being concerned about the Implementation part.
- The abstraction is an interface or abstract class and the implementer is also an interface or abstract class.
- The abstraction contains a reference to the implementer. Children of the abstraction are referred to as refined abstractions, and children of the implementer are concrete implementers. Since we can change the reference to the implementer in the abstraction, we are able to change the abstraction’s implementer at run-time. Changes to the implementer do not affect client code.
- It increases the loose coupling between class abstraction and it’s implementation.

![image](https://github.com/AvadheshChamola/Design-Pattern/assets/43910109/c7497ce2-a8e6-4104-91bf-52595be17d90)

## Ex without Bridge Design Pattern
![image](https://github.com/AvadheshChamola/Design-Pattern/assets/43910109/a52d8a65-ede0-46d2-a9fe-d493dcdc93bd)

But the above solution has a problem. If you want to change the Bus class, then you may end up changing ProduceBus and AssembleBus as well and if the change is workshop specific then you may need to change the Bike class as well.

## Ex. with Bridge Design Pattern
![image](https://github.com/AvadheshChamola/Design-Pattern/assets/43910109/045a9b67-bc89-46fd-a82d-0b8920f02122)

# Code
```java
// Java code to demonstrate
// bridge design pattern

// abstraction in bridge pattern
abstract class Vehicle {
	protected Workshop workShop1;
	protected Workshop workShop2;

	protected Vehicle(Workshop workShop1, Workshop workShop2)
	{
		this.workShop1 = workShop1;
		this.workShop2 = workShop2;
	}

	abstract public void manufacture();
}

// Refine abstraction 1 in bridge pattern
class Car extends Vehicle {
	public Car(Workshop workShop1, Workshop workShop2)
	{
		super(workShop1, workShop2);
	}

	@Override
	public void manufacture()
	{
		System.out.print("Car ");
		workShop1.work();
		workShop2.work();
	}
}

// Refine abstraction 2 in bridge pattern
class Bike extends Vehicle {
	public Bike(Workshop workShop1, Workshop workShop2)
	{
		super(workShop1, workShop2);
	}

	@Override
	public void manufacture()
	{
		System.out.print("Bike ");
		workShop1.work();
		workShop2.work();
	}
}

// Implementer for bridge pattern
interface Workshop
{
	abstract public void work();
}

// Concrete implementation 1 for bridge pattern
class Produce implements Workshop {
	@Override
	public void work()
	{
		System.out.print("Produced");
	}
}

// Concrete implementation 2 for bridge pattern
class Assemble implements Workshop {
	@Override
	public void work()
	{
		System.out.print(" And");
		System.out.println(" Assembled.");
	}
}

// Demonstration of bridge design pattern
class BridgePattern {
	public static void main(String[] args)
	{
		Vehicle vehicle1 = new Car(new Produce(), new Assemble());
		vehicle1.manufacture();
		Vehicle vehicle2 = new Bike(new Produce(), new Assemble());
		vehicle2.manufacture();
	}
}

```
# Pros
-  You can create platform-independent classes and apps.
- The client code works with high-level abstractions. It isn’t exposed to the platform details.
- Open/Closed Principle. You can introduce new abstractions and implementations independently from each other.
- Single Responsibility Principle. You can focus on high-level logic in the abstraction and on platform details in the implementation.

# Cons
- You might make the code more complicated by applying the pattern to a highly cohesive class.
