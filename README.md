# Spring Boot Basics

## Getting Started

```bash
$ brew tap pivotal/tap
$ brew install springboot
$ brew install jenv
$ brew cask install adoptopenjdk14
$ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-14.jdk/Contents/Home/
$ jenv global 14.0.1
$ java --version
```

## Creating Your First Project

Create and run a simple command-line app with the following:

```bash
$ /usr/local/bin/spring init basics
$ cd basics
$ ./mvnw spring-boot:run
```

## Disable the Spring Banner

Add the following to `src/main/resource/application.properties`:

```
spring.main.banner-mode=off
```

Then run the app again:

```bash
$ ./mvnw spring-boot:run
```

No banner!

## Build and Run a JAR

To create and run a distributable JAR:

```bash
$ ./mvnw package
$ java -jar target/basics-0.0.1-SNAPSHOT.jar
```

## Make it a Web Application

Add the following dependency to your `pom.xml`:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Now run your application:

```bash
$ ./mvnw spring-boot:run
```

Then visit <http://localhost:8080>. You should see an error page. That's fine!

## Add the Spring Boot Actuator

Add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Now run your application:

```bash
$ ./mvnw spring-boot:run
```

Then visit <http://localhost:8080/actuator>, <http://localhost:8080/actuator/health> and <http://localhost:8080/actuator/info>

## Customize the Actuator Info Endpoint

Add the following to `src/main/resource/application.properties`:

```
info.app.name=Test Application
info.app.description=An application to test stuff with!
```

Then visit <http://localhost:8080/actuator/info>

## Build and Run a Docker Image

```bash
$ ./mvnw spring-boot:build-image
$ docker run -p 8080:8080 docker.io/library/basics:0.0.1-SNAPSHOT
```

Then visit <http://localhost:8080/actuator>
