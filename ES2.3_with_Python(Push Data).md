#### Push data into Elasticsearch with Python
```
nano pyestest.csv
id;product;client;tag
90;ab2;wb;8000000
67;ab3;rf;10000000
96;ab4;as;199999
19;ab5;dd;110000000
97;ab6;fb;908700000
```
####Install Pandas, Pyes, Numpy
```
sudo apt-get -y install python-numpy
sudo apt-get -y build-dep python-lxml
sudo apt-get -y install python3-pip
sudo apt-get install python3-pandas
sudo pip3 install pyes
```
####Push data into ES
```
import pandas as pd 
import numpy as np 
import pyes 
import json
df = pd.read_csv("pyestest.csv",sep=";",decimal=".")
df["no_index"] = [x+1 for x in range(len(df["id"]))]
tmp = df.to_json(orient = "records")
df_json= json.loads(tmp)
print (df_json[0])
index_name = 'python_to_elastic'
type_name = 'pyelastic'
es= pyes.ES()

for doc in df_json:
    es.index(doc, index_name, type_name, id=doc['no_index'])
```
####Exploring Data
```
curl 'localhost:9200/_cat/indices?v'
curl -X GET 'http://localhost:9200/python_to_elastic/pyelastic/1?pretty'
curl -X GET 'http://localhost:9200/python_to_elastic/pyelastic/_search?pretty'
```

https://github.com/jerrywu2013/CloudServer/blob/master/Elasticsearch.md

Relational DB -> Databases -> Tables -> Rows -> Columns

Elasticsearch -> Indices   -> Types  -> Documents -> Fields

##### Basic
IP/navi/navi_address/_search?q=name:中國醫藥大學
