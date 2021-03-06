## Introduction
An unexpected/unwanted event which disturbs normal flow of program, that event is called Exceptions
Objective of Exception handling : Graceful termination of the program. For ex: When trying to fetch some information from DB, if we get SQL exception due to some reason, if we don’t handle exception then there might be a chance of that connection not being closed, to avoid such sort of problems it is always recommended to handle these exceptions and graceful terminate the program.

Exception handling doesn’t mean repairing an exception. We have to provide alternative way to continue rest of the program normally is the concept of Exception handling. 
For ex: To read data from remote file locating at london, if not available read from local file in catch block.
```
try{
	//to read data from remote file
catch (FileNotFoundException e) {
	//read data from local file and continue rest of program
}
```


## Runtime stack mechanism
For every thread JVM will create a runtime stack. Each and every method call performed by that thread will be stored in the corresponding stack. Each entry in the stack is called stack frame/activation record. After completion of every method call, the corresponding entry from the stack will be removed. After completing all method calls, the stack will come empty which will be destroyed by JVM just before terminating the thread.

## Default exception handling in java
- Inside a method if any exception occurs, then method in which it is raised is responsible to create exception object by including the information like name of exception, description of exception and location at which exception occurs(stack trace).
- After creating exception object method handovers that object to the JVM. JVM will check whether the method contains any exception handling code or not. If the method doesn’t contain exception handling code then JVM terminates that method abnormally and removes corresponding entry from the stack.
- Then JVM identifies caller method(of the above method) and checks whether caller method contains any handling code or not. If the caller method doesn’t contain handling code then JVM terminates that caller method also abnormally and removes corresponding entry from the stack. This process will be continued until main method and abnormally ends main method if it also doesn’t contain exception handling code. Finally JVM handovers responsibility of exception handling to default exception handler which is the part of JVM.
- default exception handler prints the stack trace and terminates the program abnormally.
- default exception handler looks like Exception in thread “xx” “name of exception” : Description and stack trace

## Exception Hierarchy
**Throwable - Exception, Error**
Throwable class acts as root for java exception hierarchy. It defines two child classes Exception, Error
Most of the times exceptions are caused by program and Exceptions are recoverable.
Error are no-recoverable from programmer point of view. Most of the times errors are not caused by program and due to lack of system resources

**Checked vs Unchecked**

Checked Exceptions:
- The exceptions which are checked by compiler for smooth execution of the program at runtime, these exceptions are called Checked Exceptions. Ex: FileNotFoundException, InterruptedException etc..

Unchecked Exceptions:
- Some exceptions which are not checked during compile time(if programmer is handling or not), these exceptions are called Unchecked Exceptions. Ex: NullPointerException, ClassCastException, ArithmeticException etc..

- Whether it is checked or unchecked every exception occurs at runtime only. There is no chance of occurring any exception at compile time.
- RuntimeExceptions and it’s child classes, Errors and it’s child classes are unchecked. Except these remaining are checked.

Fully checked vs Partially checked
- A checked exception is said to be fully checked, if and only if all it’s child classes(along with itself) also checked. Ex: IOException, InterruptedException
- A checked exception is said to be partially checked, if and only if some of it’s child classes are unchecked. Ex: Exception, Throwable. Only possible partially checked exception are Exception, Throwable
- Within try/block if there is no chance of raising an exception, then we can’t write catch block for that exception. This rule is applicable for only fully checked exceptions


## Control flow in try catch
```
try{
	//risky code
}
catch(Exception e) {
	//alternative/handling code, we can try customized information.
}
```

## Methods to print stack information
e.printStackTrace() - name of the exception, description and stack trace 
e.toString() - name of the exception and description. sop(e) or sop(e.toString()) both are smae
e.getMessage() - only description
These methods are present in Throwable class

## try with multiple catch blocks
```
try{
	//risky code
}
catch(FileNotFoundException e) {
	//alternative/handling code, customized information w.r.t FileNotFoundException.
}
catch(ArithmeticException e) {
	//alternative/handling code, customized information w.r.t ArithmeticException.
}
catch(Exception e) {
	//alternative/handling code, general customized information to catch other exception.
}
```

## finally block
It is not recommended to maintain cleanup code(like closing DB connection) inside try block because there is no guarantee for the execution of every statement inside try. It is not recommended to maintain cleanup code(like closing DB connection) inside catch block because if there is no exception, then flow doesn’t enter this block and that code will not executed. Hence to maintain/execute cleanup code irrespective of whether exception raised or not raised and whether handled or not handled such type of best place is “finally” block.
finally block maintain “cleanup code” 
Even if return statement is there in try or catch block, finally block is executed.
```
try{
	//risky code
}
catch(Exception e) {
	//alternative/handling code
}
finally{
	//cleanup code
}
```
system.exit(0) means system shutdown, if it is used in try or catch block, then finally block will not get executed.

## difference between final, finally, finalize
final is a modifier applicable for classes, methods and variables. If a class is declared as final then we can’t extend that class(no inheritance or can’t create child class for that class). If a method is declared as final, then we can’t override that method in the child class. If a variable is declared as final, then we can’t re-assign value to that variable.
finally is a block always associated with try/catch to execute cleanup code. It will be executed always irrespective of whether exception raised or not raised and whether handled or not handled.
finalize is a method which is always invoked by garbage collector just before destroying an object to perform cleanup activities. Once finalize method is completed immediately garbage collector destroys that object.
Note: finally block is responsible to perform cleanup activities related to try block i.e, whatever resources which are opened as a part of it’s try block will be closed inside finally block.
final - try/catch/finally block level cleanup activities
Whereas finalize method is responsible to perform cleanup activities related to object i.e, whatever resources associated with object will be deallocated before destroying the object.
finalize - object level cleanup activities

## control flow in try-catch-finally, control flow in nested try-catch-finally, various possible combinations of try-catch-finally
- try-catch-finally order is important
- Whenever we are writing try, catch or finally or both would be written, otherwise we will get compile time exception.
- Whenever we are writing catch/finally block, try block is required i.e, catch/finally without try is invalid.
- Nesting of try-catch-finally it allowed.
- {} is mandatory for try, catch, finally blocks.

## throw keyword
We can create exception object and hand over the object manually to JVM for which we use throw keyword.
ex: throw new ArithmeticException(“/ by zero”);
- Best use of throw keyword for user defined exceptions or customised exceptions.
- After throw keyword statement, we can’t add any statement directly else we will error saying “unreachable code”.
- We can throw only Throwable type objects(child classes of throwable or class extending throwable or it’s child classes).

## throws keyword
We can use throws keyword yo delegate responsibility of exception handling to caller(may be JVM or other method), then caller method is responsible to handle that exception.
- throws required only for checked exceptions, use for unchecked exceptions will not have any impact.
- throws required only to convince compiler to execute the program and usage of throws keyword doesn’t prevent abnormal termination of the program.
- try/catch block has better usage compared to throws because try/catch causes normal termination unlike abnormal termination of program.
- we can use throws keyword for methods and constructors but not for classes.
- If we are using throws using a class like public m1() throws Test, then Test should of Throwable type(child classes of throwable or class extending throwable or it’s child classes).

## Top 10 exceptions
Based on the person who is raising an exception, all exceptions are divided into two types: 
JVM exceptions : The exceptions which are raised automatically by JVM whenever a particular event occurs are called JVM exceptions. Ex: ArithmeticExceptions, NPE, ArrayIndexOutOfBoundException, ClassCastException etc..
Programmatic exceptions : The exceptions which are raised either by programmer or API developer to indicate that something is going wrong. Ex: NotBalanceFoundException, IllegalArgumentException, NumberFormatException, IllegalStateException, AssertionError etc..


## Customized or user defined exceptions
Ex:
```
class InvalidAgeException extends Exception{
	InvalidAgeException(String s){
		super(s);  
	}
}
```

## 1.7 version enhancements like try with resources, multi-catch block
It is highly recommended to write finally block to close resources which are opened as the part of try block.
```
BufferReader br = null;
try{
	br = new BufferReader( new FileReader(“input.txt”));
	//use br based on our requirement
}
catch(IOException e) {
	//catch IO exception and handling code.
}
finally{
	//close br connection
	br.close();
}
```
The problem in above approach is we have define finally block to close the resources at any cost which increases complexity of programming and length of code. 
We can use try with resources to avoid above difficulty.
```
try(BufferReader br = new BufferReader( new FileReader(“input.txt”))){
	//use br based on our requirement
	//br is closed automatically just before try block is finished.
}
catch(IOException e) {
	//catch IO exception and handling code.
}
```
- We can declare multi-resources but these resources should be separated with ;(semi-colon) 
- All the resources that we are using should be AutoCloseable. For ex:, if we use BufferReader, it should implement java.lang.AutoCloseable(this contains only close() method). All IO, Database, Network related resources by default implemented AutoCloseable.
- All references within try resources are implicitly final, we can’t change them in the middle of try block.
```
try(BufferReader br = new BufferReader( new FileReader(“input.txt”))){
	br = new BufferReader( new FileReader(“output.txt”)); //Compile time error as we can’t reference
	//br is closed automatically just before try block is finished.
}
catch(IOException e) {
	//catch IO exception and handling code.
}
```

## Multi-catch block
Until 1.6, even though multi different exception having handling code in catch block, for every exception type we have separate catch block which increases the length of code like below:
```
try{
	//risky code
}
catch(ArithmeticException e) {
	e.printStackTrace();
}
catch(IOException e) {
	e.printStackTrace();
}
```

From 1.7 version, we can use multi catch block, now we can have single catch block that can handle multiple different type of exception provided their handling code is the same.
```
try{
	//risky code
}
catch(ArithmeticException | IOException e) {
	e.printStackTrace();
}
```
Note: In multi catch block, there shouldn’t be any relationship between exception types(like parent child relationship ex: ArithmeticException | Exception e is incorrect).

Exception propagation
Inside a method, if an exception is raised if we aren’t handling that exception then exception object will be propagated to caller then caller method is responsible to handle exception. This process is called exception propagation. In below ex: m1() has to handle exception as exception is propagated to m1 from m2.
```
m1(){
	m2();
}
m2(){
	sop(10/0);
}
```

Rethrowing Exception
We can use this approach to convert one exception to another exception type.
```
try{
	//risky code
}
catch(ArithmeticException e) {
	throw new NullPointerException();
}
```
## Customized exception handling by using try catch
