## Overview

1. The data is stored in the documents, which is a unit of information. A doocument corresponds to a row in a relational DB and can represent a question, QS etc.
2. A document contains fields that correspond to columns in a RDB. A document is a JSON object. To add a doocument, you send a JSON object to ES api.

## Elastic Stack

### Kibana

In simple words, it is a web interface to the data that is stored in ES. It also give a lot of valuable information like CPU or memory usage.

### Logstash

The data recieved by it will be handled as events. It can be log file entries, orders, customers, chat messages etc. 
