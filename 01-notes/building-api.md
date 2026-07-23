# Building API
Date: 2026-07-21

## * Postman
Why use postman? The browser can only handle request, postman allows users to handle all request methods (GET, POST, PUT, DELETE)

#### ** Download Postman
	Go to official website -> download -> sign up -> create a workspace -> create a collection

## * Syntax
```python
from flask import Flask, Response
import json
import os
import pymongo
from bson.json_util import dumps
from bson.objectid import ObjectId

app = Flask(__name__)

MONGODB_URL= 'mongodb+srv://jevonaugustianlim01_db_user:wSorGt87EyrpXMbY@cluster0.7xabvmi.mongodb.net/?appName=Cluster0'
client = pymongo.MongoClient(MONGODB_URL)
db = client['thirty_days_of_python']


@app.route('/api/v1.0/students', methods=['GET'])
def students():
    return Response(dumps(db.students.find()), mimetype='application/json')

@app.route('/api/v1.0/students/<id>', methods=['GET'])
def single_student(id):
    student = db.students.find_one({'_id': ObjectId(id)})

    if not student:
        return Response(dumps({"mesage": "Student not found"}, mimetype="application/json", status=404))
    return Response(dumps(student), mimetype='application/json')

if __name__ == '__main__':
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)

```
#### ** Flask `Response`
	It is flask built-in class that creates proper HTTP response

#### ** `bson`
	bson stands for binary json, support ObjectID, Data, Decimal128, etc, installed together with pymongo

#### ** Core Flask Syntax
	1. app = Flask(__name__) #creates web app object
	2. @app.route #decorator that connects URL to function below
	3. app.run() #launch local web server
	4. debug=True #auto-restarts server when edit code
	5. port=5000 #port number your server runs on

#### ** Mimetype
```python
application/json #json data
text/html #normal html
text/plain #plain text
image/png #image files
application/pdf #pdf file
text/css/application/javascript #stylesheet and JS
```

#### ** `http://localhost:5000/api/v1.0/students`
	localhost is your own computer

#### ** `<id>`
It is called as URL variable/parameter, it creates placeholder inside URL to capture dynamic values as a string. The name inside `<id>` must match parameter name. 

**Ways to convert variable type**

```python
<string:id>
<int:number>
<float:price>
<path:text>
```


---

## * Mistakes I Make and Solution

1. Use find() instead of findall() for MongoDB syntax
2. To paste without formatting use `Ctrl + Shift + V`
3. Use single quotes ' ' for normal short strings (variable text, routes, keys), use double quotes " " for human-facing output messages.
4. Sometimes the reason why css file doesn't work is just a matter of wrong defining the file path
5. In browser, you cannot use method PUT and DELETE
6. To find with id, use the query `{"_id": ObjectId(id)}`
7. Building an API means building a server that use HTTP methods to perform CRUD with data in JSON format.

## * For Review
```markdown
1. Why do you use postman instead of the actual browser?
2. What Response() is used for and its syntax
3. <> as URL variable/parameter
4. Why sometimes use bson library instead of json?
```



#postman #flask #json #bson #mistakes