[toc]
## 23.2 SQLite - using the sqlite3 database
```python

>>> import sqlite3
>>> conn = sqlite3.connect("datafile.db")


>>> cursor = conn.cursor()
>>> cursor
<sqlite3.Cursor object at 0xb7a12980>


>>> cursor.execute("create table people (id integer primary key, name text, count integer)")
<sqlite3.Cursor object at 0x7fef111031f0>
>>> cursor.execute("insert into people (name, count) values ('Bob', 1)")
>>> cursor.execute("insert into people (name, count) values (?, ?)", 
...                ("Jill", 15))
<sqlite3.Cursor object at 0x7fef111031f0>
>>> conn.commit()


>>> cursor.execute("insert into people (name, count) values (:username, :usercount)", {"username": "Joe", "usercount": 10})


>>> result = cursor.execute("select * from people")
>>> print(result.fetchall())
[(1, 'Bob', 1), (2, 'Jill', 15), (3, 'Joe', 10)]
>>> result = cursor.execute("select * from people where name like :name", 
...                         {"name": "bob"})
>>> print(result.fetchall())
[(1, 'Bob', 1)]
>>> cursor.execute("update people set count=? where name=?", (20, "Jill"))
>>> result = cursor.execute("select * from people")
>>> print(result.fetchall())
[(1, 'Bob', 1), (2, 'Jill', 20), (3, 'Joe', 10)]


>>> result = cursor.execute("select * from people")
>>> for row in result:
...     print(row)
... 
(1, 'Bob', 1)
(2, 'Jill', 20)
(3, 'Joe', 10)


>>> cursor.execute("update people set count=? where name=?", (20, "Jill"))
>>> conn.commit()
>>> conn.close()

```

## 23.4 Making database handling easier with an ORM
### 23.4.1 SQLAlchemy
```python

>>> from sqlalchemy import create_engine, select, MetaData, Table, Column, Integer, String
>>> from sqlalchemy.orm import sessionmaker


>>> dbPath = 'datafile2.db'
>>> engine = create_engine('sqlite:///%s' % dbPath)
>>> metadata = MetaData(engine)
>>> people  = Table('people', metadata, 
...                 Column('id', Integer, primary_key=True),
...                 Column('name', String),
...                 Column('count', Integer),
...                )
>>> Session = sessionmaker(bind=engine)
>>> session = Session()
>>> metadata.create_all(engine)


>>> people_ins = people.insert().values(name='Bob', count=1)
>>> str(people_ins)
'INSERT INTO people (name, count) VALUES (?, ?)'
>>> session.execute(people_ins)
<sqlalchemy.engine.result.ResultProxy object at 0x7f126c6dd438>
>>> session.commit()


>>> session.execute(people_ins, [
...     {'name': 'Jill', 'count':15},
...     {'name': 'Joe', 'count':10}
... ])
<sqlalchemy.engine.result.ResultProxy object at 0x7f126c6dd908>
>>> session.commit()
>>> result = session.execute(select([people]))
>>> for row in result:
...     print(row)
... 
(1, 'Bob', 1)
(2, 'Jill', 15)
(3, 'Joe', 10)


>>> result = session.execute(select([people]).where(people.c.name == 'Jill'))
>>> for row in result:
...     print(row)
... 
(2, 'Jill', 15)


>>> result = session.execute(people.update().values(count=20).where(people.c.name == 'Jill'))
>>> session.commit()
>>> result = session.execute(select([people]).where(people.c.name == 'Jill'))
>>> for row in result:
...     print(row)
... 
(2, 'Jill', 20)
>>> 


>>> from sqlalchemy.ext.declarative import declarative_base
>>> Base = declarative_base()
>>> class People(Base):
...     __tablename__ = "people"
...     id = Column(Integer, primary_key=True)
...     name = Column(String)
...     count = Column(Integer)
...
>>> results = session.query(People).filter_by(name='Jill')
>>> for person in results:
...     print(person.id, person.name, person.count)
... 
2 Jill 20


>>> new_person = People(name='Jane', count=5)
>>> session.add(new_person)
>>> session.commit()
>>> 
>>> results = session.query(People).all()
>>> for person in results:
...     print(person.id, person.name, person.count)
... 
1 Bob 1
2 Jill 20
3 Joe 10
4 Jane 5


>>> jill = session.query(People).filter_by(name='Jill').first()
>>> jill.name
'Jill'
>>> jill.count = 22
>>> session.add(jill)
>>> session.commit()
>>> results = session.query(People).all()
>>> for person in results:
...     print(person.id, person.name, person.count)
... 
1 Bob 1
2 Jill 22
3 Joe 10
4 Jane 5


>>> jane = session.query(People).filter_by(name='Jane').first()
>>> session.delete(jane)
>>> session.commit()
>>> jane = session.query(People).filter_by(name='Jane').first()
>>> print(jane)
None

```
## 23.6 Key:value stores with Redis
```python

>>> import redis
>>> r = redis.Redis(host='localhost', port=6379)


>>> r.keys()
[]
>>> r.set('a_key', 'my value')
True
>>> r.keys()
[b'a_key']
>>> v = r.get('a_key')
>>> v
b'my value'
>>> r.incr('counter')
1
>>> r.get('counter')
b'1'
>>> r.incr('counter')
2
>>> r.get('counter')
b'2'


>>> r.rpush("words", "one")
1
>>> r.rpush("words", "two")
2
>>> r.lrange("words", 0, -1)
[b'one', b'two']
>>> r.rpush("words", "three")
3
>>> r.lrange("words", 0, -1)
[b'one', b'two', b'three']
>>> r.llen("words")
3
>>> r.lpush("words", "zero")
4
>>> r.lrange("words", 0, -1)
[b'zero', b'one', b'two', b'three']
>>> r.lrange("words", 2, 2)
[b'two']
>>> r.lindex("words", 1)
b'one'
>>> r.lindex("words", 2)
b'two'


>>> r.setex("timed", "10 seconds", 10)
True
>>> r.pttl("timed")
7165
>>> r.pttl("timed")
5208
>>> r.pttl("timed")
1542
>>> r.pttl("timed")
>>>

```
## 23.7 Documents in MongoDB
```python

>>> from pymongo import MongoClient
>>> mongo = MongoClient(host='localhost', port=27017)   #A


>>> import datetime
>>> a_document = {'name': 'Jane',
...               'age': 34,
...               'interests': ['Python', 'databases', 'statistics'],
...               'date_added': datetime.datetime.now()
... }
>>> db = mongo.my_data     #A
>>> collection = db.docs   #B 
>>> collection.find_one()  #C 
>>> db.collection_names()
[]


>>> collection.insert(a_document)
ObjectId('59701cc4f5ef0516e1da0dec')    #A
>>> db.collection_names()
['docs']


>>> collection.find_one()   #A
{'_id': ObjectId('59701cc4f5ef0516e1da0dec'), 'name': 'Jane', 'age': 34, 'interests': ['Python', 'databases', 'statistics'], 'date_added': datetime.datetime(2017, 7, 19, 21, 59, 32, 752000)}
>>> from bson.objectid import ObjectId
>>> collection.find_one({"_id":ObjectId('59701cc4f5ef0516e1da0dec')}) #B
{'_id': ObjectId('59701cc4f5ef0516e1da0dec'), 'name': 'Jane', 'age': 34, 'interests': ['Python', 'databases', 'statistics'], 'date_added': datetime.datetime(2017, 7, 19, 21, 59, 32, 752000)}
>>> collection.update_one({"_id":ObjectId('59701cc4f5ef0516e1da0dec')}, {"$set": {"name":"Ann"}}) #C
<pymongo.results.UpdateResult object at 0x7f4ebd601d38>
>>> collection.find_one({"_id":ObjectId('59701cc4f5ef0516e1da0dec')})
{'_id': ObjectId('59701cc4f5ef0516e1da0dec'), 'name': 'Ann', 'age': 34, 'interests': ['Python', 'databases', 'statistics'], 'date_added': datetime.datetime(2017, 7, 19, 21, 59, 32, 752000)}
>>> collection.replace_one({"_id":ObjectId('59701cc4f5ef0516e1da0dec')}, {"name":"Ann"})   #D
<pymongo.results.UpdateResult object at 0x7f4ebd601750>
>>> collection.find_one({"_id":ObjectId('59701cc4f5ef0516e1da0dec')})
{'_id': ObjectId('59701cc4f5ef0516e1da0dec'), 'name': 'Ann'}
>>> collection.delete_one({"_id":ObjectId('59701cc4f5ef0516e1da0dec')})     #E
<pymongo.results.DeleteResult object at 0x7f4ebd601d80>
>>> collection.find_one()


>>> db.collection_names()
['docs']
>>> collection.drop()
>>> db.collection_names()
[]


```