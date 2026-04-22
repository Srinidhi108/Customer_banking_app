# CUSTOMER BANKING APP : A FULL JOURNEY 

### LAB 1 : EXECUTING BASIC SPRING BOOT APPLICATION

**Description** : Configuring and adding dependencies to create a simple spring boot project with the help of spring initializer(https://start.spring.io)


<img width="1440" height="819" alt="Screenshot 2026-04-22 at 11 26 55 AM" src="https://github.com/user-attachments/assets/4271fd36-6e53-4045-8fa2-104a55a5cd9f" />

</br> 

After generating(for the first one, I just added *Spring web* dependency:

<img width="758" height="167" alt="Screenshot 2026-04-22 at 11 28 48 AM" src="https://github.com/user-attachments/assets/d916ffcb-9e2d-4c35-b2c7-c367d63e207f" />

</br> 

After opening the project in vscode(Already had maven build tool installed in system). Then in terminal I ran `mvn spring-boot:run`. 
</br>
Running in `localhost:8080` ( TOMCAT runs in port 8080), a **whitelabel error page** is encountered. This is because no `@GetMapping` means no method is used to handle any URL, so all requests fail.

<img width="1440" height="819" alt="Screenshot 2026-04-22 at 11 41 04 AM" src="https://github.com/user-attachments/assets/73838dbb-f8bd-401b-bf46-75b2d0a473a3" />

</br>
Adding a controller class to show an actual message:

```java
/*Class name : Hello.java */


package com.firstproject.myFirstproject;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class Hello {

    @GetMapping("/blah")
        public String hello(){
            return "Hello! I am Srinidhi";
        }
    
}
```

<img width="1440" height="900" alt="Screenshot 2026-04-22 at 11 47 00 AM" src="https://github.com/user-attachments/assets/ebcf4575-5796-4f01-9938-23dd2db7377b" />
</br>
Testing in POSTMAN:

<img width="1266" height="743" alt="Screenshot 2026-04-22 at 11 58 13 AM" src="https://github.com/user-attachments/assets/f8e1821c-49d2-4fd1-bf9a-06ac5d7d4cc8" />













