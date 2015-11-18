My Big Python Doc
=================
A document for all things python. Kept well indexed with code commentary.

### Core modules
###### utility
- datetime
- re (regular expression)
- ctypes (create and manipulate C data types) 

###### special attributes
- __file__
- __dir__

### Design Patterns
###### Creational
flask app factory pattern

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

####### Structural

####### Behavioral
