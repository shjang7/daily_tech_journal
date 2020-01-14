# daily_tech_journal

## Computer Networking

#### TCP - Three-Way Handshake (14.jan.2020)

We supposed to try a network connection such as opening google.com, what is going to have happened?

1. A client sends to server SYN packet which contains sequence numbers that support the server can connect client; this step is like "Hey, do you want to talk?"
2. The server sends back to the client SYN/ACK packet with the help of sequence numbers; this step is like "Yeah, I received your message, do you want to talk?"
3. Then the client sends ACK packet to the server, like "Yes, let's talk."

=> After this three-way Handshake occurs, the connection is established between the server and the client. Now the packets between them can be transmitted. The protocols loading over TCP is HTTP, FTP, SMTP and SSH.

As it has an opening connection, it also has a closing connection.

1. The client sends the server SYN/ACK packet; "There is no need connection, wants to leave."
2. The server sends back to the client ACK packet, "Yes, I know that you want to leave, then bye."
3. The client sends back to the server ACK packet, "Yes, bye!"

## An introduction about Rails 6 framework

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

Rails has a model-view-controller (MVC) design pattern. It presents default structures for a database, a web service, and web pages. I am going to talk about this today.

The model contains data for application and often linked to a database. And it has an order which can be used for business purpose. And it does not know user interface; it means it can be reused.

The view generates the user interface, which presents data to the users. Many views can access the same model for different reasons. Once the view created, the data is displayed to the users.

The controller receives events from the outside world, usually through views. It interacts with the model and displays the appropriate view to the users.

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

The Router in rails navigates the URL or path to proper controllers. For example, the Router 'users URL' called by external links such as user input or command line, then it will connect to 'users_controller' 'index' method.

## Data structures

```
Data structures
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

#### The differences between Array and Linked list (14.jan.2020)

The Array is a consistent set of a fixed number of data items. And the Linked list is an ordered set comprising a variable number of data items.

The indexes directly or randomly access the Array. But the Linked list is sequentially accessed, traverse starting from the first node in the list by the pointer.

The Array relatively slow at insertion or deletion as shifting is required, but the Linked list is effective, fast and efficient for that.

However, access time in memory of Linked list is slower. Because, While Array elements physically assigned consecutively in the hardware memory during compile time, Linked list elements are stored randomly in hardware during the run time.

The linear search can search them both. But Array can be searched by binary search, while Linked list is not.
