#Python and SQLAlchemy

Interacting with a SQL database using SQLAlchemy

There are various packages and libraries that interact with SQL (SQLAlchemy, Django, pewee, SQLObject, Storm, pony) but the most popular and probably the best and most beautiful Python library ever written is SQLAlchemy.
SQLAlchemy allows you to write raw SQL directly and operate in SQL tables using them essentially as Python classes - basically, read and write data using SQL and then treat that data as a Python container.

##How to use SQLAlchemy:
* Create an engine
* Define tables
* Add instances
* Query

###Create an engine: 
Create an engine that establishes a connection with the database and sets the framework in order to make SQL requests. Like so:

```
from sqlalchemy import create_engine
engine = create_engine('sqlite:////phonebook.db', echo=True)
# if working on a PC use:  engine = create_engine('sqlite:///C:\\folder\\path\\phonebook.db', echo=True) 
```

###Define tables: 
Create a class call `Base` (using `declarative_base`) to define our various tables - SQLAlchemy will refer to this class to create the table schemas. Use the `__tablename__` member to name the table and `__repr__` method when printing a table row. Like so:

```
from sqlalchemy import Column, Integer, String
class Phonebook(Base):
    __tablename__ = "friends"
    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)
    phone = Column(String)

    def __repr__(self):
        return "<Phonebook(name='%s', email='%s', phone='%s')>"\
            %(self.name, self.email, self.phone)
```

Now that we have the engine, use the metadata `create_all` method to actually create the database - if working on a mac, run this from the terminal using iPython, if working from a PC just append this line to the .py file that we are building here:

```
Base.metadata.create_all(engine)
```

###Add instances: 
Establish a session in order to interact with the database, and create instances and rows so that we can add them to the session:

```
# create a list with our friend's numbers
friends_numbers = [
    {'name': 'James Rodriguez',
     'email': 'james@email.com',
     'phone': '123-456-7890'},
    {'name': 'Pibe Valderrama',
     'email': 'pibe@email.com',
     'phone': '111-222-3333'},
    {'name': 'Farid Mondragon',
     'email': 'farid@email.com',
     'phone': '222-333-4444'}     
     ]

# create tables
Base.metadata.create_all(engine)

# establish a session
from sqlalchemy.orm import sessionmaker

session = sessionmaker(bind=engine)
session = session()

# create instances
# use ** to unpack the key-value pairs
james = Phonebook(**friends_numbers[0])

# add james to the Phonebook database
session.add(james)
session.new

# delete james from the Phonebook database
session.expunge(james)
session.new

# add all records from the friends_numbers list into the db
phonebook_rows = [Phonebook(**p) for p in friends_numbers]
session.add_all(phonebook_rows)
session.commit()
```

###Query the database
Now you can go ahead a run any query you'd like. All you have to do is use the `session` method. Like so:

```
# query the database
# count how many records we have
print session.query(Phonebook).count()

# find James Rodriguez record using filter_by
friend = session.query(Phonebook).filter_by(name='James Rodriguez')
result = list(friend)
print result
```

For a list of all available methods, check SQLAlchemy documentation [here](http://docs.sqlalchemy.org/en/latest/orm/query.html).
The entire code for this article is available [here](https://github.com/TheBecky/python_awesomeness/blob/master/python_sql.py). Send me a note if you have any issues with the above code and would like help debugging becky@datasommelier.com
