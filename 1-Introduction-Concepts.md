
## Data Hiding
Outside person can’t access our internal data directly (or) our internal data should not go out directly. This OOP feature is called data hiding. After validation or authentication outside person can access our internal data. 
Ex: 1) After providing proper username and password, we will be able to access our gmail information. 
2) Even though we are valid customer of a bank we will be able to access our account information and can’t access others account information.

How can we achieve data hiding programmatically?
By declaring data member(variable) as private we can achieve data hiding.
```
public class Account{
	private double balance;
	…..
	…..
	public double getbalance(){
		//validation
		return balance;
	}
}
```

Advantages?
- Achieve security(outside person doesn’t know how it is implemented)

Note: It is highly recommended a data member(variable) as PRIVATE.


## Abstraction
Hiding internal implementation and just highlight the set of services what we are offering.
Ex: Through bank ATM GUI screen bank will highlighting some set of services what they are offering like “Withdrawl”, “Check Deposit” etc.. without highlighting internal implementation like which server it is information and how bank is performing authenticaton etc..

Advantages?
- Security(outside/end person doesn’t know how it is implemented, we are not showing/highlighting our implementation)
- Without affecting outside person, we can perform any type of changes in our internal system hence enhancement and maintenance will become easy.
- Improves easiness to use the system which uses abstraction.

By using interfaces(full abstraction) and abstract(partial abstraction) classes we can implement abstraction.


## Encapsulation
The process of binding data members and methods into a single unit is known as encapsulation.
Ex: class Student {
	//data members
		+
	//methods(behavior)
}

Advantages?
- Security(outside/end person doesn’t know how it is implemented, we are not showing/highlighting our implementation)
- Without affecting outside person, we can perform any type of changes in our internal system hence enhancement and maintenance will become easy.

Disadvantages?
- Increases length of code and slows down execution.


## Tightly encapsulated classes
If each and every variable in a class is declared as private, then we call that class as tightly encapsulated class. We need not check if this class contains corresponding getter and setter methods are not and whether these methods are declared as public or not.


## IS-A relationship(Inheritance)
Inheritance is a property in which one object acquires all the properties and behavior of parent object. “extends” is used to get make use of inheritance feature. 
Advantage?
- Reusability of code with which we can save time and code redundancy can be achieved.

Sample Code:
```
class P {
	public void test1() {
		system.out.println(“in parent class”);
	}
}

class C extends P {
	public void test2() {
		system.out.println(“in child class”);
	}
}

class Test {
	//Case1
	P p = new P();
	p.test1();
	p.test2(); //error - cannot find method test2
	
	//Case2
	C c = new C();
	c.test1();
	c.test2(); 
	
	//Case3
	P p1 = new C();
	p1.test1();
	p1.test2(); //error

	//Case4
	C c1 = new P(); //error - incompatible types found P, required C
}
```
Conclusion of above code:
- Whatever methods parent has by default available for the child, hence on the child reference we can call both parent and child class methods(Case1)
- Whatever methods child has by default not available to the parent and hence on the parent reference we can’t call child specific methods(Case2)
- Parent reference can be used to hold child object but using that reference we can’t call child specific methods(Case3), but we can call the methods present in parent class
- Child reference can’t be used to hold parent object(Case4)

Other Notes:
i) Every class in java is a child class of Object class either directly or indirectly so that Object class methods are by default available to every java class without rewriting. 
ii) If our class doesn’t extend any other class, then only our class is direct child class of Object class like below.
```
Class A {
	//methods + variables
}
```

iii) If our class extends any other class, then our class is indirect class of Object.
```
Class A extends B {
	//variables + methods
}
```
A is a child of B, B is the child of Object. This is called multi-level inheritance. 

iv) Java doesn’t support multiple inheritance like class A extends B, C - will return error. To avoid ambiguity problem, hence java doesn’t support multiple inheritance.
v) Java provides multiple inheritance by using “interface” ex: interface A extends B,C. Since interfaces have only skeleton method body(or method declaration), we will not be facing any ambiguity problem. Strictly speaking, through interface we won’t get any inheritance as we don’t get a code re-use as methods are only declarations not implemented.
vi) Cyclic inheritance is not allowed, ofcourse it is not required as it is useless extending A to A is meaningless, in second example, extending A to B and B to A is also meaningless if you want properties of A and B to be present in both then write a single class instead of two classes.
```
class A extends A {
}

OR
class A extends B {
}
class B extends A {
}
```


## Has-A relationship
i) Has-A relationship is also known as composition or aggregation. 
```
Class Engine {
	//variables + methods
}

Class Car {
	Engine c = new Engine();
}
```

“Car” Has-A “Engine” reference.

ii) There is no specific keyword to implement has-a relation, but most of the times, we depending on “new” keyword.

Advantages?
- Reusability of code, like using Engine methods in Car

Inheritance is an "is-a" relationship. Composition is a "has-a”.

Other Notes:
**Aggregation vs Composition**
1. A "owns" B = Composition(strong association) : B has no meaning or purpose in the system without A
2. A "uses" B = Aggregation(weak association) : B exists independently (conceptually) from A
Composition : Since Engine is-part-of Car, the relationship between them is Composition. Here is how they are implemented between Java classes.
Ex:
```
public class Car {
    //final will make sure engine is initialized
    private final Engine engine;  
       
    public Car(){
       engine  = new Engine();
    }
}

class Engine {
    private String type;
}
```

Aggregation : Since Organization has Person as employees, the relationship between them is Aggregation. Here is how they look like in terms of Java classes
Ex:
```
public class Organization {
    private List<Person> employees;
}

public class Person {
    private String name;   
}
```
   Ex2: A Text Editor owns a Buffer (composition). A Text Editor uses a File (aggregation). When the Text Editor is closed, the Buffer is destroyed but the File itself is not destroyed.
	 A Company is an aggregation of People. A Company is a composition of Accounts. When a Company ceases to do business its Accounts cease to exist but its People continue to exist.

IS-A vs Has-A
If we want totally functionality of a class then we should use IS-A relation. Ex: “Maruti” IS-A “Car” because all the functionalities of car are needed in Maruti.
If we want part of functionality, then we should use Has-A relationship. Ex: “Maruti” Has-A “Engine”
http://www.journaldev.com/1775/multiple-inheritance-in-java


## Method Signature
In java method signature consists of method name followed by argument types. 
Ex: public static int method(int i, float f)
method signature : method(int, float)
Note: Compiler will use this method signature to resolve method calls to check if int, float is passed to above example, if anything else is passed, it will throw compilation error. Method signature can never be same for two methods in java.


## Method overloading(compile time polymorphism or static polymorphism or early binding)
Same method name + different argument types(or no of arguments)

Advantages?
- Not having method overloading feature will increases complexity of programming like in C, where we need to have different methods for same functionality involving int, float whereas in java we can have same method name which makes easier for programmer to use those methods. For ex: abs(int i), fabs(float f), dabs(double d), we can see that we used three functions to call same functionality, where as in java, abs(int i), abs(float f), so for anything we can just use “abs” function.
- In overloading method calling is taken care by compiler based on reference type.
```
Class test {
	public void m1() {sop(“no-arg”);
	public void m1(int i) {sop(“int-arg”);
	public void m1(float f) {sop(“float-arg”);
	//Above are overloaded methods
}

p s v m(string [] args) {
	test t = new test();
	t.m1();
	t.m1(10);
	t.m1(10.5);
}
```

Case (1): 
Automatic promotion :
When resolving overloaded methods if exact method is not available the we do not get any compile time error immediately, the compiler first promotes the arguments to the next level and checks whether the matched method is available, if its available then compiler considers it, otherwise promotes it to next level. This process will continue until all possible promotions are completed. If no match is found we would get compiler error!
Promotion available : byte->short->int->long->float->double
char->int->long->float->double
```
Class test {
	public void m1(int i) {sop(“int-arg”);
	public void m1(float f) {sop(“float-arg”);
	//Above are overloaded methods
}

p s v m(string [] args) {
	test t = new test();
	t.m1(10); //int arg
	t.m1(10.5f); //float arg
	t.m1(‘a’); //int arg
	t.m1(10L); // float arg
	t.m1(10.5); //compile time error, cannot find symbol
}
```
Case (2): 
While resolving overloaded methods compiler will always give precedence for child class(String, check below ex) when compared with parent type argument(Object).
```
Class test {
	public void m1(String s) {sop(“string version”);
	public void m1(Object O) {sop(“object version”);
	//Above are overloaded methods
}

p s v m(string [] args) {
	test t = new test();
	t.m1(“harsha”); //string version
	t.m1(new Object()); //object version
	t.m1(null); //string version
}
```
Case (3):
```
Class test {
	public void m1(String s) {sop(“string version”);
	public void m1(StringBuffer sb) {sop(“stringbuffer version”);
	//Above are overloaded methods
}

p s v m(string [] args) {
	test t = new test();
	t.m1(“harsha”); //string version
	t.m1(new StringBuffer(“harsha”)); //string buffer version
	t.m1(null); //compilation error(reference to m1 is ambiguous), because both string and stringbuffer are child classes for object, hence compiler doesn’t know which one should be give more preference.
}
```
Case (4):
```
Class test {
	public void m1(int i, float f) {sop(“int-float version”);
	public void m1(float f, int i) {sop(“float-int version”);
	//Above are overloaded methods
}

p s v m(string [] args) {
	test t = new test();
	t.m1(10, 10.5f); //int-float version
	t.m1(10.5f, 10); //float-int version
	t.m1(10, 10); //compilation error(reference to m1 is ambiguous)
	t.m1(10.5f, 10.5f); //compilation error(can’t find symbol m1(float, float))
}
```

Case (5): 
In general, when using method overloading varargs method get low priority as compared to normal method. i.e, if other method is matched then only varargs will execute.

Case (6): 
In overloading method resolution(which method has to executed parent or child method) is always taken care by compiler based on reference type, hence overloading is also called as compile time polymorphism or static polymorphism or early binding. Hence in overloading, runtime object won’t play any role.
```
class Animal{
}
class Monkey extends Animal{
}

class Test {
	public void m1(Animal a) {
		sop{“animal version”};
	}
	public void m1(Monkey m) {
		sop{“monkey version”};
	}
}

p s v m(string [] args) {
	Test t = new Test();
	Animal a = new Animal();
	t.m1(a); //animal version
	Monkey m = new Monkey();
	t.m1(m); //monkey version
	Animal a1 = new Monkey(); 
	t.m1(a1); //animal version - Since animal is referenced for a1 object, animal version is called.
}
```


## Method overriding(run time polymorphism or dynamic polymorphism or late binding)
Whatever methods parent has, by default they are available to child through inheritance, if child class is not satisfied with parent class implementation, then child is allowed to redefine that method based on its requirement, this process is called method overriding.
```
Ex:
class Parent{
	public void m(){  //overridden method
		sop(“parent”);
	}
}
class Child extends Parent{
	public void m(){   //overriding method
		sop(“child”);
	}
}

p s v m(string [] args) {
	Parent p = new Parent();
	p.m(); //parent
	Child c = new Child();
	c.m(); //child
	Parent p1 = new Child();
	p1.m(); //child, at runtime, p1 is referenced to child, hence child method is called.
}
```
In overriding, method resolution is always taken care by JVM based on runtime object and hence overriding is called as runtime polymorphism or dynamic polymorphism or late binding.

Rules for overriding:
- Method names and argument type must be same or method signature is same.
- Child class method return type need not same as parent method return type(JDK>1.4). Method overriding is said to be covariant with respect to return type, but Co-variant return type concept is applicable for only object types but not for primitive types.
- Parent class private methods are not available to child, hence we can’t do overriding. 
- Final parent class method can’t be overridden.
- Parent class abstract methods needs to be overridden in child class to provide implementation otherwise there is no use in having those abstract methods in parent class.
- In overriding “synchronize”, “native”, “strictfp”, “abstract” won’t have any restriction while doing method overriding.
- While overriding, we can’t reduce scope of access modifier(like public method in parent class can’t be changed to protected or default or private in child class), but increasing the scope is allowed.(private<default<protected<public)
```
Parent class: Child class
public: public
protected: public/protected
default: public/protected/default
private: can’t override
```

- If child class method throws an checked exception, then compulsory parent class method should throw same exception or it’s parent but there are no restriction for unchecked exception.

Overriding w.r.t static methods
- We can’t override a static method as non-static
- Similarly, we can’t override a non-static method as static
- If both parent and child class methods are static, then we won’t get any compile time error, it seems overriding concept is applicable is static methods, but it is not overriding, but is method hiding.

Method Hiding: All rules of method hiding are exactly same as overriding except for below:
- Both parent and child class methods should be static. 
- Compiler is responsible for method resolution based on reference(class) type. JVM is always responsible for method resolution based on runtime object.
Ex:
```
class Parent{
	public static void m(){  //overridden method
		sop(“parent”);
	}
}
class Child extends Parent{
	public static void m(){   //overriding method
		sop(“child”);
	}
}

p s v m(string [] args) {
	Parent p = new Parent();
	p.m(); //parent
	Child c = new Child();
	c.m(); //child
	Parent p1 = new Child();
	p1.m(); //parent
}
```
Overriding with varargs method: We can overwrite varargs method with another varargs method only. If we are trying to overriding a varargs method with normal method then it will be overloading as no of parameters are different.
Overriding concept is only for method but not for variables(instance or static).

￼
## Polymorphism
One name but multiple forms is known as polymorphism.
ex: method overloading, method overriding, usage of parent reference to hold child object(like List l = new LinkedList() or List l = new ArrayList()).
If we don’t know exact runtime type of object needs to be used, then we should use parent reference.
ex: List l = new ArrayList();

Polymorphism has two types :
1. compile time polymorphism or static polymorphism or early binding. ex: method overloading, method hiding
2. run time polymorphism or dynamic polymorphism or late binding ex: method overriding


## Static Control flow
If all the members in the class are static, then static control flow flows below rules:
```
Class test () {
	static int i = 10; —> (1), (7)
	static { —> (2)
		m1();  —> (8)
		sop(“test1”)}; —> (10)
	p s v m(String [] args){ —> (3)
		m1(); —> (13)
		sop(“main method”); —> (15)
	}
	public void static m2() { —> (4)
		sop(j); —> (9), (14)
	}
	static {  —> (5)
		sop(“test2”); —> (11)
	} 
	static int j = 20;  —> (6), (12)
}
```
1. Identification of static members from top to bottom(1 to 6)
2. Execution of static variable assignments and static blocks from top to bottom.(7 to 12)
3. Execution of main method(13 to 15)
Static blocks are executed at the time of class loading
RIWO = read indirectly write out : http://stackoverflow.com/questions/31779507/what-is-riwo-read-indirectly-write-out-state

//Without writing main method printing messages to console and writing static block
```
Class test {
	static {
		sop(“Hello”);
		system.exit(0);
	}
}
```
Output: Hello //it will not throw runtime exception

//Without writing static block and main method printing messages to console
Ex1:
```
Class test {
	static int x = m1();
	public static int m1() {
		sop(“Hello”);
		system.exit(0);
		return 10;
	}
}
```
Ex2:
```
Class test {
	static test t = new test();
	{
		sop(“Hello”);
		system.exit(0);
	}
}
```
Ex3: Using constructor
```
Class test {
	static test t = new test();
	test() {
		sop(“Hello”);
		system.exit(0);
	}
}
```

## Instance Control flow
If all the members in the class are static, then static control flow flows below rules:
1. Identification of instance members from top to bottom
2. Execution of instance variable assignments and static blocks from top to bottom.
3. Execution of constructor
Whenever constructor is called, instance block of code is automatically called.

If both instance and static block are present, then static blocks will get executed first.
```
Class test {
	{
		sop(“”Instance block 1”);
	}
	static {
		sop(“”static block 1”);
	}
	test () {
		sop(“constructor”);
	}
	p s v m (String[] args) {
		test t = new test();
		sop(“main”);
		test t1 = new test();
	}
	{
		sop(“”Instance block 2”);
	}
	static {
		sop(“”static block 2”);
	}
}
```
Output:
```
static block 1
static block 2
instance block 1
instance block 2
constructor
instance block 1
instance block 2
constructor
```

## Constructors
In how many ways we can get/create object in java?
1. Using “new” operator -> Test t = new Test();
2. Using newInstance() method —> Test t = (Test) Class.forName(“Test”).newInstance();
3. Using Factory method : By using class name if i am calling a method and method returns same class object is called factory method. ex: Runtime r = Runtime.getRuntime();
4. Using clone() method : Test t1 = new Test(); Test t2 = (Test)t1.clone(); —> t2 is new object
5. Using deserialisation 
	FileInputStream fis = new FileInputStream(“file.txt”);
	ObjectInputStream ois = new ObjectInputStream(fis);
	Dog d = (Dog)ois.readObject();

Purpose/Need of constructors:
To initialise an object.
```
Class student {
	string name;
	int rollno;
	Student (string name, int rollno) { //constructor
		this.name = name;
		this.rollno = rollno;
	}
	p s v m(String [] args){
		Student s = new Student(“Harsha”, “1”); //constructor is used to initialise the student object
		Student s = new Student(“Sriharsha”, “2”);
	}
}
```

- Only applicable modifiers for constructors are public, private, protected, default, if we try to use any other modifier(like static, final etc), we will get compile error.
- Complier is responsible to generate default constructor(but not JVM). If we are not writing any constructor, then only compiler will generate default constructor. If we are writing at-least one constructor, then we compiler won’t generate default constructor.

Prototype of default constructor
- Always no-args constructor
- Access modifier is exactly same as access modifier of class(public or default).
- It contains only one line super(); inside it. It is a no-argument call to super class constructor.


## Coupling
Degree of dependency between component is called Coupling. Two types : Loosely coupling(if dependency is less), Tight coupling(if dependency is more).
It is bad to have tight coupling in general because of below reasons:
- Any change will have impact on all the dependency components, so enhancement/any change is difficult.
- Maintainability of application is a headache if they are tightly coupled.

Loose Coupling vs Tight Coupling
Tight coupling is when a group of classes are highly dependent on one another.
This scenario arises when a class assumes too many responsibilities, or when one concern is spread over many classes rather than having its own class.
Loose coupling is achieved by means of a design that promotes single-responsibility and separation of concerns.
A loosely-coupled class can be consumed and tested independently of other (concrete) classes.
Interfaces are a powerful tool to use for decoupling. Classes can communicate through interfaces rather than other concrete classes, and any class can be on the other end of that communication simply by implementing the interface.


## Cohesion
For every component a clear will defined functionality is defined, then that component is said to be highly cohesive/follow high cohesion. Low cohesion component is difficult to maintain as code is cumbersome, enhancement changes will be difficult and reusability of code is minimal. 


## Type-casting
We can use parent reference to hold child object like for ex: Object O = new String(“harsha”);
We can use interface reference to hold implemented class object. for ex: Runnable r = new Thread();

A b = (C) d;
A = interface/class name
b = reference variable
C = interface/class name
d = reference variable
Compile time check for type-casting:
1. The type of ‘d’ and ‘C’ must have some relationship either child to parent or parent to child or same type, otherwise it will throw compile time error saying inconvertible type.
2. ‘C’ must be same/derived type of ‘A’ otherwise we will get compile error saying incompatible type.
Runtime check for type-casting:
1. Runtime object type of ‘d’ must be either same or derived type of ‘C’ otherwise, we will get runtime exception = ClassCastException
	Object O = new String(“harsha”);
	StringBuffer sb = (StringBuffer) O;
The above example satisfies compile time check, but runtime check fail because O is of type String which has no relationship with StringBuffer. Hence, A, b, C must be either same or derived types.
```
A class(parent) —> B class(Child) —> C class(grand child)
C c = new C();
B b = new C(); === (B)c -> type casting c with B 
A a = new C(); === (A(B))c) -> type casting c with A

Class P {
	public void m1() {}
}
Class C {
	public void m2() {}
}
C c = new C();
c.mi1();
c.mi2();

P p = (P)c;
p.mi1();
p.m2(); // compilation error
```

## Immutable
There are many immutable classes like String, Boolean, Byte, Short, Integer, Long, Float, Double etc. In short, all the wrapper classes and String class is immutable. We can also create immutable class by creating final class that have final data members.
```
public final class Employee{  
	final String pancardNumber;  
  
  	public Employee(String pancardNumber){  
		this.pancardNumber=pancardNumber;  
	}  

  	public String getPancardNumber(){  
		return pancardNumber;  
	}  
  
} 
```

final vs immutable
final means that you can't change the object's reference to point to another reference. Where immutable means that actual object's value can't be changed, but you can change its reference to another one.

## Marker interface 
in Java is interfaces with no field or methods or in simple word empty interface in java is called marker interface. Example of market interface is Serializable, Clonnable and Remote interface. Marker interface in Java is used to indicate something to compiler, JVM or any other tool but Annotation is better way of doing same thing.

## Strong reference vs soft vs weak vs phantom reference
https://dzone.com/articles/java-garbage-collector-and-reference-objects





## Code Refactoring
1. Duplicated code
2. Long methods
3. Complex conditional statements
4. Primitive Obsession
5. Indecent Exposure
6. Solution Sprawl
7. Alternative classes with Different interfaces
8. Lazy Classes
9. Large Classes
10. Switch statements
11. Combinational Explosions
12. Oddball Solutions


## General Notes

**Strong and weak typing**
A strongly typed language is more likely to generate an error or refuse to compile if the argument passed to a function does not closely match the expected type. On the other hand, a very weakly typed language may produce unpredictable results or may perform implicit type conversion

**Loose Coupling vs Tight Coupling**
Tight coupling is when a group of classes are highly dependent on one another.
This scenario arises when a class assumes too many responsibilities, or when one concern is spread over many classes rather than having its own class.
Loose coupling is achieved by means of a design that promotes single-responsibility and separation of concerns.
A loosely-coupled class can be consumed and tested independently of other (concrete) classes.
Interfaces are a powerful tool to use for decoupling. Classes can communicate through interfaces rather than other concrete classes, and any class can be on the other end of that communication simply by implementing the interface.


**Below points makes a class as immutable.**
* The instance variable of the class is final i.e. we cannot change the value of it after creating an object.
* The class is final so we cannot create the subclass.
* There is no setter methods i.e. we have no option to change the value of the instance variable.


**Helper Methods**



**Heavyweight vs Lightweight in java**
Heavyweight components like "AWT" components must be drawn using native GUI on a specific platform or EJB which depend on application servers
Where lightweight components like "Swing" components are drawn by java and don't rely on native GUI or spring framework are drawn from JDK and it’s jars not from application servers

**Keywords/Other notes in Java**
varargs : varrags allows the method to accept zero or multiple arguments. Advantage of using varargs is we don't have to provide overloaded methods so less code.
http://www.javatpoint.com/varargs
```
class VarargsExample{  
   
 static void display(String... values){  
  System.out.println("display method invoked ");  
 }  
  
 public static void main(String args[]){    
 display(); //zero argument   
 display("my","name","is","varargs"); //four arguments  
 }   
}
```

Static Binding vs Dynamic Binding

Decoupling

Serialization
Method overriding vs Method overloading
Exceptions
Multithreading
Collections
Strings
Memory management in Java
Spring
Servlets/JSP
Annotations
WebServices



Useful Links

http://javarevisited.blogspot.in/2013/03/top-15-data-structures-algorithm-interview-questions-answers-java-programming.html
http://javarevisited.blogspot.in/2011/09/spring-interview-questions-answers-j2ee.html
http://javarevisited.blogspot.in/2015/10/133-java-interview-questions-answers-from-last-5-years.html
http://javarevisited.blogspot.in/2011/03/10-interview-questions-on-singleton.html
http://javarevisited.blogspot.in/2011/07/java-multi-threading-interview.html
http://javarevisited.blogspot.in/2015/01/why-override-equals-hashcode-or-tostring-java.html
http://netjs.blogspot.in/p/core-java-interview-questions.html

