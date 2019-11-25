# Background
This project has been built using the awesome tutorial available here: 
https://auth0.com/blog/implementing-jwt-authentication-on-spring-boot/

# How To Setup The Application And Run It
* Make sure you have gradle installed on your system and an IDE. If 
you don't have an IDE don't worry you can still follow with a text editor and 
the terminal.
* Make sure you have Java 10 installed on your system. [Get it here](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)
* Run `gradle bootrun` to build and run the project or run the project from your ide(make sure you build it before running)

# Testing your project

- issues a GET request to retrieve tasks with no JWT
- HTTP 403 Forbidden status is expected
```console
curl http://localhost:8080/tasks
```

- registers a new user
```console
curl -H "Content-Type: application/json" -X POST -d '{
    "username": "admin",
    "password": "password"
}' http://localhost:8080/users/sign-up

- logs into the application (JWT is generated)
curl -i -H "Content-Type: application/json" -X POST -d '{
    "username": "admin",
    "password": "password"
}' http://localhost:8080/login
```

- issue a POST request, passing the JWT, to create a task
- remember to replace xxx.yyy.zzz with the JWT retrieved above

```console
curl -H "Content-Type: application/json" -H "Authorization: Bearer xxx.yyy.zzz" \
-X POST -d '{
    "description": "Buy watermelon"
}'  http://localhost:8080/tasks
```

- issue a new GET request, passing the JWT
- remember to replace xxx.yyy.zzz with the JWT retrieved above
```console
curl -H "Authorization: Bearer xxx.yyy.zzz" http://localhost:8080/tasks 
```