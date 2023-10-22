# Groovy
 There are 2 editors that come with groovy by default 
 - GroovyShell : run ```groovysh``` 
 ![Alt text](groovy/images/groovysh.png)
 - GroovyConsole: run ```groovyConsole```  
 ![Alt text](groovy/images/groovyconsole.png)


### HelloWorld in groovy 
- System.out is auto imported , so you can do println withou System.out 
- semi-colon at the end is optionl for the most part 
- parentheses are not required most of the time 

```groovy
println 'Welcome To Groovy'
``` 
### The assert statement 
assert can be used in test cases instead of junit or assertJ assertions , it gives a nice graph of details if the statment is false 

```groovy
int x = 3
int y = 4
assert 7 == x + y + 1 
```

``` 
Exception thrown

Assertion failed: 

assert 7 == x + y + 1
         |  | | | |
         |  3 7 4 8
         false

	at ConsoleScript61.run(ConsoleScript61:3)
```
### Automactic imports 
In groovy, the below imports are added by groovy 
```groovy
import java.lang.*
import java.util.*
import java.io.*
import java.net.*
import groovy.lang.*
import groovy.util.*
import java.math.BigInteger
import java.math.BigDecimal
```
This is done because the classes from these packages are most commonly used. By importing these boilerplate code is reduced.

### The def keyword 
Groovy is optionally typed, if you declare a variable of type String or Date or Employee , then you can't assign another type  

```groovy
int x = 3 
x = 'abc' 
 
Exception thrown

org.codehaus.groovy.runtime.typehandling.GroovyCastException: Cannot cast object 'abc' with class 'java.lang.String' to class 'int'
	at ConsoleScript62.run(ConsoleScript62:2)

```
def can be used to create untyped variable , the type will be determined at runtime 
```groovy
def x = 1 
println x.getClass() 
x = 'abc' 
println x.getClass() 
 
class java.lang.Integer
class java.lang.String
```
### Integer and Floating point types 
- No primitives (all are wrapper classes)
- floating values uses BigDecimal by default 
```groovy
println 3.getClass() 
println 777777777777777.getClass() 
println 88888888887878788788788788787878.getClass() 
println 0.5.getClass() 
 
class java.lang.Integer
class java.lang.Long
class java.math.BigInteger
class java.math.BigDecimal
```

### Operator Overloading 
Groovy allows you to overload the various operators so that they can be used with your own classes. 

```groovy
class Bucket{
  int size 
  
  Bucket(int size) {this.size = size}
  
  Bucket plus(Bucket other) {
    return new Bucket(this.size + other.size);
  }
}

def b1 = new Bucket(4)
def b2 = new Bucket(11) 
def b3 = b1 + b2
println b3.size
```
https://groovy-lang.org/operators.html#Operator-Overloading:~:text=Here%20is%20a%20complete%20list%20of%20the%20operators%20and%20their%20corresponding%20methods%3A

### String and Groovy Strings  
Groovy supports multiple types of strings 
- Java Strings (single quotes)
- GString (double quotes) : supports interplation 
- Multiline strings (3 quotes , 3 double quotes)
- Slashy strings : create Reqular expressions 
```groovy
def s = 'this is a String ${1 + 2}'
println s
s = "this is a String ${1 + 2}" 
println s
s = '''
select * from books b
where b.title = 'the west';
'''
println s
def zip =  /\d{5}(-\d)?/
assert '12345' ==~ zip

```

### POGOs
- In groovy , by default , attributes are private , methods are public and classes are public . 
- Getters and Setters are generated for you 
- property access ```p.last ``` will call the setter/getter
- If you need a custom getter/setter you can provide them 
- By default you get a map based constructor
- Groovy won't repalce something that is alrady generated 

```groovy

class Person {
   String first
   String last
   
   void setLast(String last) {
     println 'Inside setLast'
     this.last = last
   }
     
}

Person p = new Person()
p.setFirst('David')
p.last = 'Ortiz'
println "${p.first} ${p.last}"   

Person p2 = new Person(first:'Hanley' , last :'Ramirez')
println "${p2.first} ${p2.last}"
```

### ASTs
- You can add @ToString AST to autogenerate a toString implementation  
- You can use @EqualsAndHashCode also to add equals and hashcode 
- @TupleConstructor : adds a constructor that takes argments in order 
- @Cononical = @ToString + @EqualsAndHashCode + @TupleConstructor  
```groovy

import groovy.transform.*

@ToString @EqualsAndHashCode 
@TupleConstructor 
class Person {
   String first
   String last     
}

Person p1 = new Person(first :'Dustin' , last: 'Pedoria')
Person p2 = new Person(first: 'Dustin' , last: 'Pedoria')
Person p3 = new Person(first: 'David', last: 'Ortiz')
Person p4 = new Person('Dustin' , 'Pedoria')

println p1 == p2
println p1 != p3
Set people = [p1,p2,p3]
println people.size()
```
### Ranges
- Groovy provides range operator (..) to create ranges of object.
- Range operator works for all objects which implements Comparable and which provide some means to determine next and previous values

```groovy
Range r = 1..10
println r.from
println r.to
println r.contains(10)

r = 1..<10 // open range 
println r.contains(10)
```

```groovy
import java.time.LocalTime

Range timeRange = LocalTime.now()..LocalTime.now().plusHours(5)
println timeRange.from
println timeRange.to
```
### Lists 
- Groovy uses a native syntax for lists  
```groovy
List nums = [3,1,4,1,5,9,2,6,5]
println nums 
println nums.class.name
println nums + [19,19]
println nums << [19,20]

def nums2 = [3 , [1,4, [1,1]],5]
println nums2.flatten()
println nums2
println nums2.flatten() - 1
```


