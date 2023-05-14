# REST API

- `Representational State Transfer (REST)` is an architectural style that defines a set of constraints to be used for creating web services. `REST API` is a way of accessing web services in a simple and flexible way without having any processing.

- REST technology is generally preferred to the more robust Simple Object Access Protocol (SOAP) technology because REST uses less bandwidth, simple and flexible making it more suitable for internet usage. It’s used to fetch or give some information from a web service. All communication done via REST API uses only HTTP request. 

- `Working`: A request is sent from client to server in the form of a web URL as `HTTP GET` or `POST` or `PUT` or `DELETE` request. After that, a response comes back from the server in the form of a resource which can be anything like `HTML`, `XML`, `Image`, or `JSON`. But now `JSON` is the most popular format being used in Web Services. 

- In `HTTP` there are five methods that are commonly used in a `REST-based Architecture` i.e., `POST`, `GET`, `PUT`, `PATCH`, and `DELETE`. These correspond to create, read, update, and delete (or `CRUD`) operations respectively. There are other methods which are less frequently used like `OPTIONS` and `HEAD`.  
  - `GET`: The `HTTP GET` method is used to read (or retrieve) a representation of a resource. In the safe path, `GET` returns a representation in `XML` or `JSON` and an `HTTP` response code of `200 (OK)`. In an error case, it most often returns a `404 (NOT FOUND)` or `400 (BAD REQUEST)`. 
  - `POST`: The `POST` verb is most often utilized to create new resources. In particular, it’s used to create subordinate resources. That is, subordinate to some other (e.g. parent) resource. On successful creation, return `HTTP status 201`, returning a Location header with a link to the newly-created resource with the `201 HTTP status`. 
  ```
      NOTE: POST is neither safe nor idempotent. 
  ```
  - `PUT`: It is used for updating the capabilities. However, `PUT` can also be used to create a resource in the case where the resource ID is chosen by the client instead of by the server. In other words, if the `PUT` is to a `URI` that contains the value of a non-existent resource ID. On successful update, return 200 (or 204 if not returning any content in the body) from a `PUT`. If using `PUT` for create, return `HTTP status 201` on successful creation. 
  ```
      PUT is not safe operation but it’s idempotent. 
  ```
  - `PATCH`: It is used to modify capabilities. The `PATCH` request only needs to contain the changes to the resource, not the complete resource. This resembles `PUT`, but the body contains a set of instructions describing how a resource currently residing on the server should be modified to produce a new version. This means that the `PATCH` body should not just be a modified part of the resource, but in some kind of patch language like `JSON Patch` or `XML Patch`. 
  ```
      PATCH is neither safe nor idempotent. 
  ```
  - `DELETE`: It is used to delete a resource identified by a `URI`. On successful deletion, return `HTTP status 200 (OK)` along with a response body. 
- `Idempotence`: An idempotent `HTTP` method is a `HTTP` method that can be called many times without different outcomes. It would not matter if the method is called only once, or ten times over. The result should be the same. Again, this only applies to the result, not the resource itself. 

- **Example:**
```
    1. a = 4 // It is Idempotence, as final value(a = 4)
             // would not change after executing it multiple
             // times.

    2. a++  // It is not Idempotence because the final value
            // will depend upon the number of times the
            // statement is executed.
```

## Request and Response
- Now we will see how request and response work for different HTTP methods. Let’s assume we have an API(https://www.geeksforgeeks.org/api/students) for all students data of gfg.

- `GET`: Request for all Students.

```
    GET:/api/students
```

- `POST`: Request for Posting/Creating/Inserting Data

```
    POST:/api/students

    {“name”:”Raj”}
```

- `PUT` or `PATCH`: Request for Updating Data at id=1

```
    PUT or PATCH:/api/students/1

    {“name”:”Raj”}
```

- `DELETE`: Request for Deleting Data of id=1

```
    DELETE:/api/students/1
```

- RESTful web services are very popular because they are light weight, highly scalable and maintainable and are very commonly used to create APIs for web-based applications.

# Python | Build a REST API using Flask

- REST stands for REpresentational State Transfer and is an architectural style used in modern web development. It defines a set or rules/constraints for a web application to send and receive data.

- In this article, we will build a REST API in Python using the Flask framework. Flask is a popular micro framework for building web applications. Since it is a micro-framework, it is very easy to use and lacks most of the advanced functionality which is found in a full-fledged framework. Therefore, building a REST API in Flask is very simple.

- There are two ways of creating a REST API in Flask:
  - Using `Flask` without any external libraries
  - Using `flask_restful` library

## Method 1: using only Flask
- Here, there are two functions: One function to just return or print the data sent through GET or POST and another function to calculate the square of a number sent through GET request and print it.

```
    # Using flask to make an api
    # import necessary libraries and functions
    from flask import Flask, jsonify, request

    # creating a Flask app
    app = Flask(__name__)

    # on the terminal type: curl http://127.0.0.1:5000/
    # returns hello world when we use GET.
    # returns the data that we send when we use POST.
    @app.route('/', methods = ['GET', 'POST'])
    def home():
        if(request.method == 'GET'):

            data = "hello world"
            return jsonify({'data': data})


    # A simple function to calculate the square of a number
    # the number to be squared is sent in the URL when we use GET
    # on the terminal type: curl http://127.0.0.1:5000 / home / 10
    # this returns 100 (square of 10)
    @app.route('/home/<int:num>', methods = ['GET'])
    def disp(num):

        return jsonify({'data': num**2})


    # driver function
    if __name__ == '__main__':

        app.run(debug = True)
```

## Method 2: Using flask-restful
- `Flask Restful` is an extension for Flask that adds support for building REST APIs in Python using Flask as the back-end. It encourages best practices and is very easy to set up. `Flask restful` is very easy to pick up if you’re already familiar with flask.

- In `flask_restful`, the main building block is a resource. Each resource can have several methods associated with it such as GET, POST, PUT, DELETE, etc. for example, there could be a resource that calculates the square of a number whenever a get request is sent to it. Each resource is a class that inherits from the Resource class of `flask_restful`. Once the resource is created and defined, we can add our custom resource to the api and specify a URL path for that corresponding resource.

```
    # using flask_restful
    from flask import Flask, jsonify, request
    from flask_restful import Resource, Api

    # creating the flask app
    app = Flask(__name__)
    # creating an API object
    api = Api(app)

    # making a class for a particular resource
    # the get, post methods correspond to get and post requests
    # they are automatically mapped by flask_restful.
    # other methods include put, delete, etc.
    class Hello(Resource):

        # corresponds to the GET request.
        # this function is called whenever there
        # is a GET request for this resource
        def get(self):

            return jsonify({'message': 'hello world'})

        # Corresponds to POST request
        def post(self):

            data = request.get_json()     # status code
            return jsonify({'data': data}), 201


    # another resource to calculate the square of a number
    class Square(Resource):

        def get(self, num):

            return jsonify({'square': num**2})


    # adding the defined resources along with their corresponding urls
    api.add_resource(Hello, '/')
    api.add_resource(Square, '/square/<int:num>')


    # driver function
    if __name__ == '__main__':

        app.run(debug = True)
```
