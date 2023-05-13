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

# Installation

## Python Version
- We recommend using the latest version of Python. Flask supports Python 3.8 and newer.

## Dependencies
- These distributions will be installed automatically when installing Flask.
  - `Werkzeug` implements WSGI, the standard Python interface between applications and servers.
  - `Jinja` is a template language that renders the pages your application serves.
  - `MarkupSafe` comes with Jinja. It escapes untrusted input when rendering templates to avoid injection attacks.
  - `ItsDangerous` securely signs data to ensure its integrity. This is used to protect Flask’s session cookie.
  - `Click` is a framework for writing command line applications. It provides the flask command and allows adding custom management commands.
  - `Blinker` provides support for `Signals`.
## Optional dependencies
- These distributions will not be installed automatically. Flask will detect and use them if you install them.
  - `python-dotenv` enables support for `Environment Variables From dotenv` when running flask commands.
  - `Watchdog` provides a faster, more efficient reloader for the development server.

## Virtual environments
- Use a virtual environment to manage the dependencies for your project, both in development and in production.
- What problem does a virtual environment solve? The more Python projects you have, the more likely it is that you need to work with different versions of Python libraries, or even Python itself. Newer versions of libraries for one project can break compatibility in another project.
- Virtual environments are independent groups of Python libraries, one for each project. Packages installed for one project will not affect other projects or the operating system’s packages.
- Python comes bundled with the `venv` module to create virtual environments.

## Create an environment
- Create a project folder and a `.venv` folder within:
  - **macOS/Linux**
  ```
      $ mkdir myproject
      $ cd myproject
      $ python3 -m venv .venv
  ```
  - **Window** 
  ```
      > mkdir myproject
      > cd myproject
      > py -3 -m venv .venv
  ```
  
## Activate the environment
- Before you work on your project, activate the corresponding environment:
  - **macOS/Linux** 
  ```
      $ . .venv/bin/activate
  ```
  - **Window** 
  ```
      > .venv\Scripts\activate
  ```
- Your shell prompt will change to show the name of the activated environment.
  
## Install Flask
- Within the activated environment, use the following command to install Flask:
```
      $ pip install Flask
```

# Quickstart

## A Minimal Application
- A minimal Flask application looks something like this:
```
    from flask import Flask

    app = Flask(__name__)

    @app.route("/")
    def hello_world():
        return "<p>Hello, World!</p>"
```
- So what did that code do?
  - First we imported the `Flask` class. An instance of this class will be our WSGI application.
  - Next we create an instance of this class. The first argument is the name of the application’s module or package. `__name__` is a convenient shortcut for this that is appropriate for most cases. This is needed so that Flask knows where to look for resources such as templates and static files.
  - We then use the `route()` decorator to tell Flask what URL should trigger our function.
  - The function returns the message we want to display in the user’s browser. The default content type is HTML, so HTML in the string will be rendered by the browser. 
- Save it as `hello.py` or something similar. Make sure to not call your application `flask.py` because this would conflict with Flask itself.
- To run the application, use the `flask` command or `python -m flask`. You need to tell the Flask where your application is with the `--app` option.
- This launches a very simple builtin server, which is good enough for testing but probably not what you want to use in production.
- Now head over to `http://127.0.0.1:5000/`, and you should see your hello world greeting.
- If another program is already using port 5000, you’ll see `OSError: [Errno 98]` or `OSError: [WinError 10013]` when the server tries to start. 
- **Application Discovery Behavior**
  - As a shortcut, if the file is named `app.py` or `wsgi.py`, you don’t have to use `--app`.
- **Externally Visible Server**
  - If you run the server you will notice that the server is only accessible from your own computer, not from any other in the network. This is the default because in debugging mode a user of the application can execute arbitrary Python code on your computer.
  - If you have the debugger disabled or trust the users on your network, you can make the server publicly available simply by adding `--host=0.0.0.0` to the command line:
  - `$ flask run --host=0.0.0.0`
  - This tells your operating system to listen on all public IPs.

## Debug Mode
- The `flask run` command can do more than just start the development server. By enabling debug mode, the server will automatically reload if code changes, and will show an interactive debugger in the browser if an error occurs during a request.
- **Warning**
  - The debugger allows executing arbitrary Python code from the browser. It is protected by a pin, but still represents a major security risk. Do not run the development server or debugger in a production environment.
- To enable debug mode, use the `--debug` option as below or `app.run(debug=True)`.
```
    $ flask --app hello run --debug
     * Serving Flask app 'hello'
     * Debug mode: on
     * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)
     * Restarting with stat
     * Debugger is active!
     * Debugger PIN: nnn-nnn-nnn
```

## HTML Escaping
- When returning HTML (the default response type in Flask), any user-provided values rendered in the output must be escaped to protect from injection attacks. HTML templates rendered with Jinja, introduced later, will do this automatically.
- `escape()`, shown here, can be used manually. It is omitted in most examples for brevity, but you should always be aware of how you’re using untrusted data.
```
    from markupsafe import escape

    @app.route("/<name>")
    def hello(name):
        return f"Hello, {escape(name)}!"
```
- If a user managed to submit the name `<script>alert("bad")</script>`, escaping causes it to be rendered as text, rather than running the script in the user’s browser.
- `<name>` in the route captures a value from the URL and passes it to the view function. These variable rules are explained below.

## Routing
- Modern web applications use meaningful URLs to help users. Users are more likely to like a page and come back if the page uses a meaningful URL they can remember and use to directly visit a page.
- Use the `route()` decorator to bind a function to a URL.
```
    @app.route('/')
    def index():
        return 'Index Page'

    @app.route('/hello')
    def hello():
        return 'Hello, World'
```
- You can do more! You can make parts of the URL dynamic and attach multiple rules to a function.

## Variable Rules
- You can add variable sections to a URL by marking sections with `<variable_name>`. Your function then receives the `<variable_name>` as a keyword argument. Optionally, you can use a converter to specify the type of the argument like `<converter:variable_name>`.
```
    from markupsafe import escape

    @app.route('/user/<username>')
    def show_user_profile(username):
        # show the user profile for that user
        return f'User {escape(username)}'

    @app.route('/post/<int:post_id>')
    def show_post(post_id):
        # show the post with the given id, the id is an integer
        return f'Post {post_id}'

    @app.route('/path/<path:subpath>')
    def show_subpath(subpath):
        # show the subpath after /path/
        return f'Subpath {escape(subpath)}'
```
- **Converter types:**
  - `string` : (default) accepts any text without a slash
  - `int` : accepts positive integers
  - `float` : accepts positive floating point values
  - `path` : like string but also accepts slashes
  - `uuid` : accepts UUID strings

## Unique URLs / Redirection Behavior
- The following two rules differ in their use of a trailing slash.
```
    @app.route('/projects/')
    def projects():
        return 'The project page'

    @app.route('/about')
    def about():
        return 'The about page'
```
- The canonical URL for the `projects` endpoint has a trailing slash. It’s similar to a folder in a file system. If you access the URL without a trailing slash (`/projects`), Flask redirects you to the canonical URL with the trailing slash (`/projects/`).
- The canonical URL for the `about` endpoint does not have a trailing slash. It’s similar to the pathname of a file. Accessing the URL with a trailing slash (`/about/`) produces a 404 “Not Found” error. This helps keep URLs unique for these resources, which helps search engines avoid indexing the same page twice.

## URL Building
- To build a URL to a specific function, use the `url_for()` function. It accepts the name of the function as its first argument and any number of keyword arguments, each corresponding to a variable part of the URL rule. Unknown variable parts are appended to the URL as query parameters.
- Why would you want to build URLs using the URL reversing function `url_for()` instead of hard-coding them into your templates?
  - Reversing is often more descriptive than hard-coding the URLs.
  - You can change your URLs in one go instead of needing to remember to manually change hard-coded URLs.
  - URL building handles escaping of special characters transparently.
  - The generated paths are always absolute, avoiding unexpected behavior of relative paths in browsers.
  - If your application is placed outside the URL root, for example, in `/myapplication` instead of `/`, `url_for()` properly handles that for you.

- For example, here we use the `test_request_context()` method to try out `url_for()`. `test_request_context()` tells Flask to behave as though it’s handling a request even while we use a Python shell.
```
    from flask import url_for

    @app.route('/')
    def index():
        return 'index'

    @app.route('/login')
    def login():
        return 'login'

    @app.route('/user/<username>')
    def profile(username):
        return f'{username}\'s profile'

    with app.test_request_context():
        print(url_for('index'))
        print(url_for('login'))
        print(url_for('login', next='/'))
        print(url_for('profile', username='John Doe'))
```
```
    /
    /login
    /login?next=/
    /user/John%20Doe
```

## HTTP Methods
- Web applications use different HTTP methods when accessing URLs. You should familiarize yourself with the HTTP methods as you work with Flask. By default, a route only answers to `GET` requests. You can use the `methods` argument of the `route()` decorator to handle different HTTP methods.
```
    from flask import request

    @app.route('/login', methods=['GET', 'POST'])
    def login():
        if request.method == 'POST':
            return do_the_login()
        else:
            return show_the_login_form()
```
- The example above keeps all methods for the route within one function, which can be useful if each part uses some common data.

- You can also separate views for different methods into different functions. Flask provides a shortcut for decorating such routes with `get()`, `post()`, etc. for each common HTTP method.

```
    @app.get('/login')
    def login_get():
        return show_the_login_form()

    @app.post('/login')
    def login_post():
        return do_the_login()
```
- If `GET` is present, Flask automatically adds support for the `HEAD` method and handles `HEAD` requests according to the HTTP RFC. Likewise, `OPTIONS` is automatically implemented for you.

## Static Files
- Dynamic web applications also need static files. That’s usually where the CSS and JavaScript files are coming from. Ideally your web server is configured to serve them for you, but during development Flask can do that as well. Just create a folder called `static` in your package or next to your module and it will be available at `/static` on the application.
- To generate URLs for static files, use the special `'static'` endpoint name:
```
  url_for('static', filename='style.css')
```
- The file has to be stored on the filesystem as `static/style.css`.

## Rendering Templates
- Generating HTML from within Python is not fun, and actually pretty cumbersome because you have to do the HTML escaping on your own to keep the application secure. Because of that Flask configures the Jinja2 template engine for you automatically.
- Templates can be used to generate any type of text file. For web applications, you’ll primarily be generating HTML pages, but you can also generate markdown, plain text for emails, and anything else.
- For a reference to HTML, CSS, and other web APIs, use the MDN Web Docs.
- To render a template you can use the `render_template()` method. All you have to do is provide the name of the template and the variables you want to pass to the template engine as keyword arguments. Here’s a simple example of how to render a template:
```
    from flask import render_template

    @app.route('/hello/')
    @app.route('/hello/<name>')
    def hello(name=None):
        return render_template('hello.html', name=name)
```
Flask will look for templates in the `templates` folder. So if your application is a module, this folder is next to that module, if it’s a package it’s actually inside your package:

  - Case 1: a module:
  ```
      /application.py
      /templates
        /hello.html 
  ```
  - Case 2: a package:
  ```
    /application
      /__init__.py
      /templates
          /hello.html
```

- For templates you can use the full power of Jinja2 templates. Head over to the official Jinja2 Template Documentation for more information.
- Here is an example template:
- 
```
    <!doctype html>
    <title>Hello from Flask</title>
    {% if name %}
      <h1>Hello {{ name }}!</h1>
    {% else %}
      <h1>Hello, World!</h1>
    {% endif %}
```

- Inside templates you also have access to the `config`, `request`, `session` and `g` 1 objects as well as the `url_for()` and `get_flashed_messages()` functions.

- Templates are especially useful if inheritance is used. If you want to know how that works, see Template Inheritance. Basically template inheritance makes it possible to keep certain elements on each page (like header, navigation and footer).

- Automatic escaping is enabled, so if `name` contains HTML it will be escaped automatically. If you can trust a variable and you know that it will be safe HTML (for example because it came from a module that converts wiki markup to HTML) you can mark it as safe by using the `Markup` class or by using the `|safe` filter in the template. Head over to the Jinja 2 documentation for more examples.

- Here is a basic introduction to how the Markup class works:

```
    from markupsafe import Markup
    Markup('<strong>Hello %s!</strong>') % '<blink>hacker</blink>'
    Markup('<strong>Hello &lt;blink&gt;hacker&lt;/blink&gt;!</strong>')
    Markup.escape('<blink>hacker</blink>')
    Markup('&lt;blink&gt;hacker&lt;/blink&gt;')
    Markup('<em>Marked up</em> &raquo; HTML').striptags()
    'Marked up » HTML'
```
- Unsure what that `g` object is? It’s something in which you can store information for your own needs. See the documentation for `flask.g` and `Using SQLite 3 with Flask`.


## The Request Object
- The request object is documented in the API section and we will not cover it here in detail (see `Request`). Here is a broad overview of some of the most common operations. First of all you have to import it from the `flask` module:

```
    from flask import request
```

- The current request method is available by using the `method` attribute. To access form data (data transmitted in a `POST` or `PUT` request) you can use the `form` attribute. Here is a full example of the two attributes mentioned above:

```
@app.route('/login', methods=['POST', 'GET'])
def login():
    error = None
    if request.method == 'POST':
        if valid_login(request.form['username'],
                       request.form['password']):
            return log_the_user_in(request.form['username'])
        else:
            error = 'Invalid username/password'
    # the code below is executed if the request method
    # was GET or the credentials were invalid
    return render_template('login.html', error=error)
```

- What happens if the key does not exist in the `form` attribute? In that case a special `KeyError` is raised. You can catch it like a standard `KeyError` but if you don’t do that, a HTTP 400 Bad Request error page is shown instead. So for many situations you don’t have to deal with that problem.

- To access parameters submitted in the URL (`?key=value`) you can use the `args` attribute:

```
    searchword = request.args.get('key', '')
```
- We recommend accessing URL parameters with get or by catching the `KeyError` because users might change the URL and presenting them a 400 bad request page in that case is not user friendly.

- For a full list of methods and attributes of the `request` object, head over to the Request documentation.
