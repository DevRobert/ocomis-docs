# Ocomis Docs

## Environments

### Overview

All microservices must support the following environments:

1) `development`: Local development of one miroservice including local unit tests for the microservice
2) `integration`: Isolated testing of one microservice, initiated by the CI Sever; the term "integration" refers to the integration of code changes by multiple developers
3) `testing`: Human and automated testing of the whole system consisting of multiple microservices; the focus lies on deployed environments for testers but it can also be used for a local deployment of the whole system on the developer machine
4) `staging`: Final testing of the whole system consisting of multiple microservices before releasing it to production
5) `production`: Live software used by the end users

### Database

* Docker container/ connect from docker host
    * `development`
    * `integration`
* Docker container/ inside docker compose
    * `testing`
* Managed service
    * `staging`
    * `production`

### Logging

* None
    * `integration`
* Docker compose ELK/ connect from docker host; or none
    * `development`
* Docker compose ELK/ inside docker compose
    * `testing`
* Managed service
    * `staging`
    * `production`



## API Service Errors

API Services must use the respective HTTP Error codes.

API Services must return an JSON response in case of errors. These error responses must include at least one attribute `message` (string).

Example:

```json
{
    "message": "The user was not found."
}
````

### Status Codes

* **200** OK: default
* **201** Created: The resource has been created
* **400** Bad request: The command was not executed due to validation rules.
* **401** Not authorized: The user has not authenticated (no or expired JWT token)
* **403** Forbidden: The user has authenticated but he or she has not the required permissions to proceed
* **404** Not found: The resource was not found
* **500** Internal Server Error: Error at server side
## Health Checks

Todo

## Recommended NPM Packages

### Testing and Quality Assurance

* lab (test runner)
* code (assertions)
* eslint (style checks)

### Webserver/ Application

* hapi (HTTP server)
* react (view)
* redux (state management)

### Deployment

* babel (transpiling)
* webpack (bundle sources for deployment)

### Miscellaneous

* pino (logging)

## Authentication

The `user` service is responsible for storing users.

The `authentication` service is responsible for issueing JSON Web Tokens (JWTs). It uses the `user` service to validate the credentials before issueing the token that identifies the user.

### Authentication between a user and a service

All services must accept JWTs from the `authentication` service to identify the requesting user. The integrity of the JWTs is verified using the public key of the `authentication` service.

### Authentication between services

If two services communicate with each other, they basically forward the JWT token they have received from the user who has initiated the request.

If the requesting user has not been authenticated (anonymous) or the request has not been initiated by any user (e.g. data replication jobs), the calling microservice has to pass a token that identifies the service itself but not the user.

Therefore, for each service a user account has to be created. The service has to obtain a JWT from the authentication service to pass it to the service it likes to request.

## Architecture principles

1) All microservices are responsible for persisting their own data.
2) One microservice may call another microservice in order to serve a user request. The called microservice must not call another one in the same request cycle. A good design of service boundaries and data duplication may support this principle.