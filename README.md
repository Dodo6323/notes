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