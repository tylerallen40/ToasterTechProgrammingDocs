# FRCProgrammingCheatSheet
A cheat sheet covering basic java concepts for FRC

# Basic Programming Concepts	

## Variables
Variables store data of a certain type. Variables can be declared locally inside any function, or inside a **class** as an **instance variable** (see **class** section). The datatype of a variable can be a built in type (**int**, **double**, **String**), or a **class** in which case the variable would be reffered to as an **instance** of that class.

Variables can be declared as follows:
```Java
datatype x; // Declaring a variable 
datatype x=value; // Declaring a variable and setting the value
```

### Examples:
```Java
int y; // Create an integer variable without assigning a value;
int x=1; // Creates a variable stroing an integer number and assiging it one 
String name="Joe"; // Create a new String variable with value Joe
TalonSRX talon=new TalonSRX(0) // Create a new TalonSRX variable and give it the value of a TalonSRX in port 0
boolean z = true; // Declare a boolean as true
```

## Builtin Datatypes
Java has several built in datatypes: 
| Datatype  | Description | Examples |
| ------------- | ------------- | ------------- |
| int  | whole number  | `1, 2, 3, -1, -2, -3` | 
| double  | decimal representation of a number (there are some hangups here, but we will save that for later)  | `1.0, 0.0, -1.0` |
| boolean | true or false | `true, false` |
| char | single character | `'a', 'b', 'z'` | 
| String | a word, or a string of characters | `"test"`| 

In addition java has useful builtin classes that will be covered as needed.

## Operators
Java has basic operations that can be performed on datatypes. 

| Operator  | Description | valid datatypes | Examples |
| ------------- | ------------- | ------------- | ------------- |
| x = y | assign to variable  | all datatypes | `x = 1` |
| x == y | compares values, evaluates as true if both are equal | all basic datatypes* | `1 == 1, 1 == 2, x == 1` |
| x > y | compares values, evaluates as true if x is greater than y | int, double** | `1>0, x>0,` |
| x < y | compares values, evaluates as true if x is less than y | int, double** | `1 < 0, x < 0,` |
| x + y | adds two values together | int, double, String*** | `1 + 0, x + 0,` |
| x - y | subtracts two values | int, double | `1 - 0, x - 0,` |
| x * y | multiply two values together | int, double | `1 * 0, x * 0,` |
| x / y | divide x by w | int, double | `1 / 2, x / 2,` |
| x % y | divide x by y and get the remainder  | int | `5 % 2, 4 / 2,` |
| x && y | logical and, returns true if both x and y are true  | boolean | `x && y, x && true` |
| x \|\| y | logical or, returns true if either x or y are true  | boolean | ```x \|\| y, x \|\| true``` |
| !x | negation, returns the opposite of the boolean ie. true => false or false => true  | boolean | `!x,` |

\* equality on instance techincally works but does not give the results you are usually looking for. Generally comparision of classes is not very common in FRC.

\*\*  doubles have some pitfalls that aren't very relevant to FRC and won't be covered here

\*\*\*  addition on a string results in concatination of the string, ie appending one string to the end of the other/ 

## Functions/Methods
While variables store data, functions manipulate data to do things. In other words functions take in data, perform a calculation on it and give us new data. Functions sometimes also perform other actions **side effects** such as setting the value of a motor controller. Java functions are usually defined in classes and are referred to as methods, but can usually be used interchangably. 

Functions have 2 parts, the declaration which determines the **function name**, the **return type** and the **arguments**, and the **function body**. Methods additionally have an **access modifier** (see **class**)

Java methods can be declared in this way:
``` Java
access_modifier datatype function_name(argument_datatype arguement_name) {
    function_body;
    return return_value; //Not needed if datatype is void.
}
```

### Examples
``` Java
public boolean isGreaterThanZero(int number){
    return number > 0;
}
public int sum(int number1, int number2, int number3 ){
    return (number1 + number2 + number3),
}
public int sumIsGreaterThanZero(int number1, int number2, int number3 ){
    int sumValue = sum(number1, number2, number3);
    return isGreaterThanZero(sumValue);
}
```

### Terms 
**Function Name**: defines the name of the function to use elsewhere

**Return Type**: defines the datatype of the value the function will return. This can be any datatype, or void if you don't want to return any value. The value returned is determined by the return key word.

**Arguments**: defines the data the function can take in to do its computation. All java methods have an implicit this argument that allows it to access the instance variables (see **class**)  

**Function Body**: the body of the function. Contains any computation that needs to be done as part of the function. Local variables can be defined in the function body to store temporary values and other functions can also be called.

**access modifier**: for a method determines who can call it, *usually* should be public for methods.

## Conditionals
For anything non trival it is important to do different things depending on the results of the computation. To do that we use a **conditional statement**. A conditional statement runs one code path if a statement evaluates to true, and another if it is evaluates to false. 

### Declaration:
``` Java
if(conditional expression) {
    // execute this code if conditional expression is true
} else if (conditional expression 2){
    // execute this code if conditional expression 2 is true
} else {
    // execute this code if the expression is false
}
```

### Examples
``` Java
public int onlyPositive(int number) {
    if (number < 0 ) {
        // Return the negative of a negative number
        return - number; 
    } else {
        return number;
    }
}

public double filterDeadzone(double value, double deadzone) {
    // Return a value only if it is greater than the given number, else return zero
    boolean isGreaterThan = number > deadzone;
    if (isGreaterThan) { // Expression can also be a boolean variable
        // Return the negative of a negative number
        return - number; 
    } else {
        return 0;
    }
}

```

## Classes 
Classes can be thought of blueprints that define the behavior of the code in the abstract.  

Like blueprints for real things, classes must also be built before they can be used. Classes can be built or **instantiated** by using a special method called the **constructor** to create an **instance** or **object** with specific data. You can have multiple seperate **instances** of the same class at once, which allows you to easily reuse code. 

Classes contain data as **instance variables**, and **methods** that act on that data. **Instance Variables** are unique to the instance, so if you create another instance of a class it will have different **instance variables** but the same **methods**. The methods might do different things since they are allowed to act on **Instance Variables**. 

**Instance Variables** can be reference inside of methods by the following syntax:
``` Java
this.instanceVariableName;
```

They can also be set:
``` Java
this.instanceVariableName=value;
```

Once an instance is created you have access to any public **methods** or **instance variables** for that class.

### Declaration
Like a method a class contains two parts a **declaration**, and a **definition**. A declaration gives a **class name** and **access modifier** (usually public). The definition consists of a body surronded by curly brackets. 

Inside the body you define the **instance variables** and **methods**. Any variable inside the body that is not inside a method is an **instance variable**, and any function inside the body is a **method**. 

Take note that java classes must be created in their own file with the same name as the class and the extension `.java`.
``` Java
// In a file called ClassName.java
public class ClassName {
    // Instance Variable
    private datatype instanceVariable;

    // Constructor, note that it is a method without a returnType 
    public ClassName(datatype constructorArg) {
        this.instancevariable = constructorArg;
    }
    
    // A default constructor with no args
    public ClassName() {
        this.instancevariable = value;
    }

    // Method
    public void methodName() {
        // do something
    }
}
```
Note all java classes must be in a file with the same name as the class. 

### Constructors
To create an instance use a special method called a **constructor**. A **constructor** is a special method that is always the same name as the class it is a part of and has no return value. 

Constructors can optionally have **arguments** that can define what data the instance is being created with. There can be multiple constructors as long as they have different arguement lists (such as a empty one that will provide default values).

Example call of a constructor:
``` Java
ClassName variableName = new ClassName()
```

### Examples
``` Java
public class Toggle {
    private boolean state;

    public Toggle() {
        this.state = false;
    }

    public boolean getState() {
        return this.state;
    }

    public void update(boolean trigger) {
        if(trigger) {
            this.state = !this.state;
        }
    }
}
```

``` Java
public class EdgeDetect {
    // Detects when an edge occurs in a digital signal, ie going from true => false or false => true
    private boolean detectLowToHigh;
    private boolean detectHighToLow;
    private boolean lastSignal;

    public EdgeDetect() {
        this.detectLowToHigh = true; // Default to bidirectional
        this.detectHighToLow = true;
        this.lastSignal = false;
    }

    public EdgeDetect(boolean detectLowToHigh, boolean detectHighToLow) {
        this.detectLowToHigh = detectLowToHigh; // Default to bidirectional
        this.detectHighToLow = detectHighToLow;
        this.lastSignal = false;
    }

    public boolean detect(boolean signal) {
        boolean lowToHigh = !this.lastSignal && signal; // last signal is false and current is true
        boolean highToLow = !signal && this.lastSignal; // last signal is true and current is false
        this.lastSignal = signal;
        if (this.detectLowToHigh && this.detectHighToLow) { // If bidirectional return either
            return lowToHigh || highToLow;
        } else if (this.detectLowToHigh) { // Else return the correct one that is enabled
            return lowToHigh;
        } else if (this.detectHighToLow) {
            return highToLow;
        } else {
            return false; // return false if neither are enabled
        }
    }
}
```

Used in code:
``` Java 
// This is an example to implement a toggle on a button (represented by the constant booleans as an example)
EdgeDetect edgeDetect = new EdgeDetect(true, false); // Only on high
Toggle toggle = new Toggle();

toggle.update(edgeDetect.detect(false));
boolean value1 = toggle.getState(); // False

toggle.update(edgeDetect.detect(true));
boolean value2 = toggle.getState(); // True
```