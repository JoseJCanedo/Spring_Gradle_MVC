# Spring MVC Basics

The MVC in spring MVC stands for Model View Controller and it is a pattern in software design commonly used to implement user interfaces, data, and controlling logic. It emphasizes separation of business logic and the UI display. 

The three parts of the MVC software-design pattern can be described as follows:

- Model: Manages data and business logic.
- View: Handles layout and display.
- Controller: Routes commands to the model and view parts.

Up to this point the configuration we are using for spring and MVC is being imported and handled by the package we added when we created our Spring application using the tool. You can see the import for spring web (mvc) within your build.gradle file or your maven XML imports. 

## Annotations

Before we jump into it a bit more we should cover something quick about annotations since we will be using them. Annotations within spring are denoted with the ```@``` symbol and they allows us to configure dependencies and implement dependency injection through java programs. To this point we have probably used them to denote that a file is a controller or that a class method has a specific HTML method, ie GET, PUT, POST, DELETE. 

You can see a list of spring core annotations [here](https://www.baeldung.com/spring-core-annotations).

## Controllers and Views

The controller as we have learned is where our end points of the application live. In contrast the view would be what is returned to the requester. The view can come from a couple of different file types. Those can either be HTML files, Freemarker, Thymyleaf, or JSP to name a few. These files live within a special directory within spring to make sure the files are only accessible through the application itself. 

## Domains

Within a domains folder in the app we will be keeping our java objects. The objects will be used for the requests and resposnes from the controllers and or database/API requests/responses.

## Service Components

Our controllers should be simple and clean. They should accept the request and all the business logic that goes into processing the said request should happen in the service components. Our service components are broken down into two files:
- a service file which is an interface for the methods contained within the implementation file
- a service impl file which implements the interface

This is done for abstraction and for code readability. With the business logic moved to the service components we can also reuse that logic over different services or controllers. 

Example Services with Controller

~/controller/ExampleController.java
```java
@RestController
public class ExampleController {
   @Autowired
   ExampleService exampleService;

   @RequestMapping(value = "/example")
   public ResponseEntity<Object> getProduct() {
      return new ResponseEntity<>(exampleService.getSomeExample(), HttpStatus.OK);
   }
}
```

~/service/ExampleService.java
```java
public interface ExmapleService {
    public String getSomeExample();
}
```

~/service/impl/ExampleServiceImpl.java
```java
@Service
public interface ExmapleServiceImpl implements ExmapleService {
    @Override
    public String getSomeExample(){
        // Business Logic
    }
}
```

We will be following this structure for our projects.
