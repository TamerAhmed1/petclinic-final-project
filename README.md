
## Understanding the Spring Petclinic application with a few diagrams


## Running petclinic locally
Petclinic is a [Spring Boot](https://spring.io/guides/gs/spring-boot) application built using [Maven](https://spring.io/guides/gs/maven/). You can build a jar file and run it from the command line:


```
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic
./mvnw package
java -jar target/*.jar
```

You can then access petclinic here: http://localhost:8080/

<img width="1042" alt="petclinic-screenshot" src="https://cloud.githubusercontent.com/assets/838318/19727082/2aee6d6c-9b8e-11e6-81fe-e889a5ddfded.png">

Or you can run it from Maven directly using the Spring Boot Maven plugin. If you do this it will pick up changes that you make in the project immediately (changes to Java source files require a compile as well - most people use an IDE for this):

```
./mvnw spring-boot:run
```

## In case you find a bug/suggested improvement for Spring Petclinic
Our issue tracker is available here: https://github.com/spring-projects/spring-petclinic/issues
## Running Petclinic using Docker

Inside the Dockerfile, create the last line as:

ENTRYPOINT [ "sh", "-c", "java -Dspring.profiles.active=${ENV} -Djava.security.egd=file:/dev/./urandom -jar /app.jar" ]

Create a docker image and push it to the Docker Hub

And while running the docker:

```
docker run --env ENV=mysql -d -p 8080:8080 <image id> 
```
This way, environment variable gets local as value and passes to Dockerfile when we bring up a container.

You can also pass on the Spring Profile as an environment variable at the run time as:

```
$ docker run -e "SPRING_PROFILES_ACTIVE=prod" -p 8080:8080 -t ibuchh/spring-petclinic
