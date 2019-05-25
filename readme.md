# SOLID
*(quick reference - check the cheatheet)*

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

* `Model` - Model represents an object or JAVA POJO carrying data. It can also have logic to update controller if its data changes.
* `View` - View represents the visualization of the data that model contains.
* `Controller` - Controller acts on both model and view. It controls the data flow into model object and updates the view whenever data changes. It keeps view and model separate.