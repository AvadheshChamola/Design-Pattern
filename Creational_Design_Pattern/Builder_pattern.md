# Builder Design Pattern
- design to construct a complex object step by step.
- Why?
    - Too Many arguments to pass from client program to the Factory class that can be error prone as the type of arguments are same and from client side its hard to maintain the order of the argument.
    - Some of the parameters might be optional but in Factory pattern, we are forced to send all the parameters and optional parameters need to send as NULL.
    - If the object is heavy and its creation is complex, then all that complexity will be part of Factory classes that is confusing.

## Code

### Builder Class
- create a static nested class and then copy all the arguments from the outer class to the Builder class.
- Java Builder class should have a public constructor with all the required attributes as parameters.
- Java Builder class should have methods to set the optional parameters and it should return the same Builder object after setting the optional attribute.
- The final step is to provide a build() method in the builder class that will return the Object needed by client program. For this we need to have a private constructor in the Class with Builder class as argument.
```java
public class Computer {
	
	//required parameters
	private String HDD;
	private String RAM;
	
	//optional parameters
	private boolean isGraphicsCardEnabled;
	private boolean isBluetoothEnabled;
	

	public String getHDD() {
		return HDD;
	}

	public String getRAM() {
		return RAM;
	}

	public boolean isGraphicsCardEnabled() {
		return isGraphicsCardEnabled;
	}

	public boolean isBluetoothEnabled() {
		return isBluetoothEnabled;
	}
	
	private Computer(ComputerBuilder builder) {
		this.HDD=builder.HDD;
		this.RAM=builder.RAM;
		this.isGraphicsCardEnabled=builder.isGraphicsCardEnabled;
		this.isBluetoothEnabled=builder.isBluetoothEnabled;
	}
	
	//Builder Class
	public static class ComputerBuilder{

		// required parameters
		private String HDD;
		private String RAM;

		// optional parameters
		private boolean isGraphicsCardEnabled;
		private boolean isBluetoothEnabled;
		
		public ComputerBuilder(String hdd, String ram){
			this.HDD=hdd;
			this.RAM=ram;
		}

		public ComputerBuilder setGraphicsCardEnabled(boolean isGraphicsCardEnabled) {
			this.isGraphicsCardEnabled = isGraphicsCardEnabled;
			return this;
		}

		public ComputerBuilder setBluetoothEnabled(boolean isBluetoothEnabled) {
			this.isBluetoothEnabled = isBluetoothEnabled;
			return this;
		}
		
		public Computer build(){
			return new Computer(this);
		}

	}

}
```
## Client Class
```java
public class BuilderPattern {
	public static void main(String[] args) {
		//Using builder to get the object in a single line of code and 
        //without any inconsistent state or arguments management issues		
		Computer comp = new Computer.ComputerBuilder("500 GB", "2 GB")
                .setBluetoothEnabled(true)
				.setGraphicsCardEnabled(true)
                .build();
	}
}
```
## When to use Builder Design Pattern
- Complex Object Construction
- Step-by-Step Construction
- Avoiding constructors with multiple parameters
- Immutable Objects
- Configurable Object Creation / Readable code
- Common Interface for Multiple Representations

## When not to use Builder Design Pattern
- Simple Object Construction
- Performance Concerns
- Immutable Objects with Final Fields
- Increased Code Complexity
- Tight Coupling with Product