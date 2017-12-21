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