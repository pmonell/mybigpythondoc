My Big Python Doc
=================
A document for all things python. Kept well indexed with code commentary.
- [Core Modules](#core modules)
    - [Utility](#utility)
    - [Special Attributes](#special attributes)
- [Design Patterns](#design patterns)
    - [Creational](#creational)
    - [Structural](#structural)
    - [Behavioral](#behavioral)

-
### Core modules
###### utility
- datetime
```python
import datetime

now = datetime.datetime.now()
utc_now = datetime.datetime.utcnow()
time = datetime.time()
```

- re (regular expression)
matching and using groups
```python
import re

sentence = "Hello, this is my garble.d sentence"

# use parenthesis to group matching strings, 
# search for one or more characters matching the set in a word
matched = re.match(r'([A-Za-z])\w+', sentence)

print matched.groups() # prints '('H',)'
print matched.group(0) # prints 'Hello'
print matched.group(1) # prints 'H'
```

- ctypes (create and manipulate C data types) 

###### special attributes
- \__file__
- \__dir__

### Design Patterns
##### Creational
flask app factory pattern

app.py
```python
from flask import Flask, blueprint
from flask.ext.mongoengine import MongoEngine
from app.routes import login

# initialize db object
db = MongoEngine()

# app factory allows configuration overrides
def create_app(**config_overrides):
    app = Flask(__name__)
    app.config.from_object('config')
    app.config.update(config_overrides)
    
    # initialize db within flask app
    app.init_db(db)
    
    # register routes into app from module
    app.register_blueprint(login)

    return app
```
run.py
```python
from app import create_app
# standard from configuration file
app = create_app()
app.run
```
-
##### Structural 
**adapter**
creates compatibility between client code and objects, standardizes the interface of classes

**decorator**
simple logger decorator
```python
def logger(func):
    # define function that arbitrary number and type of parameters
    def inner(*args, **kwargs):

        for count, arg in enumerate(args):
            print "arg %d: %s" % (count, arg)

        for key, value in kwargs.iteritems():
            print "key %s: %s" % (key, value)
        
        # return func with passed parameters from inner
        return func(*args, **kwargs)
    return inner

@logger
def add_values(x, y, z=5):
    return x + y + z

if __name__ == '__main__':
    add_values(5, 4, z=8)

    '''prints:
    arg 0: 5
    arg 1: 4
    key z: 8
    '''
```

**facade**

##### Behavioral

### Unit Testing
- frameworks include unittest, pytest, nose, all of which extend unittest
- extensions can be found in many modules, ie. Flask

```python
import unittest
import mongoengine

from app import create_app as create_app_base

def create_app():
    return create_app_base(
        MONGODB_SETTINGS={'DB': 'db_test'},
        TESTING = True,
        CSRF_ENABLED = False,
    )

class TestCase(unittest.TestCase):
    
    def setUp(self):
        self.app = create_app()

    def tearDown(self):
        pass

    def test_app_creation(self): 
        assert mongoengine.connection.get_db().name == 'db_test'
        assert self.app.config['TESTING']

    def test_hello_world(self):
        with self.app.test_client() as c:
            result = c.get('/')
            self.assertEqual(result.data, 'hello world')
```
