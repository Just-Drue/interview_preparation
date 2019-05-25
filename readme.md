# SOLID
*(quick reference - check the cheat-sheet)*

The idea is that, by applying those principles together, you are able to write `better quality` code that is `robust`. The system created becomes **easy** to `maintain`, to `reuse` and to `extend` over time. Basically, `SOLID` principles help software developers to achieve `scalability` and avoid that your code breaks every time you face a change:

* **S** – Single-responsibility principle<br/>
*There should be never more than one reason for a class to change*

* **O** – Open-closed principle<br/>
*Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification*

* **L** – Liskov substitution principle<br/>
*Subtypes must be substitutable for their base types*

* **I** – Interface segregation principle<br/>
*Classes that implement interfaces, should not be forced to implement methods they do not use*

* **D** – Dependency Inversion Principle<br/>
*High level modules should not depend on low level modules rather both should depend on abstraction. Abstraction should not depend on details; rather detail should depend on abstraction*

---

# DRY
*Don't repeat yourself*

The `DRY Principle` is actually about removing duplicate ideas and not duplicate code.

---

# Design Patterns

## MVC
*Model-View-Controller*

* `Model` - Model represents an object carrying data. It can also have logic to update controller if its data changes.
* `View` - View represents the visualization of the data that model contains.
* `Controller` - Controller acts on both model and view. It controls the data flow into model object and updates the view whenever data changes. It keeps view and model separate.

The main idea is to be able to remove any of the components, change them and connect to the other two without the other two being impacted negatively. Scales well as well.

A good example is how `web apps` are currently made, for example let's take `React.js` as the `view`, `Django` as the `controller` and `PostgreSQL` as the `model`. Going even deeper the `Django` can have its `seperate controllers` and `models` for multiple complex inner modules.

## Singleton
*Prevents duplication when all you need is one instance at all times*

In object-oriented programming, a `singleton class` is a class that can have only one object (an instance of the class) at a time. After first time, if we try to instantiate the Singleton class, the new variable also points to the first instance created. So whatever modifications we do to any variable inside the class through any instance, it affects the variable of the single instance created and is visible if we access that variable through any variable of that class type defined.

To design a singleton class:

* Make constructor as private.
* Write a static method that has return type object of this singleton class. Here, the concept of Lazy initialization in used to write this static method.

```java
class Singleton 
{ 
    private static Singleton single_instance = null;
    public String s; 
  
    // private constructor restricted to this class itself 
    private Singleton() { 
        s = "Hello I am a string part of Singleton class"; 
    } 
  
    // static method to create instance of Singleton class 
    public static Singleton getInstance() { 
        if (single_instance == null) 
            single_instance = new Singleton(); 
  
        return single_instance; 
    } 
}
  
class Main { 
    public static void main(String args[]) { 
        Singleton x = Singleton.getInstance(); 
        Singleton y = Singleton.getInstance(); 
        Singleton z = Singleton.getInstance(); 
  
        x.s = (x.s).toUpperCase(); 
  
        System.out.println("String from x is " + x.s); 
        System.out.println("String from y is " + y.s); 
        System.out.println("String from z is " + z.s); 
        System.out.println("\n"); 
  
        z.s = (z.s).toLowerCase(); 
  
        System.out.println("String from x is " + x.s); 
        System.out.println("String from y is " + y.s); 
        System.out.println("String from z is " + z.s); 
    } 
}
```

```
Output:

String from x is HELLO I AM A STRING PART OF SINGLETON CLASS
String from y is HELLO I AM A STRING PART OF SINGLETON CLASS
String from z is HELLO I AM A STRING PART OF SINGLETON CLASS

String from x is hello i am a string part of singleton class
String from y is hello i am a string part of singleton class
String from z is hello i am a string part of singleton class
```

## Observer
*Backwards communication is awesome, let the parents listen to the kids*

`Observer` pattern is used when there is one-to-many relationship between objects such as if one object is modified, its depenedent objects are to be notified automatically. It is achieved by calling the `dependant's method` that is responsible for handling the state changes, this is achieved my the main instance storing all observers in a data structure, e.g. a list.


```java
import java.util.ArrayList;
import java.util.List;

public class Subject {
	
   private List<Observer> observers = new ArrayList<Observer>();
   private int state;

   public int getState() {
      return state;
   }

   public void setState(int state) {
      this.state = state;
      notifyAllObservers();
   }

   public void attach(Observer observer){
      observers.add(observer);		
   }

   public void notifyAllObservers(){
      for (Observer observer : observers) {
         observer.update();
      }
   } 	
}
```

```java
public abstract class Observer {
   protected Subject subject;
   public abstract void update();
}
```

```java
public class OctalObserver extends Observer{

   public OctalObserver(Subject subject){
      this.subject = subject;
      this.subject.attach(this);
   }

   @Override
   public void update() {
     System.out.println( "Octal String: " + Integer.toOctalString( subject.getState() ) ); 
   }
}
```

```java
public class BinaryObserver extends Observer{

   public BinaryObserver(Subject subject){
      this.subject = subject;
      this.subject.attach(this);
   }

   @Override
   public void update() {
      System.out.println( "Binary String: " + Integer.toBinaryString( subject.getState() ) ); 
   }
}
```

```java
public class ObserverPatternDemo {
   public static void main(String[] args) {
      Subject subject = new Subject();

      new HexaObserver(subject);
      new OctalObserver(subject);
      new BinaryObserver(subject);

      System.out.println("First state change: 15");	
      subject.setState(15);
      System.out.println("Second state change: 10");	
      subject.setState(10);
   }
}
```

```
Output

First state change: 15
Hex String: F
Octal String: 17
Binary String: 1111
Second state change: 10
Hex String: A
Octal String: 12
Binary String: 1010
```