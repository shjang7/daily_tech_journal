# daily_tech_journal
### An introduction about Rails 6 framework

This writing is to introduce Rails framework which is a server-side web app framework to a person new to and inexperienced in Rails.

```
source /
├─ app
│  ├─ controllers
│  ├─ models
│  └─ views
├─ config
│  └─ routes
└─ db
   └─ migrate
```

##### MVC (13.jan.2020)

Rails has a model-view-controller (MVC) design pattern. It presents default structures for a database, a web service, and web pages. I am going to talk about this today.

The model contains data for application and often linked to a database. And it has an order which can be used for business purpose. And it does not know user interface; it means it can be reused.

The view generates the user interface, which presents data to the users. Many views can access the same model for different reasons. Once the view created, the data is displayed to the users.

The controller receives events from the outside world, usually through views. It interacts with the model and displays the appropriate view to the users.
