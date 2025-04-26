# My Web Application (Maven + Tomcat)

This project demonstrates how to create a simple Java web application using Maven and deploy it to Apache Tomcat.

## Features
- Basic Java Servlet and JSP configuration
- Maven integration for building and packaging the app
- Tomcat plugin for deployment and running the application

## Table of Contents
- [Prerequisites](#prerequisites)
- [Steps to Build the Project](#steps-to-build-the-project)
- [How to Generate the WAR Package](#how-to-generate-the-war-package)
- [Running the Application with Tomcat](#running-the-application-with-tomcat)
- [Accessing the Application](#accessing-the-application)

---

## Prerequisites

Before you begin, ensure you have the following installed:

- **Java 8 or later**  
- **Apache Maven**  
- **Apache Tomcat 7+**  
- **IDE** (e.g., IntelliJ IDEA, Eclipse, or VS Code)

---

## Steps to Build the Project

1. Clone this repository:

   ```bash
   git clone https://github.com/yourusername/mywebapp.git
   cd mywebapp
   ```

2. Open the project in your IDE or any text editor.

3. The project has the following structure:
   ```plaintext
   mywebapp/
   ├── src/
   │   ├── main/
   │   │   ├── java/
   │   │   │   └── com/mywebapp/servlets/HelloServlet.java
   │   │   ├── resources/
   │   │   └── webapp/
   │   │       └── index.jsp
   ├── pom.xml
   ```

---

## How to Generate the WAR Package

Maven helps automate the packaging process of the Java web application. The WAR (Web Application Archive) file is generated using the following command:

1. Run Maven `clean` and `install` commands to build the project and package it into a WAR file:

   ```bash
   mvn clean install
   ```

2. After running the command, the WAR file will be located in the `target/` directory. It will be named something like:

   ```plaintext
   target/myapp.war
   ```

---

## Running the Application with Tomcat

You can run Tomcat directly from Maven using the **Tomcat7 Maven Plugin**. This avoids the need to manually deploy the WAR file to the Tomcat webapps folder.

### 1. Add Tomcat Plugin to `pom.xml`

Make sure your `pom.xml` contains the following Maven plugin configuration for Tomcat:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
                <url>http://localhost:8080/manager/text</url>
                <server>TomcatServer</server>
                <path>/myapp</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

### 2. Configure Tomcat Manager Credentials

For Tomcat to allow the Maven plugin to deploy the WAR file, you need to configure the Tomcat Manager credentials in the `settings.xml` file:

- Locate your `settings.xml` file, which is typically found in the `~/.m2` directory (Linux/macOS) or `C:\Users\<User>\.m2` (Windows).
- Add the following server configuration:

```xml
<servers>
    <server>
        <id>TomcatServer</id>
        <username>admin</username>
        <password>admin</password>
    </server>
</servers>
```

Replace `admin` with your actual Tomcat Manager username and password.

### 3. Start Tomcat from Maven

To start Tomcat and deploy your web app, run the following Maven command:

```bash
mvn tomcat7:run
```

This will:
- Start an embedded Tomcat server.
- Deploy your application to Tomcat.

---

## Accessing the Application

Once the server is up and running, you can access the web application by visiting the following URL in your browser:

```
http://localhost:8080/myapp/hello
```

---

## Troubleshooting

- **HTTP Status 404 - Not Found**: This error typically occurs when the URL or servlet path is incorrect. Ensure that the servlet mappings in your `web.xml` are correct, and that the URL you are trying to access is valid.
- **Cannot find `javax.servlet` classes**: Make sure your `pom.xml` includes the necessary dependencies (see the full `pom.xml` above for reference).

---

## Conclusion

This is a simple example of using Maven to create, build, and deploy a Java web application with Apache Tomcat. Maven handles the build and packaging process, and the Tomcat plugin allows for easy deployment and testing of the web application.

---
