
# Spring Boot tutorial 

based on [Official Guide]


[Install JDK]

`Make tutorial guide to install JDK 1.8`

[Install Gradle]

```bash
# Download Gradle binary-only
wget https://services.gradle.org/distributions/gradle-5.0-bin.zip

# Unpack the distribution
sudo mkdir /opt/gradle
unzip -d /opt/gradle gradle-5.0-bin.zip

# Configure your system environment
export PATH=$PATH:/opt/gradle/gradle-5.0/bin

# Verify your installation
gradle -v
```

Make prokect diretory

```bash
mkdir -p src/main/java/hello
```

Criate file gradle settings (example with sublime text editor)

```bash
subl build.gradle
```

Add content

```gradle
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:2.0.5.RELEASE")
    }
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'org.springframework.boot'
apply plugin: 'io.spring.dependency-management'

bootJar {
    baseName = 'gs-spring-boot'
    version =  '0.1.0'
}

repositories {
    mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile("org.springframework.boot:spring-boot-starter-web")
    testCompile("junit:junit")
}
```

Criate class HelloController (example with sublime text editor)

```bash
subl src/main/java/hello/HelloController.java
```

Add content

```java
package hello;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;

@RestController
public class HelloController {

    @RequestMapping("/")
    public String index() {
        return "Greetings from Spring Boot!\n";
    }

}
```

Criate class Application (example with sublime text editor)

```bash
subl src/main/java/hello/Application.java
```

Add content

```java
package hello;

import java.util.Arrays;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

    @Bean
    public CommandLineRunner commandLineRunner(ApplicationContext ctx) {
        return args -> {

            System.out.println("Let's inspect the beans provided by Spring Boot:");

            String[] beanNames = ctx.getBeanDefinitionNames();
            Arrays.sort(beanNames);
            for (String beanName : beanNames) {
                System.out.println(beanName);
            }

        };
    }

}
```

Run Gradle build

```bash
gradlew build && java -jar build/libs/gs-spring-boot-0.1.0.jar
```

Wait to build the project..

Run:

```bash
curl localhost:8080
```

See result


> Greetings from Spring Boot!



[Install Gradle]: <https://gradle.org/install/>
[Official Guide]: <https://spring.io/guides/gs/spring-boot/>