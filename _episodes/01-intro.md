---
title: Python Flask Fundamentals
teaching: 10
exercises: 10
questions:
- "What is Flask?"
- "How can I create a simple Flask app?"
- "How do I prepare it for extension?"
objectives:
- "Build your first Flask app"
keypoints:
- "Flask is a microframework running in Python."
- "Django is similar but not minimal."
- "Chalice is the AWS equivalent that supports AWS specifics."
---

## Flask - What is it

Flask is a means to create endpoints and webapps. It is a microframework.

It does not force you towards certain methods e.g. databases.

Flask is used by Pintrest and LinkedIn.

A lot can be done with just Flask. But further libraries will extend what you can do- while Django is similar in aims but comes with a lot more assest making such apps bigger, and forces your hand on certain options.

Included in Flask are the components:

- Werkzeug - a WGSI toolkit
- Jinja a template engine
- MarkupSafe -  a string handling library
- ItsDangerous - a data serialization library. Used to store the session of the Flask app in a cookie in a safe way.

## Hello World
~~~
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello() -> str:
    return "Hello World"


if __name__ == "__main__":
    app.run(debug=False)
~~~
{: .language-python}


What does the above mean?

First we import from the `flask` library the `Flask` class.

Then to the app variable we associate an instance of Flask. __name__ is the current name of the module we are building within.

@app.route() is a decorator. This will associate to an URL serviced by the app some code, in our case the function hello().

In this case the function is defined with '->'. This is an annotation. In this case a string class. So we can use this to find out what a function is taking as inputs and returning.

The line checking is __name__ is identical to "__main__" is checking the variable is the same as __main__. So if this were a module being imported that would not be the case. In our example it is so app.run(debug=false) is run. This starts the app.

To run the Flask app we can either;

~~~
$ python3 app.py
~~~
{: .terminal}

or

~~~
$ flask run
~~~
{: .terminal}

The latter is performed in the directory and is looking for app.py. Flask can be run with other keywords other than run.

Doing so produces in the terminal the following

~~~
(flask-vue) chandley@LTW017:~/hello-world-flask$ flask run
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
~~~
{: .output}

We could add more routes to the app.

~~~
from flask import Flask, request
app = Flask(__name__)

@app.route("/")
def hello() -> str:
    return "Hello World"

@app.route("/test", methods=['POST'])
def respond():
    content = request.json
    body = {
        "message": "Go Serverless v1.0! Your function executed successfully!",
        "input": content
    }

    response = {
        "statusCode": 200,
        "body": content['value']
    }

    return response

if __name__ == "__main__":
    app.run(debug=False)
~~~
{: .language-python}

Using Postman we can send the json file payload to our endpoint http://127.0.0.1:5000/test, and the response is the
`value` in content in the response.

~~~
{
    "body": "what",
    "statusCode": 200
}
~~~
{: .output}

The decorator to our `respond` function has the methods attribute of POST. This informs the endpoint it can receive a payload.

Request takes the payload, a json, and only a json, and processes it to content where is is held as a dictionary.

> ## Better File Structure?
>
> How do we improve the file structure?
> Can we improve the way we import our routes?
>
> > ## Solution 
> > ~~~
> > microapp/
> > ├── app
> > │   ├── __init__.py
> > │   └── routes.py
> > └── app.py
> > ~~~
> > {: .terminal}
> > 
> > The routes are split out from the main application
> > as it makes it much easier to then have the routes for each endpoint
> > in their own folder
> >
> > ~~~
> > from app import app
> > 
> > if __name__ == "__main__":
> >     app.run(debug=False)
> > ~~~
> > {: .language-python}
> >
> > A bit confusing, but what is happening is from the app folder the app instance is being imported.
> >
> > ~~~
> > from flask import Flask
> > 
> > app = Flask(__name__)
> > 
> > from app import routes
> > ~~~
> > {: .language-python}
> > 
> > The `__init__.py` file informs python the the files in the folder can be imported as modules
> > and can be left empty. If it is not, then it is preparing other things, like our app, that can then
> > be imported elsewhere.
> >
> > ~~~
> > from app import app
> > from flask import request
> > 
> > @app.route("/")
> > def hello() -> str:
> >     return "Hello World"
> > 
> > @app.route("/test", methods=['POST'])
> > def respond():
> >     content = request.json
> >     body = {
> >         "message": "Go Serverless v1.0! Your function executed successfully!",
> >         "input": content
> >     }
> > 
> >     response = {
> >         "statusCode": 200,
> >         "body": content['value']
> >     }
> >     return response
> > ~~~
> > {: .language-python}
> > 
> > Here we again import the app instance from the app folder.
> > Then we define some of our routes. Routes could be defined elsewhere and imported in a similar manner
> > but then you must still import app from from app for the decorator to work
> {: .solution}

{% include links.md %}
