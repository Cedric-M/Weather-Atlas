# Getting started with MongoDB Atlas

https://www.mongodb.com/cloud/atlas

    python3 -m pip install pymongo


```python
from pymongo import MongoClient

client = MongoClient("mongodb://test:test@clusteraws1-shard-00-00-pecbe.mongodb.net:27017,clusteraws1-shard-00-01-pecbe.mongodb.net:27017,clusteraws1-shard-00-02-pecbe.mongodb.net:27017/test?ssl=true&replicaSet=ClusterAWS1-shard-0&authSource=admin&retryWrites=true&w=majority")
```

    To find the URI, go to: Your Cluster > Connect > Connect your application > Driver "Python" and version "3.4 or later".


```python
db = client.get_database('weather_db')
```


```python
records = db.weather_data
```

# Count documents


```python
records.count_documents({})
```




    1



# Create new document


```python
new_weather = {
    'name': 'Toulouse',
    'temp': 32,
    'country': 'France'
}
```


```python
records.insert_one(new_weather)
```




    <pymongo.results.InsertOneResult at 0x7f45fac40af0>




```python
new_weathers = [
    {
        'name': 'Marseille',
        'temp': 35,
        'country': 'France'
    },
    {
        'name': 'Pau',
        'temp': 12,
        'country': 'France'
    }
]
```


```python
records.insert_many(new_weathers)
```




    <pymongo.results.InsertManyResult at 0x7f45e8812690>



# Find documents


```python
list(records.find())
```




    [{'_id': ObjectId('5df28f5e1c9d4400002690c8'),
      'name': 'Paris',
      'temp': 35,
      'country': 'France'},
     {'_id': ObjectId('5df7a20a4d0d42a9e3e84c4b'),
      'name': 'Toulouse',
      'temp': 32,
      'country': 'France'},
     {'_id': ObjectId('5df7a3094d0d42a9e3e84c4c'),
      'name': 'Marseille',
      'temp': 35,
      'country': 'France'},
     {'_id': ObjectId('5df7a3094d0d42a9e3e84c4d'),
      'name': 'Pau',
      'temp': 12,
      'country': 'France'}]




```python
records.find_one({'temp': 12})
```




    {'_id': ObjectId('5df7a3094d0d42a9e3e84c4d'),
     'name': 'Pau',
     'temp': 12,
     'country': 'France'}



# Update documents


```python
weather_updates = {
    'name': 'Lyon'
}
```


```python
records.update_one({'temp': 32}, {'$set': weather_updates})
```




    <pymongo.results.UpdateResult at 0x7f45ea312eb0>



# Delete documents


```python
records.delete_one({'temp': 12})
```




    <pymongo.results.DeleteResult at 0x7f45e87e5b90>

