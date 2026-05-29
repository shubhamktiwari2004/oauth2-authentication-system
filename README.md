# OAuth2 Demo Project with Spring Boot and GitHub Login

## Author

**Shubham Tiwari**

---

# Project Overview

This project demonstrates how to implement **OAuth2 Login Authentication** using:

* Java
* Spring Boot
* Spring Security
* OAuth2 Client
* GitHub OAuth App

The application uses GitHub as the OAuth provider and secures all endpoints using Spring Security.

When a user accesses the application:

1. Spring Security redirects the user to GitHub login.
2. User authenticates using GitHub.
3. GitHub redirects back to the Spring Boot application.
4. Spring Security authenticates the user.
5. User can now access secured endpoints.

---

# What This Project Demonstrates

This project helps beginners understand:

* OAuth2 Authentication Flow
* Spring Security OAuth2 Login
* GitHub OAuth App Integration
* Redirect URI Handling
* Callback URL Configuration
* Protected Routes using Spring Security
* Authentication Redirection
* Basic Security Configuration in Spring Boot

---

# Technologies Used

| Technology       | Purpose                          |
| ---------------- | -------------------------------- |
| Java             | Backend Language                 |
| Spring Boot      | Application Framework            |
| Spring Security  | Security & Authentication        |
| OAuth2 Client    | OAuth2 Login Support             |
| GitHub OAuth App | External Authentication Provider |
| Maven            | Dependency Management            |

---

# Project Structure

```text
src/main/java
│
├── Controller
│   └── DemoController.java
│
├── security
│   └── AppSecurity.java
│
└── OAuth2DemoProjectApplication.java

src/main/resources
│
└── application.yml
```

---

# Dependencies Used

Add these dependencies in your `pom.xml`:

```xml
<dependencies>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-oauth2-client</artifactId>
    </dependency>

</dependencies>
```

---

# Security Configuration

```java
package com.shubhamktiwari.OAuth2DemoProject.security;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.Customizer;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.web.SecurityFilterChain;

@EnableWebSecurity
@Configuration
public class AppSecurity {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

        http
                .csrf(csrf -> csrf.disable())
                .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
                .oauth2Login(Customizer.withDefaults());

        return http.build();
    }
}
```

---

# Controller

```java
package com.shubhamktiwari.OAuth2DemoProject.Controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoController {

    @GetMapping("/")
    public String test() {
        return "Hello World";
    }
}
```

---

# Application Configuration

```yaml
spring:
  application:
    name: OAuth2DemoProject

  security:
    oauth2:
      client:
        registration:
          github:
            client-id: YOUR_CLIENT_ID
            client-secret: YOUR_CLIENT_SECRET

server:
  port: 8000
```

---

# Important Security Note

Never push your actual GitHub Client Secret publicly.

Use:

```yaml
client-id: YOUR_CLIENT_ID
client-secret: YOUR_CLIENT_SECRET
```

instead of real credentials.

If credentials are leaked:

1. Open GitHub Developer Settings
2. Regenerate Client Secret
3. Update your application configuration

---

# How OAuth2 Flow Works

## Step 1

User opens:

```text
http://localhost:8000/
```

---

## Step 2

Spring Security detects that authentication is required.

---

## Step 3

Spring redirects user to:

```text
/oauth2/authorization/github
```

---

## Step 4

GitHub login page appears.

---

## Step 5

User logs in using GitHub.

---

## Step 6

GitHub redirects back to:

```text
http://localhost:8000/login/oauth2/code/github
```

---

## Step 7

Spring Security authenticates the user.

---

## Step 8

User gains access to secured endpoints.

---

# Creating GitHub OAuth App

## Step 1: Open GitHub Developer Settings

Open:

[https://github.com/settings/developers](https://github.com/settings/developers)

---

## Step 2: OAuth Apps

Click:

```text
OAuth Apps
```

---

## Step 3: Create New OAuth App

Click:

```text
New OAuth App
```

---

# Fill OAuth App Details

## Application Name

Example:

```text
Spring OAuth2 Demo Project
```

---

## Homepage URL

```text
http://localhost:8000
```

---

## Authorization Callback URL

```text
http://localhost:8000/login/oauth2/code/github
```

IMPORTANT:
This callback URL must match exactly.

---

## Step 4: Register Application

Click:

```text
Register Application
```

---

## Step 5: Generate Client Secret

After app creation:

1. Copy Client ID
2. Generate Client Secret
3. Add both inside `application.yml`

---

# Running the Project

## Step 1

Clone repository:

```bash
git clone <repository-url>
```

---

## Step 2

Open project in IntelliJ IDEA.

---

## Step 3

Configure your GitHub OAuth credentials.

---

## Step 4

Run the application.

---

## Step 5

Open browser:

```text
http://localhost:8000/
```

---

# Expected Output

After successful GitHub login:

```text
Hello World
```

---

# Common Errors

## Redirect URI Error

### Error Message

```text
The redirect_uri is not associated with this application.
```

### Cause

The callback URL configured in GitHub does not match Spring Security callback URL.

### Solution

Use:

```text
http://localhost:8000/login/oauth2/code/github
```

inside GitHub OAuth App settings.

---

## Invalid Client Error

### Cause

Wrong client-id or client-secret.

### Solution

Verify credentials properly.

---

## Port Mismatch

### Cause

GitHub configured with different port.

### Solution

Ensure:

```text
8000
```

matches everywhere.

---

# Learning Outcomes

After completing this project, you will understand:

* How OAuth2 authentication works internally
* Difference between Authentication and Authorization
* Spring Security OAuth2 Login Flow
* Redirect URI and Callback Mechanism
* OAuth2 Client Registration
* Securing APIs with Spring Security
* Integrating third-party login providers

---

# Conclusion

This project provides a beginner-friendly practical implementation of OAuth2 authentication using Spring Boot and GitHub.

It is a strong foundational project for learning:

* Spring Security
* OAuth2
* Authentication flows
* Third-party login integrations
* Secure backend development

---

# License

This project is created for educational and learning purposes.
