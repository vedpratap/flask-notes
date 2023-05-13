# flask-notes

- **Flask** is a web framework, it’s a Python module that lets you develop web applications easily. It’s has a small and easy-to-extend core: it’s a microframework that doesn’t include an ORM (Object Relational Manager) or such features. It does have many cool features like url routing, template engine. It is a WSGI web app framework.
- A **Web Application Framework** or a simply a **Web Framework** represents a collection of libraries and modules that enable web application developers to write applications without worrying about low-level details such as protocol, thread management, and so on.
- **Flask** is a web application framework written in Python. It was developed by Armin Ronacher, who led a team of international Python enthusiasts called Poocco. Flask is based on the Werkzeg WSGI toolkit and the Jinja2 template engine.Both are Pocco projects.
- **WSGI** : The Web Server Gateway Interface (Web Server Gateway Interface, WSGI) has been used as a standard for Python web application development. WSGI is the specification of a common interface between web servers and web applications.
- **Werkzeug** is a WSGI toolkit that implements requests, response objects, and utility functions. This enables a web frame to be built on it. The Flask framework uses Werkzeg as one of its bases.
- **Jinja2** is a popular template engine for Python.A web template system combines a template with a specific data source to render a dynamic web page.This allows you to pass Python variables into HTML templates like this:
```
  <html>
      <head>
          <title>{{ title }}</title>
      </head>
      <body>
          <h1>Hello {{ username }}</h1>
      </body>
  </html>
```
- Flask is often referred to as a microframework. It is designed to keep the core of the application simple and scalable. Instead of an abstraction layer for database support, Flask supports extensions to add such capabilities to the application.
- Unlike the Django framework, Flask is very Pythonic. It’s easy to get started with Flask, because it doesn’t have a huge learning curve.
- On top of that it’s very explicit, which increases readability. To create the “Hello World” app, you only need a few lines of code.
- This is a boilerplate code example.
```
    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def hello_world():
        return 'Hello World!'

    if __name__ == '__main__':
        app.run()
```
- If you want to develop on your local computer, you can do so easily. Save this program as `server.py` and run it with `python server.py`.
```
$ python server.py
 * Serving Flask app "hello"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```
- It then starts a web server which is available only on your computer. In a web browser open localhost on port 5000 (the url) and you’ll see **“Hello World”** show up.
- It’s a microframework, but that doesn’t mean your whole app should be inside one single Python file. You can and should use many files for larger programs, to handle complexity.
- Micro means that the Flask framework is simple but extensible. You may all the decisions: which database to use, do you want an ORM etc, Flask doesn’t decide for you.
- Flask is one of the most popular web frameworks, meaning it’s up-to-date and modern. You can easily extend it’s functionality. You can scale it up for complex applications.
