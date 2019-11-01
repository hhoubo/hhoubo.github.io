---
layout: single
title:  "Swagger definitions"
date:   2019-11-01 16:38:23 +0900
categories: serverless
tags: cloud serverless
---
## Basic Structure
- Metadata
- Base URL
    1. schemes
    2. host
    3. basePath
-Consumes, Produces
  Example: `- application/json`
- Path
```yaml
paths:
  /users:
    get:
      summary: Returns a list of users.
      description: Optional extended description in Markdown.
      produces:
        - application/json
      responses:
        200:
          description: OK
```
- Parameters
- Responses
- Input and Output Models
JSON:
```json
{
  "id": 4,
  "name": "Arthur Dent"
}
```
Model definition:
```yaml
definitions:
  User:
    properties:
      id:
        type: integer
      name:
        type: string
    # Both properties are required
    required:  
      - id
      - name
```
Ref:
```yaml
paths:
  /users/{userId}:
    get:
      summary: Returns a user by ID.
      parameters:
        - in: path
          name: userId
          required: true
          type: integer
      responses:
        200:
          description: OK
          schema:
            $ref: '#/definitions/User'
  /users:
    post:
      summary: Creates a new user.
      parameters:
        - in: body
          name: user
          schema:
            $ref: '#/definitions/User'
      responses:
        200:
          description: OK
```
- Authentication
## Other specs
### Query String in Paths
WRONG example:
```
GET /users?firstName=value&lastName=value
GET /users?role=value
```
This is because Swagger considers a unique operation as a combination of a path and the HTTP method, and additional parameters do not make the operation unique. Instead, you should use unique paths such as:
```
GET /users/findByName?firstName=value&lastName=value
GET /users/findByRole?role=value
```
### Describing Request Body
There can be only one body parameter, although the operation may have other parameters (path, query, header).
> Note: The payload of the application/x-www-form-urlencoded and multipart/form-data requests is described by using form parameters, not body parameters.

## Open API extention for `ESP` and `Service Control`


## Reference
1. [Swagger OPenAPI Specification](https://swagger.io/docs/specification/2-0/basic-structure/)
