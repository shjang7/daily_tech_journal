# Daily Tech Journal

## Ruby on Rails
### Skinny Controllers, Skinny Models, Fat Services (13.feb.2020)
Traditionally, it has the term "Skinny Controllers, Fat Models". <br />
Controllers are hard to test; to keep skinny controllers, we could move as many methods to fat model.<br />
But if the model structure becomes lengthy code, it is hard to read and can break the single responsibility rule.<br />
We could move some methods to services to have enhanced readability and to keep high cohesion and low coupling.

### Callbacks (12.feb.2020)
Callbacks are hooks into the life cycle of an Active Record object that allow you to trigger logic before or after an alteration of the object state. (api.rubyonrails.org)<br />
ex) before_action, after_save in rails controller

### The advantages of using Ruby on Rails (23.jan.2020)
#### Faster development time
Ruby on Rails minimizes the website development time by 25-50% as compared to other popular web frameworks.

It has many ready-made plugins which are gems, MVC structure, modular design, object-oriented, and huge open-source communities.

### Additional advantages of using Ruby (23.jan.2020)
#### Clean and Simple Syntax
The syntax is modest and compact, which empowers developers to solve complex problems with fewer lines of code.<br /> It supports the human-readable code as well.

#### Metaprogramming
Ruby can be designed to read or transform other programs, and even modify itself while running.

## Discrete mathematics
### Counting theory (10.feb.2020)
#### Permutation
The Permutation is the arrangement of elements with an order.<br />
The number of cases from n elements picking r is that,
```
nPr = n! / (n - r)!
Because of: nPr = n x (n-1) x ... x (n - r + 1) = n! / (n - r)!
Consider: 0!(factorial) == 1, n! = n x (n-1) x ... x 1! x 0!
```
#### Combination
The Combination is the arrangement of elements with no order.<br />
The number of cases from n elements picking r is that,
```
nCr = n! / (n - r)! r!
Because of: nCr = nPr / r! (to disregard order)
```

### WebSockets

#### ActionCable (21.jan.2020)
Web applications are giving service using the HTTP protocol, half-duplex communication between server and client.<br /> For example, chatting app needs to send info from server to client, it uses polling in background service.<br /> But, rails 5.0 ActionCable integrates WebSockets to enable bidirectional simultaneous communication between server and client.

### An introduction about Rails 6 framework

This writing is to introduce Rails framework which is a server-side web app framework to a person new to and inexperienced in Rails.

```
source /
│
├─ app /
│  ├─ controllers
│  ├─ models
│  └─ views
│
├─ config /
│  └─ routes
│
└─ db /
   └─ migrate
```

#### MVC (13.jan.2020)

Rails has a model-view-controller (MVC) design pattern.<br />It presents default structures for a database, a web service, and web pages.<br />I am going to talk about this today.

The model contains data for application and often linked to a database.<br />And it has an order which can be used for business purpose.<br />And it does not know user interface; it means it can be reused.

The view generates the user interface, which presents data to the users.<br />Many views can access the same model for different reasons.<br />Once the view created, the data is displayed to the users.

The controller receives events from the outside world, usually through views.<br />It interacts with the model and displays the appropriate view to the users.

#### Routes (14.jan.2020)

```
source /
│
├─ app /
│  └─ controllers /
│     └─ users_controller.rb
│
└─ config /
   └─ routes.rb

[ users_controller.rb ]
  def index
    @users = User.all
  end

[ routes.rb ]
  get 'users#index', as: :users
```

The Router in rails navigates the URL or path to proper controllers. <br />For example, the Router 'users URL' called by external links such as user input or command line, then it will connect to 'users_controller' 'index' method.


## Ruby
#### Reference external files (11.feb.2020)
'load' every time access the file, 'require' access the file once at the initial time. <br />
And 'include' enables to access the module's methods as instances, <br />
while 'extend' allow us to access the module's methods as class methods.
```
Module Talk
  def say_hi
    puts 'hi'
  end
end

class Ex1
  include Talk
end

class Ex2
  extend Talk
end

Ex1.new.say_hi #=> hi
Ex2.say_hi #=> hi
```

#### The differences between modules and classes (07.feb.2020)
The big difference is that Class can generate an instance while Module is not.<br />
While Class can have subclass, but Module cannot have it.<br />

Ruby doesn't provide multiple inheritances. <br />
But if a Class which didn't access enumerable methods has the 'include Enumerable' keyword, it can use enumerable methods. <br />
This way, we can keep a simple structure and reuse some methods of modules.

### Closures (24.jan.2020)
Closures often pass into a function as a parameter, a particular part in the function can call the closure.<br />
Closures have Blocks, Procs and Lambda's.

#### Blocks

The Block is a snipped code, after passing into a function, it can be executed with the 'yield' in the function.<br />
If we want to use the same Block to another array2 or array3, to prevent repeating it, we could use Procs or Lambda's.

<details>
  <summary>example</summary>

  ```sh
  class Array
    def some_func
      self.each do |n|
        ...
        x = yield(n)    (n = 3 => 3 ** 2 => 9)
        ...
      end
    end
  end

  array = [1,2,3,4,5]
  array2 = [11,14,20,24,25]
  array.some_func do | n |
      n ** 2
  end
  array2.some_func do | n |
      n ** 2
  end
  ```
</details>

#### Procs

```
class Array
  def some_func(s)
    self.each do |n|
      ...
      x = s.call(n)    (n = 3 => 3 ** 2 => 9)
      ...
    end
  end
end

array = [1,2,3,4,5]
array2 = [11,14,20,24,25]
square = Proc.new do | n |
    n ** 2
end
array.some_func(square)
array2.some_func(square)
```

#### Lambda's

```
class Array
  def some_func(s)
    self.each do |n|
      ...
      x = s.call(n)    (n = 3 => 3 ** 2 => 9)
      ...
    end
  end
end

array = [1,2,3,4,5]
a = lambda do |n|
  n ** 2
end
array.some_func(a)
```

```
def some_func(b)
  b.call(1, 2)
end
some_func(Proc.new{ |a, b, c| print a, b, c }) => c == null
some_func(lambda{ |a, b, c| print a, b, c }) => wrong number of parameters error
```

#### The differences between *lambda* and *proc* (12.feb.2020)
*Lambda* and *proc* looks similar but different.<br />
While *proc* doesn't check parameters count, *lambda* checks it and throws an error in case of no matches.

And it is another difference.<br />
*Proc* works like code snippet, and once it has seen the return statement, it returns directly.<br />
But *lambda* is an anonymous function and works like a keyword, and it will read the function until the end of the line.
```
def first
  Proc.new { return 'baam' }.call
  return 'this is not reached'
end

def second
  lambda { return 'baam' }.call
  return 'this is printed'
end

print first #=> 'baam'
print second #=> 'this is printed'
```

## React
#### State and props (06.feb.2020)
React component can handle data using props and state.

Props(properties) is the data what parent component gives child component.<br />
Once the child component get props, it cannot be modified.

State is defined with a default value when a component mounts and can be changed.<br />

Props are a component's configuration, props also includes callback functions.<br />
State is a data structure.

#### Why Hooks are preferred than using classes (28.jan.2020)
Hooks provide intuitive API such as useState, useEffect. <br />Using Hooks, we can abstract state-related logic, and it enables us to reuse and share that logic.

## Script language overview (05.feb.2020)
The software at an early age was written in assembly language. <br />After building the compiler, software developers can write code for the more human-understandable higher language, and compiler changes it to assembly one.<br />

But compiler needs compile time for executing a program. <br />If the software changed often, it becomes overloaded.<br />

Scripting language such as Python, Javascript, and Ruby is interpreted when execution time.<br />Generally, compiled language is faster at execution time due to running assembly language.<br />But script language has advantages of faster building time.

## CPU scheduling (04.feb.2020)
When we make a cup of coffee, we are not only waiting for boiling water.<br />
We can clean or wash or setting a cup and table while the water is boiling.<br />

CPU process also be a status until the job is done.<br />
How the process can manage the limited resources efficiently.<br />

```
Process scheduling
│
├─ Preemptive scheduling
│  │
│  ├─ Shortest remaining time
│  ├─ Round-robin
│  ├─ Multi-level Queue
│  └─ Multi-level feedback Queue
│
└─ Non-Preemptive scheduling
   │
   ├─ Highest response ratio next
   ├─ Shortest job first
   ├─ Priority
   ├─ Deadline
   └─ FIFO
```

Preemptive scheduling is suitable for handling tasks what has higher priority, but it cannot assume response time when it has overhead.<br />
Shortest remaining time scheduling is a priority for shortest time.<br />
Round-Robin scheduling separate equal amount of time to every task, and handle those with first in first out.<br />
Multi-level queue scheduling is using several ready queues, and those queues also have a priority.<br />
Multi-level feedback queue scheduling is similar with the multi-level queue, but each process can move among queues<br />

Non-preemptive scheduling happens when a previous task is finished.<br />
Highest response ratio next scheduling bridge the gap of inequality of long-hour task and short task and set the priority.<br />
Shortest job first scheduling has a higher priority for short time process, and it decreases average waiting time.<br />
Priority scheduling gives priority to process static or dynamic way.<br />
Deadline scheduling lead work to end within particular term.<br />
First In First Out scheduling care only the arrived time.<br />


## Software design pattern
<details>
  <summary>Patterns</summary>

```
├─ Creational Pattern
│  │
│  ├─ Factory Method
│  ├─ Abstract Factory
│  ├─ Builder
│  ├─ Prototype
│  └─ Singleton
│
├─ Behavioral Pattern
│  │
│  ├─ Chain of Responsibility
│  ├─ Command
│  ├─ Exchange role
│  ├─ Iterator
│  ├─ Interpreter
│  ├─ Mediator
│  ├─ Memento
│  ├─ Observer
│  ├─ State
│  ├─ Strategy
│  ├─ Template method
│  └─ Visitor
│
└─ Structural Pattern
   │
   ├─ Adapter
   ├─ Bridge
   ├─ Composite
   ├─ Decorator
   ├─ Facade
   ├─ Flyweight
   └─ Proxy
```
</details>

Object-oriented languages are manageable to implementing software design patterns. <br />Patterns help improve developer communication. <br />But like always, uses of patterns should not be overloaded more than practical reason.

### Behavioral Pattern (03.feb.2020)
For example, there is a lion and a cheetah.<br />
The common Behavioral between them is hunting animals, living in the yard.<br />
If it has a parent class like Wild animals, then the Lion and Cheetah class can inherit it and implemented detail.

ex) Template Method

### Creational Pattern
#### Singleton Pattern (17.jan.2020)
We use this if we want to limit the creation of the class into one object only.<br />
ex) User Interface, Game Board

But it should be used in a limited way. <br />This pattern doesn't fit with a multi-thread system while it can generate only one instance. <br />Also, it could be violating the single responsibility rule. <br />As a conclusion, this pattern needs carefully used.

#### Factory Method (17.jan.2020)
When we create a object, this pattern secures producing the same instances.

#### Abstract Factory (17.jan.2020)

The customer application can access to use of factory with no knowledge of conception through an interface of factories.

## Testing Software
#### The importance of testing (31.jan.2020)
If a business application doesn't work correctly, the manufacturers can lose the business image, time, money, for some case life as well.

The software test is very important in the reasons above, but for the faster development, a company can overlook building software without the test.

The purposes of the test are checking software working well, but also the satisfaction of the software specifications.

The test can be done by a unit or an integration test. <br />The unit test helps us to write smaller and full-fill single-responsibility code condition. <br />Another advantages of unit test are catching the problems early, more straightforward integration, and improving the architecture.

## General Programming
### Static method, static variable
#### Class method, a.k.a. static method (30.jan.2020)
The Class method used to be called as a static method.<br /> When the class loads, this static method prepared in memory.<br /> The Static method or static variables can be accessed everywhere in application like class.

<details>
  <summary style="">Example</summary>

- c++
```
Class Robot {
    static void hi(name) {
      cout << name << ' hi!!';
    }
}
```
- ruby
```
Class Robot
    def self.hi(name)
      print `${name} hi!!`
    end
end
```
- class method
```
human_name = 'suhy'
Robot.hi(human_name)
>> suhy hi!!
```
- instance method
```
my_dog = Dog('warr')
my_dog.bark()
>> Woof Woof
```
</details>

#### Class variable, a.k.a. Static variable (14.feb.2020)
The static variable can be called a class variable. <br />
As a static method, a static variable is defined when the class called.

In Ruby, the variable with @@var_name form is the static variable. <br />
The static variable keeps the same value for the class while the instance variable formed by @var_name can have a different value for each instance.

#### The differences between Session and Cookie (29.jan.2020)
It is different from the data saving place of user's information.<br />
Cookie does not use server's resources, Session uses server's resources.<br />
The session has better at security, and Cookie has better response speed.

## Data structures

```
Data structures (non-primitive)
│
├─ Linear data structures
│  ├─ Array
│  ├─ Linked list
│  ├─ Stack
│  └─ Queue
│
└─ Non linear data structures
   │
   ├─ Graphs
   ├─ Trees
   ├─ Trie
   └─ HashTable
      │
      ├─ Set
      └─ Map
```

#### The differences between Set and Map (27.jan.2020)
Set or Map can be stored in computer memory with an order or as a Hashmap Table.<br />
The case of storing with order is useful to have sorted order, but we could have constant time efficiency using Hashmap Table.<br />So the purpose of using it should be considered, and it needs trade-off for the circumstance.

Set is a mathematical terminology to use in computer programming; it indicates whether an element contained in a Set or not.<br />
And Map is used to store key-value pairs, and this can solve Graph algorithm, frequency algorithm.

#### The differences between Stack and Queue (16.jan.2020)
Queue uses First Input First Output (FIFO). <br />For instance, the people wait for a queue to hop on the bus, the first person in the line will get on the bus.

Stack uses Last Input First Output (LIFO). <br />For example, when I put one piece of paper on the stack of papers, some others will pick first that paper what I put from the pile.

#### The selection between Breadth-First Search and Depth-First Search (14.feb.2020)
Breadth-First Search traverse the shortest distance from current location.<br />
While traversing, it pops current spot, checks visited point, pushes the place to visit.<br />
BFS is useful to perform maze algorithm.<br />
But if we need to consider some additional information like weight factor, it is better to use Depth-First Search to handle information efficient in memory.

#### The differences between Array and Linked list (14.jan.2020)
The Array is a consistent set of a fixed number of data items.<br />And the Linked list is an ordered set comprising a variable number of data items.

The indexes directly or randomly access the Array.<br />But the Linked list is sequentially accessed, traverse starting from the first node in the list by the pointer.

The Array relatively slow at insertion or deletion as shifting is required, but the Linked list is effective, fast and efficient for that.

However, access time in memory of Linked list is slower.<br /> Because, While Array elements physically assigned consecutively in the hardware memory during compile time, Linked list elements are stored randomly in hardware during the run time.

The linear search can search them both.<br /> But Array can be searched by binary search, while Linked list is not.

## Javascript

### Asynchronous
The response time after sending a request to the server could be slower than code execution time. <br />So we need to use the asynchronous function.

#### Async-await (22.jan.2020)
Async function is written like just general function, but it works like promise function.

An Async function can involve Await; it pauses Async function and waits for promise work; it resumes Async function and returns a result.<br />While the Async function breaks, the calling function runs continuously.

Await keyword only works in an Async function.<br />If we use this out of Async function, it will get a syntax error.


## Asymptotic notation

#### *Θ*, *O*, *Ω*, *o*, *ω* notations (20.jan.2020)
For the small size algorithm, the task ends very fast regardless of the effectiveness.<br />
But when the input size is big enough, the efficiency becomes an issue.<br />
So, to calculate the execution time of an algorithm, always we analyze the time for big sized input case, aka Asymptotic notation.

First, Look the three notations.<br />
**Big *Θ*** (theta) notation means an **asymptotic increasing rate** of an algorithm.<br /> *Θ*(*f*(*n*)) is a group of matching asymptotic increasing rate with *f*(*n*). <br />For example,
```sh
5n² + 4n + 6 = Θ(n²)
```

**Big *O*** notation means asymptotic **upper bound** of increasing rate, and it calculates **worst case**.<br />
And **Big *Ω*** (omega) notation means an asymptotic **lower bound** of increasing rate, and it calculates the **best case**.

And look deep into the strict definition.
It also has **Little *o*** and **Little *ω***.
**Little *o*** means asymptotic **strict upper bound** of increasing rate.
```sh
5n = O(n)
5n = o(n²)
```
**Little *ω*** means asymptotic **strict lower bound** of increasing rate.
```sh
5n = ω(n)
```

## Computer Networking

### Network Layers

Two computers communicate help of network connection. <br />But, if this two has different OS or architecture or even different capacity of data acceptance speed,<br />
how they can communicate with each other in real-time.

#### Five-layer internet protocol stack (15.jan.2020)

```
Protocol stack
│
├─ Application
├─ Transport
├─ Network
├─ Link
└─ Physical
```

Each layers is a package of protocols.

The Application layer includes some protocols, such as the HTTP, SMTP, FTP protocol. <br />It also does transmitting human-readable url domain to the actual address.
Application layer data transported by TCP, UDP protocols in the Transport layer.

Network layer moves Datagram packets from one host to another.<br />
The Network layer combines Transport layer segment and a destination address, like a postal service a letter with a destination address.

The Network layer passes the Datagram down to the Link layer, and the Link layer passes the Datagram up to the Network layer.

Finally, the job of the Physical layer is to move the individual bits within the frame from one node to the next.

But we should mention that it has not only protocol stack around. <br />The network can be organized around seven layers which is OSI (Open System Interconnection) model.

#### 7 layers of OSI model (15.jan.2020)

```
OSI model
│
├─ Application
├─ Presentation
├─ Session
├─ Transport
├─ Network
├─ Data link
└─ Physical
```

OSI(Open System Interconnection) model has 7 layers.

Application layer includes HTTP, FTP, SMTP, ... protocols. <br />That provides services of network applications such as Chrome, Firefox, Outlook, Skype, etc.

Presentation layer receives data from the Application layer. <br />This data is the form of characters and numbers and translated to
machine understandable binary format. <br />And Presentation layer compresses this data for faster sending, also does encryption or decryption.

Session layer helps session management, authentication, authorization.

The Transport layer is envolved segmentation, flow control for speed differences, error control, connection-oriented and connection-less transmission.

The Transport layer provides various forms of process-to-process communication by relying on the network layer's host-to-host communication service.

The function of the Network layer is logical addressing of IPv4 and IPv6, path determination and Routing. <br />When the data arrives, the Routing does finding where to move data with the separation of host and computer address.

Their has two types of addressing, logical addressing is from the Network layer, and physical addressing is from Data link layer.<br />
The Data link layer is embedded as software in the network interface card of the computer.

Physical layer considered by the data communication through optic, electrical transmitting information.

### TCP

#### Three-Way Handshake (14.jan.2020)

We supposed to try a network connection such as opening google.com, what is going to have happened?

1. A client sends to server SYN packet which contains sequence numbers that support the server can connect client; this step is like "Hey, do you want to talk?"<br />
2. The server sends back to the client SYN/ACK packet with the help of sequence numbers; this step is like "Yeah, I received your message, do you want to talk?"<br />
3. Then the client sends ACK packet to the server, like "Yes, let's talk."

=> After this three-way Handshake occurs, the connection is established between the server and the client. <br />Now the packets between them can be transmitted. <br />The protocols loading over TCP is HTTP, FTP, SMTP and SSH.

As it has an opening connection, it also has a closing connection.

1. The client sends the server SYN/ACK packet; "There is no need connection, wants to leave."<br />
2. The server sends back to the client ACK packet, "Yes, I know that you want to leave, then bye."<br />
3. The client sends back to the server ACK packet, "Yes, bye!"
