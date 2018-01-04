# Ocomis Docs

## Environments

### Overview

All microservices must support the following environments:

1) `development`: Local development including local unit tests
2) `integration`: Isolated testing of a microservice, initiated by the CI Sever; the term "integration" refers to the integration of the code changes by multiple devleopers
3) `testing`: Human and automated testing of the whole system consisting of multiple microservices.
4) `staging`: Final testing of the whole system consisting of multiple microservices before releasing it to production
5) `production`: Live software used by the end users

## API Service Errors

API Services must use the respective HTTP Error codes.

API Services must return an JSON response in case of errors. These error responses must include at least one attribute `message` (string).

Example:

```json
{
    "message": "The user was not found."
}
````

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
