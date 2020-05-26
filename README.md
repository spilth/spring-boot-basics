# Spring Boot Basics

A crash course in getting up and running with [Spring Boot](https://spring.io/projects/spring-boot) on macOS.

## Install Homebrew

The first few steps rely on [Homebrew](https://brew.sh/) being installed:

```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

## Install Java

We can now use Homebrew to install [AdoptOpenJDK](https://adoptopenjdk.net/):

```bash
$ brew tap AdoptOpenJDK/openjdk
$ brew cask install adoptopenjdk14
```

## Install jEnv (Optional)

Install [jEnv](https://www.jenv.be/) if you need to manage multiple versions of Java:

```bash
$ brew install jenv
$ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-14.jdk/Contents/Home/
$ jenv global 14.0.1
$ java --version
```

## Install the Spring Boot CLI

The [Spring Boot CLI](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-cli.html) makes it easy to spin up Spring BooT projects using either Maven or Gradle:

```bash
$ brew tap pivotal/tap
$ brew install springboot
```

## Create a Spring Boot Project

You can create and run a simple command-line Spring Boot app with the following:

```bash
$ spring init basics
$ cd basics
$ ./mvnw spring-boot:run
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

Add the following to `src/main/resources/application.properties`:

```
info.app.name=Test Application
info.app.description=An application to test stuff with!
```

Then visit <http://localhost:8080/actuator/info>

## Build and Run a JAR

To create and run a distributable JAR:

```bash
$ ./mvnw package
$ java -jar target/basics-0.0.1-SNAPSHOT.jar
```

Then visit <http://localhost:8080/actuator>

## Build and Run a Docker Image (Optional)

To create and run a [Docker](https://www.docker.com/) image with port forwarding:

```bash
$ ./mvnw spring-boot:build-image
$ docker run -p 8080:8080 docker.io/library/basics:0.0.1-SNAPSHOT
```

Then visit <http://localhost:8080/actuator>

## Deploy to Heroku

To commit your code and run the application on [Heroku](https://www.heroku.com/):

```bash
$ git init
$ git add .
$ git commit -m "First commit"
$ brew tap heroku/brew
$ brew install heroku
$ heroku login
$ heroku create
$ git push heroku master
$ heroku open actuator
```

The last step opens your web app using the hostname provided by Heroku.

## Other Little Things

### Disable the Spring Banner

You can disable the Spring Banner by adding the following entry to `src/main/resources/application.properties`:

```
spring.main.banner-mode=off
```

Then run the app again:

```bash
$ ./mvnw spring-boot:run
```

Yay, no banner!
