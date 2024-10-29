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


  All of these annotations and ResponseStatusException are imported from the org.springframework.web.bind.annotation package.