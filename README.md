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
    * Returns a list of actor objects, total number of actors, and reports success as true
* Sample: curl -X GET -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/actors
```
{
    "success": True,
    "actors": [
        {
            "id": 1,
            "name": "miso",
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
    * Returns a specific actor if they exist and reports success as true
    * Returns error and message for HTTP response status code 404 if not found
* Sample: curl -X GET -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/actors/1
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
    * Deletes a specific actor if they exist and reports success as true
    * Returns error and message for HTTP response status code 422 if not found
* Sample: curl -X DELETE -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/actors/1
```
{
    "success": True,
    "deleted": 1
}
```

#### POST /actors
* General:
    * Creates a new actor and reports success as true
    * Returns error and message for HTTP response status code 400 if "name", "age", or "gender" not found in the submitted data
    * Returns error and message for HTTP response status code 422 if "name" is not a string, "age" is not an integer, or "gender" is not a string
* Sample: curl -X POST -H "Content-Type: application/json" -d '{"name": "chance", "age": 3, "gender": "none of your business"}' -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/actors
```
{
    "success": True,
    "actor": {
        "id": 3,
        "name": "chance",
        "age": 3,
        "gender": "none of your business"
    }
}
```

#### PATCH /actors/<actor_id>
* General:
    * Updates an actor and reports success as true
    * Returns error and message for HTTP response status code 422 if "name" is not a string, "age" is not an integer, or "gender" is not a string
* Sample: curl -X PATCH -H "Content-Type: application/json" -d '{"name": "honey", "gender": "who cares"}' -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/actors/1
```
{
    "success": True,
    "actor": {
        "id": 1,
        "name": "honey",
        "age": 5,
        "gender": "who cares"
    }
}
```

#### GET /movies
* General:
    * Returns a list of movies objects, total number of movies, and reports success as true
* Sample: curl -X GET -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/movies
```
{
    "success": True,
    "actors": [
        {
            "id": 1,
            "title": "miso is a good cate",
            "release_date": "2018-08-10"
        },
        {
            "id": 2,
            "title": "mister is a bad dog",
            "release_date": "2020-06-30"
        }
    ],
    "num_movies": 2
}
```

#### GET /movies/<movie_id>
* General:
    * Returns a specific movie if it exists and reports success as true
    * Returns error and message for HTTP response status code 404 if not found
* Sample: curl -X GET -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/movies/1
```
{
    "success": True,
    "actor": {
        "id": 1,
        "title": "miso is a good cate",
        "release_date": "2018-08-10"
    }
}
```

#### DELETE /movies/<movie_id>
* General:
    * Deletes a specific movie if it exists and reports success as true
    * Returns error and message for HTTP response status code 422 if not found
* Sample: curl -X DELETE -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/movies/1
```
{
    "success": True,
    "deleted": 1
}
```

#### POST /movies
* General:
    * Creates a new movie and reports success as true
    * Returns error and message for HTTP response status code 400 if "title or "release_date" not found in the submitted data
    * Returns error and message for HTTP response status code 422 if "title" is not a string or "release_date" is not of the type "YYYY-MM-DD"
* Sample: curl -X POST -H "Content-Type: application/json" -d '{"title": "chance is also a good dog", "release_date": "2020-07-05"}' -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/movies
```
{
    "success": True,
    "actor": {
        "id": 3,
        "title": "chance is also a good dog",
        "release_date": "2020-07-05"
    }
}
```

#### PATCH /movies/<movie_id>
* General:
    * Updates an movie and reports success as true
    * Returns error and message for HTTP response status code 422 if "title" is not a string or "release_date" is not of the type "YYYY-MM-DD"
* Sample: curl -X PATCH -H "Content-Type: application/json" -d '{"title": "mister is actually a good dog"}' -H "Authorization: Bearer \<token\>" https://full-stack-capstone-project-jacob-brown.onrender.com/movies/1
```
{
    "success": True,
    "actor": {
        "id": 1,
        "name": "mister is actually a good dog",
        "release_date": "2020-06-30"
    }
}
```