# Project Title: Comprehensive Comparison Of RDBMS and NoSQL Databases For Healthcare Applications

Performance analysis of RDBMS and Document NoSQL MongoDB for Healthcare Insurance Recommendation Application. Organizations who needs to change their database for better performance can be benefited from this project.

## Overview
Healthcare Insurance Recommendation Application gives user or patient the best suited medical coverage plan based on some predefined conditions.
We have generated pseudo data which includes two tables with Insurance details and with Patient details. 
With the use of Jmeter and python modules performance wrt time is measured.
## Installation
#### 1. Jmeter
#### Download a jmeter package:
http://apache.mirrors.pair.com//jmeter/binaries/apache-jmeter-5.1.1.zip

#### Download groovy jar file:
https://jar-download.com/artifacts/org.codehaus.groovy/groovy/2.4.4/source-code

#### Download mongo java jar file:
https://download.jar-download.com/cache_jars/org.mongodb/mongo-java-driver/3.8.0/jar_files.zip

#### 2. RDS AWS
RDS Basics
📒 Homepage ∙ https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html ∙ FAQ ∙ Pricing (see also ec2instances.info/rds/)
RDS is a managed relational database service, allowing you to deploy and scale databases more easily. It supports Oracle, Microsoft SQL Server, PostgreSQL, MySQL, MariaDB, and Amazon’s own Aurora.
RDS offers out of the box support for high availability and failover for your databases.

#### 3. Mongodb-Atlas with 3 clusters
https://account.mongodb.com/account/login

#### 4. Download Python
https://www.python.org/
    
## Project Pre
#### 1. Synthetic Data Creation
sample code for Patient table creation
```python
import pandas as pd
import numpy as np
from datetime import datetime, date
import random

np.random.seed(4)
val1 = np.random.choice(['Male','Female'],nrows)
val2 = pd.to_datetime(np.random.randint(pd.Timestamp(start).value, pd.Timestamp(end).value,nrows, dtype=np.int64)).strftime('%Y/%m/%d')
```
For Insurance data we increased records from 100k to 300k repeating the above tests.

Sample data csv for Insurance table: 
![Insurance_Sample_Data](https://user-images.githubusercontent.com/98043861/169841831-06947243-21e0-4ad5-a611-24a7e90a8c11.png)
For Patient data we increased records from 501k to 150k repeating the above tests.

Sample data csv for Patient table:
![Patients_Sample_Data](https://user-images.githubusercontent.com/98043861/169842347-005a05ac-6e1d-4778-8786-a34643bbd1a4.png)
#### 2. Connection to MongoDB
```python
from pymongo import MongoClient

cluster = <cluster connection string>
client = MongoClient(cluster)
```
#### 3. Connection to AWS RDS
```python
import pymysql

db = pymysql.connect(host= <connection string>, user= <user name>, password= <pwd>)
cursor=db.cursor()
```



## Tests Performed

Sample code for running CRUD operations

#### 1. CREATE for RDS
```python
file_name=df
values1=list()
for r in range(0,len(file_name)): values1.append(tuple(list(file_name.iloc[r])))
cursor.executemany(query1,values1)
db.commit()
```
#### CREATE for MongoDB
```python
db = client.Mongo_db
coll = db.coll_name
payload = json.loads (csv_df.to_json(orient='records'))
coll.insert_many(payload)
```
#### 2. INSERT for RDS
```python
sql = '''
INSERT INTO Tablename (column1, column2, column3,.......) VALUES ("value1''', "value2",....)
cursor.execute(sql)
db.commit()
```
#### INSERT for MongoDB
```python
result = coll.insert_one(dict)
```
#### 3. READ for RDS
```python
SQL_Query = pd.read_sql_query( <select statement >, db, params=(variables))
selector_results = pd.DataFrame(SQL_Query)
```
#### READ for MongoDB
```python
pipeline = <aggregation operations>
results = coll.aggregate(pipeline)
```
#### 4. UPDATE for RDS
```python
sql = <SQL update statement>
cursor.execute(sql)
db.commit()
```
#### UPDATE for MongoDB
```python
result=coll.update_one(<column_update>)
```
#### 5. DELETE for RDS
```python
sql = <delete statement>
cursor.execute(sql)
db.commit()
```
#### DELETE for MongoDB
```python
one=coll.delete_one(<column_delete>)
```


## Sample Results
Read operation results using Jmeter:
![Read - Jmeter (2)](https://user-images.githubusercontent.com/98043861/169919717-0d7a7e73-56c3-4265-a9df-a10d71df1965.png)

Read operation results using python timestamp:
![Read - Python](https://user-images.githubusercontent.com/98043861/169837702-215017b7-9644-4048-9894-19909c407c85.png)



## Credits
#### Team Members:

Swetha Subramanian https://github.com/swethasubu93

Revathi Boopathi

Madhura Pandit https://github.com/madhurapandit
## Appendix

Github Project Link: 
https://github.com/Revathi-Praveen/DB225_TermProject_Group1

