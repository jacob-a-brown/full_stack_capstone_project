# Capstone Project
This is the capstone project for Udacity's full stack web developer course.

## Getting Started
### Prerequisits and Installation
* SQLAlchemy and Flask are used for the backend
* Python 3.9.x is used
* Auth0 and JWTs are used for authentication and role-based access control

## API References

### Getting Started
* Based URL: This app can be run locally or accessed through Render at 
    https://full-stack-capstone-project-jacob-brown.onrender.com
* Authentication: JWTs, roles, and permissions are handled via Auth0

### Error Handling
Errors are returned as JSON objects with the following formats:
```
{
    "success": False,
    "error": <status code>,
    "message": <error message>
}
```
The API will return 6 error types when requests fail:
* 400: bad request
    * this could also happen if permissions are not included in the payload
* 401: a variety of authorization errors
    * authorization header expected
    * autherization of type Bearer expected
    * bearer token expected
    * authorization malformed
    * token expired
    * incorrect claims
* 403: incorrect permissions
* 404: resource not found
* 405: method not allowed
* 422: cannot process
* 500: internal server error

### Endpoints

#### GET /am_i_healthy
* General:
    * Used to determine if application is hosted and running
* Sample: curl https://full-stack-capstone-project-jacob-brown.onrender.com/am_i_healthy
```
You are healthy
```
#### GET /actors
* General:
    * Returns a list of actor objects, success value, and total number of actors
* Sample: curl https://full-stack-capstone-project-jacob-brown.onrender.com/actors
```
{
    "success": True,
    "actors": [
        {
            "id": 1,
            "name": miso,
            "age": 5,
            "gender": "none of your business"
        },
        {
            "id": 2,
            "name": "mister",
            "age": 3,
            "gender": "none of your business"
        }
    ],
    "num_actors": 2
}
```

#### GET /actors/<actor_id>
* General:
    * Returns a specific actor if they exist
    * Returns error and message for HTTP response status code 404 if not found
* Sample: curl -X GET -H "Authorization: Bearer <token>" https://full-stack-capstone-project-jacob-brown.onrender.com/actors/1
```
{
    "success": True,
    "actor": {
        "id": 1,
        "name": "miso",
        "age": 5,
        "gender": "none of your business"
    }
}
```

#### DELETE /actors/<actor_id>
* General:
    * Deletes a specific actor if they exist
    * Returns error and message for HTTP response status code 422 if not found
* Sample: curl -X DELETE https://full-stack-capstone-project-jacob-brown.onrender.com/actors/1
```
{
    "success": True,
    "deleted": 1
}
```

#### POST /actors
* General:
    * Creates a new actor
    * Returns error and message for HTTP response status code 400 if "name", "age", or "gender" not found in the submitted data
    * Returns error and message for HTTP response status code 422 if "name" is not a string, "age" is not an integer, or "gender" is not a string
* Sample: curl -X POST -d 

#### PATCH /actors/<actor_id>

#### GET /movies

#### GET /movies/<movie_id>

#### DELETE /movies/<movie_id>

#### POST /movies

#### PATCH /movies/<movie_id>