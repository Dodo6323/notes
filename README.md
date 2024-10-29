# Poznámky

### Get request - Curl
curl localhost:8080/blabla

### Post request - Curl
curl -X POST -d "{\"name\":\"Charlie\", \"breed\":\"German Shepherd\"}" -H "Content-Type: application/json" localhost:8080/blabla

-X POST povie serveru, že klient robí POST request -X je curl parameter, špecifikuje typ requestu
 
-d (short pre --data) indikuje posielanie nových dáť do existujúcej aplikácie

"{ }" kontent, ktorý chce klient poslať. Syntax: {\"key1\":\"value1\", \"key2\":\"value2\"}

-H "Content-Type: application/json" špecifikuje formát napr. json

Nakoniec URL - povie serveru kde poslať tieto nové dáta


## Start
### 1. start.spring.io

### 2. Folder Structure
#### pom.xml
pom = Project Object Model - xml súbor, ktorý špecifikuje a nahráva dôležité projektové dáta (configuration, build profiles, ...)

#### application.properties - 
src/main/resources - application.properties - špecifikuje vlastnosti Spring aplikácie

#### [ProjectName]Application.java
rc/main/java/com/example/mySpringProject - MySpringProjectApplication.java - main method

### 3. Implement Spring Code
src/main/java/com/example/mySpringProject - HelloController.java

    package com.example.mySpringProject.controller;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class HelloController {

        @GetMapping("/helloworld")
        public String helloWorld() {
            return "Hello World!";
        }
    }

@GetMapping("/helloworld") - anotácia sa spustí vždy keď appka dostane GET request

### 4. Run
mvnw spring-boot:run


## Curl

### -X
Skratka pre --request

curl -X DELETE http:adresa

### -d
Skratka pre --data

curl -X PUT -d "username=Lily" http:adresa

curl -X PUT -d "username=Lily&height=180" http:adresa
(pomocou & sa dajú kombinovať)

curl -X POST -d "username=Lily" http:adresa

curl -d "username=Lily" http:adresa (bez špecifivkovania
automaticky postuje POST request)

### -H
Skratka pre --header

Pridávanie (špecifikovanie) header content-type

curl -d "{ \"username\": \"Lily\" }" -H "Content-Type:
application/json" http:adresa

### -i
Skratka pre --include

Printuje response header

$ curl -i http:adresa

HTTP/2 200

date: ...

content-type: ...

## Mapping Requests

**@RestController** sa používa na deklarovanie triedy ako kontroléra,
ktorý môže poskytovať typy údajov špecifické
pre aplikáciu ako súčasť odpovede HTTP.

**@RequestMapping** sa používa na prepojenie typov požiadaviek
a koncových bodov
so špecifickými metódami triedy.

**@RestController** by sa mala pridať do každej triedy,
ktorá bude spracovávať odpovede na požiadavky HTTP.
@RestController kombinuje funkčnosť
dvoch samostatných anotácií, **@Controller** a **@ResponseBody**.

**@Controller** sa používa na to, aby bola trieda identifikovateľná
pre Spring ako súčasť webovej aplikácie.

**@ResponseBody** povie Springu, aby skonvertoval
návratové hodnoty metód ovládača na JSON a naviazala
tento JSON na telo odpovede HTTP. Keďže takmer každý hlavný
programovací jazyk ponúka nejaký typ podpory JSON (JavaScript
Object Notation), môžeme jednoducho vziať objekt vytvorený v
Spring a preložiť ho do
JSON, ktorý sa dá ľahko analyzovať v HTML a zobraziť na stránke.

**@RequestMapping** akceptuje niekoľko argumentov.
Prvým a najdôležitejším je cesta. Argument
cesta sa používa na určenie, kde sú mapované požiadavky.
Napríklad, ak používateľ požiada o získanie zdroja „knihy“,
server odošle požiadavku metóde s anotáciou
@RequestMapping(cesta = „/kniha“) a táto metóda poskytne odpoveď.

**@RequestMapping** tiež akceptuje niekoľko ďalších
argumentov vrátane **method**,
**params** a **consumes**

**method**: umožňuje vývojárovi určiť, ktorá metóda HTTP by
sa mala použiť pri prístupe k metóde ovládača. Najbežnejšie
sú RequestMethod.GET, ...POST, ...PUT a ...DELETE. Keďže ide o
voliteľný argument,
ak nešpecifikujeme metódu HTTP, predvolene sa použije GET.

**params**: filtruje požiadavky na základe daných parametrov.

**consums**: používa sa na určenie, ktorý typ média sa môže
spotrebovať – niektoré bežné typy médií sú „text/plain“,
„application/JSON“ atď.

    @Controller
    public class VirtualLibrary{

    @RequestMapping("/books/all", RequestMethod.GET)
    public Book getAllBooks() {
        return getBook();
        }

    }

## HTTP Method Annotation	Usage

    @GetMapping	Used to specify GET requests to retrieve resources
    @PostMapping	Used to specify POST requests to create new resources
    @PutMapping	Used to specify PUT requests to update existing resources
    @DeleteMapping	Used to specify DELETE requests to remove specific resources



- Map HTTP requests to controllers and
Preview: Docs Methods are reusable pieces of code in classes. The difference between a method and a function is that methods are always related to a class or an object.
methods
(**@RestController** and **@RequestMapping**)
- Specify a path attribute to become a base path
(**@RequestMapping** at the class level)
- Declare request types using HTTP method annotations
(**@GetMapping**, **@PostMapping**, **@PutMapping**, and **@DeleteMapping**)
- Access request parameters in a method (**@RequestParam**)
- Bind data using template (**@PathVariable**)
- Fine-tune the status code returned by a method (**@ResponseStatus**)


  All of these annotations and ResponseStatusException are
  imported from the org.springframework.web.bind.annotation package.
  
## Beans

### @Component

    @Component
    public class RaceTrack {
        private String location;
        private int miles;
        private String trackType;
    }
    
    @Component
    public class Driver {
        private String name;
        private String team;
        private int yearsExperience;
    }

### @Autowired

    public class RaceRound {
        private String startTime;
        @Autowired
        private RaceTrack currentRaceTrack;
        @Autowired
        private Driver currentDriver;
    }

The fully-automatic annotations approach is facilitated using three annotations:

- **@Configuration**, which notifies the framework that beans may be created via the annotated class.
- **@ComponentScan**, which tells the framework to scan our code for components such as classes, controllers, services, etc.
- **@EnableAutoConfiguration**, which tells the container to auto-create beans from the found components.

The **@SpringBootApplication** annotation is a compilation
of **@Configuration**, **@ComponentScan**, and **@EnableAutoConfiguration**.
When we apply the **@SpringBootApplication** annotation to the class
containing our main method, our application runs with all of this
built-in functionality. Therefore, when our application starts up
the container scans
our code for components from which beans should be instantiated.

    @SpringBootApplication
    public class RecipeApplication {
    
        public static void main(String[] args) {
            SpringApplication.run(RecipeApplication.class, args);
        }
    }

## Spring Boot

### @SpringBootApplication
The **@SpringBootApplication** annotation is equivalent to
**@Configuration**, **@ComponentScan**, and **@EnableAutoConfiguration**. 
The first two are from the Spring framework, but the third, 
**@EnableAutoConfiguration**, is from Spring Boot.

This annotation enables Spring Boot to review our dependencies 
(such as spring-boot-starter-jpa and h2) and assume the intended 
purpose of the application. It will configure and run the application
to best fit the assumed purpose.

When we start our application with ./mvnw spring-boot:run, 
Spring Boot does some tasks by default: it makes some assumptions, 
like using port 8080, but it also checks for additional 
configuration instructions in the application.properties file. 
This allows us to make high-level changes to our application 
without writing any Java code.

For example, you can override the default 8080 port using:

    server.port=4000

You can disable JPA warnings:

    spring.jpa.open-in-view=false

Or customize the level of logging in your application:

    logging.level.org.springframework=DEBUG

In the case of the downloadable application we provided, the application.properties file customizes the database behavior,
such as the local file to use for storage:

    spring.datasource.url=jdbc:h2:file:~/springcap

## CRUD (Create, Read, Update, Delete)

### Create

To create resources in a REST environment, we most commonly
use the HTTP POST method. POST creates a new resource of the
specified resource type.

For example, let’s imagine that we are adding a new food item
to the stored list of dishes for this restaurant, and the dish
objects are stored in a dishes resource. If we wanted 
create the new item, we would use a POST request:

Request:

    POST http://www.myrestaurant.com/dishes/

Body -

    {
        "dish": {
            "name": "Avocado Toast",
            "price": 8
        }
    }

This creates a new item with a name value of "Avocado Toast"
and a price value of 8. Upon successful creation, the server should
return a header with a link to the newly-created resource, along
with a HTTP response code of 201 (CREATED).

Response:

Status Code - 201 (CREATED)

Body -

    {
        "dish": {
            "id": 1223,
            "name": "Avocado Toast",
            "price": 8
        }
    }

From this response, we see that the dish with name
“Avocado Toast” and price 8 has been successfully
created and added to the dishes resource.

### Read

To read resources in a REST environment, we use the GET method.
Reading a resource should never change any information — it should
only retrieve it. If you call GET on the same information 10 times
in a row, you should get the same response on the first call that
you get on the last call.

GET can be used to read an entire list of items:

Request:

    GET http://www.myrestaurant.com/dishes/

Response: Status Code - 200 (OK)

Body -

    {
        "dishes": [
            {
                "id": 1,
                "name": "Spring Rolls",
                "price": 6
            },
            {
                "id": 2,
                "name": "Mozzarella Sticks",
                "price": 7
            },
                ...
            {
                "id": 1223,
                "name": "Avocado Toast",
                "price": 8
            },
            {
                "id": 1224,
                "name": "Muesli and Yogurt",
                "price": 5
            }
        ]
    }

GET requests can also be used to read a specific item, when
its id is specified in the request:

Request:

    GET http://www.myrestaurant.com/dishes/1223

Response: Status Code - 200 (OK)

Body -

    {
        "id": 1223,
        "name": "Avocado Toast",
        "price": 8
    }

After this request, no information has been changed
in the database. The item with id 1223 has been retrieved
from the dishes resource, and not modified. When there are
no errors, GET will return the HTML or JSON of the desired
resource, along with a 200 (OK) response code. If there is an
error, it most often will return a 404
(NOT FOUND) response code.

### Update

PUT is the HTTP method used for the CRUD operation, Update.

For example, if the price of Avocado Toast has gone up, we should
go into the database and update that information. We can do
this with a PUT request.

Request:

    PUT http://www.myrestaurant.com/dishes/1223

Body -

    {
        "dish": {
            "name": "Avocado Toast",
            "price": 10
        }
    }

This request should change the item with id 1223 to have the attributes supplied in the request body. This dish with id 1223 should now still have the name “Avocado Toast”, but the price value should now be 10, whereas before it was 8.

Response: Status Code - 200 (OK)

Body -

    {
        "dish": {
            "name": "Avocado Toast",
            "price": 10
        }
    }

The response includes a Status Code of 200 (OK) to signify that the operation was successful. Optionally, the response could use a Status Code of 204 (NO CONTENT) and not include a response body. This decision depends on the context.

### Delete

The CRUD operation Delete corresponds to the HTTP method DELETE. It is used to remove a resource from the system.

Let’s say that the world avocado shortage has reached a critical point, and we can no longer afford to serve this modern delicacy at all. We should go into the database and delete the item that corresponds to “Avocado Toast”, which we know has an id of 1223.

Request:

    DELETE http://www.myrestaurant.com/dishes/1223

Such a call, if successful, returns a response code of 204 (NO CONTENT), with no response body. The dishes resource should no longer contain the dish object with id 1223.

Response: Status Code - 204 (NO CONTENT)

Body - None

Calling GET on the dishes resource after this DELETE call would return the original list of dishes with the {"id": 1223, "name": "Avocado Toast", "price": 10} entry removed. All other dish objects in the dishes resource should remain unchanged. If we tried to call a GET on the item with id 1223, which we just deleted, we would receive a 404 (NOT FOUND) response code and the state of the system should remain unchanged.

Calling DELETE on a resource that does not exist should not change the state of the system. The call should return a 404 response code (NOT FOUND) and do nothing.

    1. Create
    
    Route: POST /classes
    
    Effect on Database: Adds the class provided in the request body to the database
    
    Response Body: { "class": The Newly-Created Class }
    
    Success Response Code: 201
    
    2. Read (All Classes)
    
    Route: GET /classes
    
    Effect on Database: None
    
    Response Body: { "classes": [ Array of All Saved Classess ] }
    
    Success Response Code: 200

    3. Read (One Class)
    
    Route: GET /classes/:id
    
    Effect on Database: None
    
    Response Body: { "class": The class with the specified ID }
    
    Success Response Code: 200
    
    4. Update
    
    Route: PUT /classes/:id
    
    Effect on Database: Updates the class with the specified ID to have the class information provided in the request body
    
    Response Body: { "class": The updated class now saved in the database }
    
    Success Response Code: 200
    
    5. Delete
    
    Route: DELETE /classes/:id
    
    Effect on Database: Removes the class with the specified ID from the database
    
    Response Body: None
    
    Success Response Code: 204

## Model

- **@Entity**: tells the ORM that this model will be used to represent a table or relation in our database
- **@Table**: tells the ORM what table name in the underlying database that this model corresponds to. Here, it is used to say that the Person entity represents a single entry in the "PEOPLE" table of the underlying database.
- **@Id**: tells the ORM that this field (id) will be used to uniquely identify a single entry in our "PEOPLE" relation
- **@GeneratedValue**: tells the ORM that the developer will not be supplying the value for this field themselves. Instead, it should be “auto-generated” by the database. Typically, an @Id field for an entity will be auto-generated in this way, so that we can leverage the database to guarantee that the ID will always be unique.
- **@Column**: tells the ORM what column in the underlying relation that the annotated field corresponds to. For example, the eyeColor field of our entity corresponds to the "EYE_COLOR" column in the "PEOPLE" relation.

## Repository

- **.findById(Integer id)**: allows you to query the database to find an instance of your model by its ID field
- **.findAll()**: allows you to retrieve ALL the entries in the database for a given model
- **.save(Person p)**: allows you to create AND modify instances of your model in the database
- **.delete(Person p)**: allows you to delete instances of your model from the database


    public interface PlantRepository extends CrudRepository<Plant, Integer> {

    }

- Create plants in the database by making POST requests and the .save method of CrudRepository
- Read plants in the database by making GET requests and the .findAll() and .findById()
- Preview: Docs Methods are reusable pieces of code in classes. The difference between a method and a function is that methods are always related to a class or an object.
methods
of CrudRepository
- Update plants in the database by using getters and setters to check and modify fields in the Plant entity, and the .save method of CrudRepository
- Delete plants in the database by using the .delete method of the CrudRepository.