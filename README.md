# Ocomis Docs

## API Service Errors

API Services must use the respective HTTP Error codes.

API Services must return an JSON response in case of errors. These error responses must include at least one attribute `message` (string).

Example:

```json
{
    "message": "The user was not found."
}
````

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
