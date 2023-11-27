## Setting up Elasticsearch and Kibana using docker
Running Elasticsearch and Kibana locally using Docker is a convenient way to set up these tools for development and testing purposes. 
Below are the step-by-step instructions to run Elasticsearch and Kibana using Docker:

### Step 1: Install Docker

If you haven't already, install Docker on your local machine. You can download Docker Desktop for Windows or macOS, or Docker Engine for Linux, from the official Docker website: https://www.docker.com/get-started

### Step 2: Pull Elasticsearch Docker Image

Open a terminal or command prompt and run the following command to pull the Elasticsearch Docker image:

```bash
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.15.0
```

This command downloads the Elasticsearch 7.15.0 Docker image from the official Elasticsearch Docker repository.

### Step 3: Run Elasticsearch Container

Now, start an Elasticsearch container by running the following command:
```bash
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.15.0
-d: Runs the container in the background (daemon mode).
--name elasticsearch: Assigns the name "elasticsearch" to the container.
-p 9200:9200 -p 9300:9300: Maps Elasticsearch ports for HTTP and transport.
-e "discovery.type=single-node": Configures Elasticsearch as a single-node cluster.
```

### Step 4: Pull Kibana Docker Image

Next, pull the Kibana Docker image using the following command:

```bash
docker pull docker.elastic.co/kibana/kibana:7.15.0
```

This command downloads the Kibana 7.15.0 Docker image from the official Kibana Docker repository.

### Step 5: Run Kibana Container

Start a Kibana container by running the following command:
```bash
docker run -d --name kibana -p 5601:5601 --link elasticsearch:elasticsearch docker.elastic.co/kibana/kibana:7.15.0
-d: Runs the container in the background.
--name kibana: Assigns the name "kibana" to the container.
-p 5601:5601: Maps the Kibana port.
--link elasticsearch:elasticsearch: Links the Kibana container to the Elasticsearch container.
```

### Step 6: Access Kibana

After a brief startup period, you can access Kibana by opening a web browser and navigating to http://localhost:5601. Kibana's web interface should now be accessible.

### Step 7: Access Elasticsearch

Elasticsearch is running on http://localhost:9200. You can test Elasticsearch's REST API by opening a web browser or using a tool like curl:
```bash
`curl -X GET "http://localhost:9200/"`
```

---

> Endpoints

* `GET /_cluster/health`

* `GET /_cat/nodes?v`

* `GET /_cat/indices?v&expand_wildcards=all`

* `PUT /pages`

* `GET /pages`

* `GET /_cat/indices?v`

* `GET /_cat/shards?v`

* `GET /_cat/indices`

* `DELETE /pages`


> Below elastic search query will create a new index with name products.
```bash
PUT /products
{
  "settings": {
    "number_of_shards": 2,
    "number_of_replicas": 2
  }
}
```


> Below elastic search query will create a new document with random id in products index.

```bash
POST /products/_doc
{
  "name": "Coffee Maker",
  "price": 64,
  "in_stock": 10
}
```

Response:
```json
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "XZ1Zo3IBX6Q5QX6Q5QX6",
  "_version" : 1,
  "result" : "created",
  "_shards" : {
    "total" : 3,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 0,
  "_primary_term" : 1
}
```


> Below elastic search query will create a new document with id 100 in products index.
```bash
PUT /products/_doc/100
{
  "name": "Toaster",
  "price": 45,
  "in_stock": 3
}
```

Response:
```json
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "100",
  "_version" : 1,
  "result" : "created",
  "_shards" : {
    "total" : 3,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 0,
  "_primary_term" : 1
}
```

> Below elastic search query will get the document with id 100 from products index.
`GET /products/_doc/100`

Response:

```json
{
  "_index" : "products", // index name
  "_type" : "_doc", // type of document
  "_id" : "100",  // id of document
  "_version" : 1, // version of document
  "_seq_no" : 0,  // sequence number
  "_primary_term" : 1,  // primary term
  "found" : true, // document found or not
  "_source" : { // document source
    "name" : "Toaster", // name of product
    "price" : 45, // price of product
    "in_stock" : 3  // stock of product
  }
}
```


// Below elastic search query will update the document with id 100 in products index.

```json
POST /products/_update/100
{
  "doc": {
    "in_stock": 6
  }
}
```

Response:

```json
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "100",
  "_version" : 2,
  "result" : "updated",
  "_shards" : {
    "total" : 3,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 1,
  "_primary_term" : 1
}
```

> Below elastic search query will update the document with id 100 in products index and add the tags field.

```json
POST /products/_update/100
{
  "doc": {
    "tags": ["electronics"]
  }
}
```


Response:
```json
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "100",
  "_version" : 4,
  "result" : "updated",
  "_shards" : {
    "total" : 3,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 3,
  "_primary_term" : 1
}
```

How the update API works
- The current document is retreived from the index.
- The field values are changed.
- The existing document is replaced with the modified document
- The exact same thing can be done at the application level


Scripted Updates:

```json
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock --",
  }
}
```

//Below elastic search query will update the document with id 100 in products index and decrement the in_stock by 4

```json
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock -= params.quantity",
    "params": {
      "quantity": 4
    }
  }
}
```

Response:
```json
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "100",
  "_version" : 7,
  "result" : "updated",
  "_shards" : {
    "total" : 3,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 6,
  "_primary_term" : 1
}
```


```bash
POST /products/_update/100 
{
  "script": {
    "source": """
      if (ctx._source.in_stock == 0) {
        ctx.op = 'noop'
      }
      ctx._source.in_stock --;
    """
  }
}
```

```bash
POST /products/_update/100
{
  "script": {
    "source": """
      if (ctx._source.in_stock == 0) {
        ctx._source.in_stock --; 
      }
    """
  }
}
```

```bash
POST /products/_update/100
{
  "script": {
    "source": """
      if (ctx._source.in_stock <= 1) {
        ctx.op = 'delete'
      }
      ctx._source.in_stock --;
    """
  }
}
```

```bash
PUT /products/_update/101
{
  "script": {
    "source": "ctx._source.in_stock ++";
  },
  "upsert": {
    "name": "Blender",
    "price": 355,
    "in_stock": 12
  }
}
```

Response:

```json
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "101",
  "_version" : 1,
  "result" : "created",
  "_shards" : {
    "total" : 3,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 9,
  "_primary_term" : 1
}
```


```bash
GET PUT /products/_doc/100
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "101",
  "_version" : 2,
  "_seq_no" : 10,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "name" : "Blender",
    "price" : 355,
    "in_stock" : 13
  }
}
```


> Replacing documents with the index API
```bash
PUT /products/_doc/100
{
  "name": "Toaster",
  "price": 45,
  "in_stock": 5
}
```

- `GET /products/_doc/100`

- `DELETE /products/_doc/100`


When we index a document, elasticsearch uses a simple formula to calculate which shard the document should be stored.

Formula:
shard_num = hash(_routing) % num_primary_shards

This value equals the document id. The same applies for update and delete documents.

Routing value is a string that is either provided by the application or generated by elasticsearch.

Searching for some documents based on some criteria other than id works differently.

- Routing is 100% transparent when using the elasticsearch
- It is possible to customize the routing.



Ex:

```json
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "101",
  "_version" : 2,
  "_seq_no" : 10,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "name" : "Blender",
    "price" : 355,
    "in_stock" : 13
  }
}
```

Elasticsearch stores a bit of metadata along with document that we index.
The actual data is specified under _source field in the response.
The _id is the document identifier.
The default routing strategy uses the field _id, we will not see the _routing field as part of this response.
It will appear when we use custom routing.

Note: The number of shards cannot be changed once the index is created. The number of replicas can be changed at any time. 

As num of shards is used in below formula, so it cannot be changed once the index is created.
shard_num = hash(_routing) % num_primary_shards
It will not cause issue in indexing new documents but it will cause issue in searching the exisiting documents.



## How Elasticsearch reads data

Initially, a given node receives the request. The node is responsible for coordinating the request, and is therefore referred to as coordinating node.

The first step is to figure out where the document we are looking for is stored. As we know, it is done with routing.
Routing resolves to a shard that stores a given document.

- If elasticsearch regtrieves the document from the primary shard, all retreivals will end up in the same shard which doesn't scale well.
- Instead a shard is chosen from the replication group.
- Elasticsearch uses a technique called Adaptive replica selection(ARS) for this purpose.
- It actually selects the shard copy that is most available at the time of the request. This is evaluated by a formula that takes number of factors into the account.
- In short, it selects the shard copy that can yeild the best performance.
- Once a shard is selected, the coordinating node sends a request to that shard. 

The client will typically be an application using one of the elasticsearch sdks but it could be kibana or my dev machine.


## How Elasticseach writes data

- The request goes through the routing process as discussed earlier.
- The request is resolved to the replication group that stores or should store the document.
- Instead of routing the request to any of the shards in the replication group, write requests are always routed through the primary shard
- The primary shard is first responsible for validating the request.
  - This involves validating the structure of the requsts as well as validating the fields of the requests.
  - For instance, an attempt to add an object for a numeric field would cause a validation error
- The primary shard performs the write operation locally before forwarding it to the replica shards to keep up to date those as well.
- To improve the performance, the primary shard forwards the operation to its replica shards in parallel.
  - The operation will succeed even if the operation is not succeeded in the replica shards.

- Since elasticsearch is distributed and many operations happen asynchronously, a lot of things can go wrong such as hardware failurs.
- For example, suppose we index a new document. The primary shards validates the operation and index the document locally. There are two replica shards in the replication group and the primary shard sends the operation to both. The operation reaches to only one of the replica shard before the primary shard goes down, perhaps due to the hardware failure. When this happens the elasticseach goes for recovery process. It involves one of the replica shard being promoted to a new primary shard because in each replication group must have a primary shard. The problem here now is that two remaining shards do not share the same state, because one of them indexed the new document, while the other didn't. The replica shard that didn't receive the index operation, thinks its up to date but that's not the case.
The document will be found only half of the time depending on the shards that are selected. This is called split brain problem. 

Elasticsearch solves this and a number of other issues with something called primary terms and sequence number.

### Primary Terms:
  - A way to distinguish between the old and the new primary shards when the primary shard of the replication group has changed.
  - It is essentially a counter for how many times the primary shard has changed.
  - The primary term is appended to the write operations
    - In the prev example, the primary term value will be increased by 1 because the primary shard failed and a new primary shard was elected.
  - The primary terms for all replication groups are persisted in the cluster's state.
  - As part of write operations, the current primary term is appended to the operations that are sent to the replica shards.
  - This enables the replica shards whether or not the primary shard has changed since the operation was forwarded.

### Sequence Number:

  - Apart from associating each operation with a primary term, each operation is also associated with a sequence number. 
  - These sequence number is just a counter that is incremented for each operations(write) atleast until the primary shard changes.
  - Enables elasticsearch to order write operations.


### Recovering when the primary shards fails

  - Primary terms and sequence numbers are key when elasticsearch needs to recover from a primary shard failure, for instance due to networking error.
    - Instead of comparing data on disks, it can use primary terms and sequence number to figure out which operations have already been performed and which are needed to bring the replica shards up to date.
  - When the primary shard fails, the replica shards will continue to serve read requests.

### Global and local checkpoint
  - Essentially a sequence number
  - A global checkpoint is the sequence number that all active shards within a replication group have been aligned at least up to.
  - This means that any operations containing a sequence number lower than the global checkpoint have already been performed on all shards within the replication group.
  - If the primary shards fails and rejoins the cluster at a later point, elasticsearch needs to compare only the operations that are above the global checkpoint that it last knew about.
  - Likewise, if the replica shards fails and rejoins the cluster, it needs to compare only the operations that are above the local checkpoint that it last knew about.



## Introduction to versioning

- It is not a revision history of the documents
- Elasticsearch stores an _version field as metadata with every document
  - It is incremented by 1 for each operation that changes the document
- Elasticsearch will retain the version number for 60 seconds after the document is deleted
- If we index the document with the same ID within 60 seconds, the version number will be incremented by 1, otherwise it will be reset to 1
  - Configured with the index.gc_deletes setting

- The version number is used to ensure that the correct version of the document is updated
- The version number is also used to ensure that the correct version of the document is deleted
- The version number is also used to ensure that the correct version of the document is retrieved

This is the default type of versioning that is called internal versioning.

- Elasticsearch also supports external versioning. 
- This is useful when versions are maintained outside of elasticsearch such as within the database.

EX:

```bash
PUT /products/_doc_/101?version=531&version_type=external
{
  "name": "Blender",
  "price": 355,
  "in_stock": 12
}
```

### Point of using versioning
- we can tell how many times a document has been updated
- versioning is hardly used anymore
- it is used to implement optimistic concurrency control
- It was previously the way to do optimistic concurrency control
  - Now there is a better way


## Optimistic concurrency control

- Way to prevent overwriting documents invertently due to concurrent operations.
- Scenarios:
  - Eg. Handling concurrent visitors for a web application

- Old way of doing optimistic concurrency control
  - Using versioning
    - Sending _version in response after modifying the document
    - if the version number is different from the one we sent, we know that the document has been modified by someone else and we can retry the operation

- New way of doing optimistic concurrency control is using primary terms and sequence number
  - We can use the primary term and sequence number to determine whether the document has been modified by someone else

> Ex: 

```bash
  PUT /products/_update/101?if_seq_no=10&if_primary_term=1
  {
    "script": {
      "source": "ctx._source.in_stock += params.quantity",
      "params": {
        "quantity": 4
      }
    }
  }
```

  - Elasticsearch will use these two values if_seq_no and if_primary_term to ensure we dont overwrite a document invertently if it has changed since we retreived it.
  - If that happen, the operations will fail and we can try the process again.

```json
  {
    "_index" : "products",
    "_type" : "_doc",
    "_id" : "100",
    "_version" : 9,
    "_seq_no" : 8, // sequence number
    "_primary_term" : 1,  // primary term
    "found" : true,
    "_source" : {
      "name" : "Toaster",
      "price" : 45,
      "in_stock" : 4,
      "tags" : [
        "electronics",
        "trending"
      ]
    }
  }
  ```

```bash
POST /products/_update/100?if_seq_no=8&if_primary_term=1
{
  "doc" {
    "in_stock": 123
  }
}
```

Response:

```json
{
  "_index" : "products",
  "_type" : "_doc",
  "_id" : "100",
  "_version" : 10,
  "_seq_no" : 11, // sequence number changed
  "_primary_term" : 4, // primary term changed
  "found" : true,
  "_source" : {
    "name" : "Toaster",
    "price" : 45,
    "in_stock" : 123,
    "tags" : [
      "electronics",
      "trending"
    ]
  }
}
```

**Request:**

```bash
POST /products/_update/100?if_seq_no=8&if_primary_term=1
{
  "doc" {
    "in_stock": 123
  }
}
```

**Error:**

```json
{
  "error" : {
    "root_cause" : [
      {
        "type" : "version_conflict_engine_exception",
        "reason" : "[100]: version conflict, required seqNo [8], primary term [1]. current document has seqNo [11] and primary term [4]",
        "index_uuid" : "LQF31ri9TMeklo9hlYJGLA",
        "shard" : "0",
        "index" : "products"
      }
    ],
    "type" : "version_conflict_engine_exception",
    "reason" : "[100]: version conflict, required seqNo [8], primary term [1]. current document has seqNo [11] and primary term [4]",
    "index_uuid" : "LQF31ri9TMeklo9hlYJGLA",
    "shard" : "0",
    "index" : "products"
  },
  "status" : 409
}
```

> Note: Elasticsearch will reject the write operation if it contains the wrong primary term or sequence number.


## Update by Query
- Updating multiple documents within a single query

> Below query will update all the documents that matches the query

```bash
POST /products/_update_by_query
{
  "script": {
    "source": "ctx._source.in_stock --"
  },
  "query": {
    "match_all": {}
  }
}
```

Response:
```json
{
  "took" : 48,
  "timed_out" : false,
  "total" : 3,
  "updated" : 3,
  "deleted" : 0,
  "batches" : 1,
  "version_conflicts" : 0,
  "noops" : 0,
  "retries" : {
    "bulk" : 0,
    "search" : 0
  },
  "throttled_millis" : 0,
  "requests_per_second" : -1.0,
  "throttled_until_millis" : 0,
  "failures" : [ ]
}
```

- Before performing the bulk update, elasticsearch takes the snapshot of the documents.
- Then the search query is sent to each of the index's shards
- When the search query matches any documents, a bulk request is sent to update those documents.
- A query may match thousands of documents. Each pair of search and bulk requests are sent sequentially, i.e one at a time
- The reason for not doing everything simultaneously is related to how errors are handled.
- If an error occurs for any search or bulk query, Elastisearch will automatically retries upto 10 times
- If the affected query is still not successful, the whole query will be aborted.
- The failures will then be specified in the results, within the "failures" key
- Its important to check if the query is aborted or rollbacked.


### How the snapshots are used:
- Prevents overwriting changes made after the snapshot was taken
- When the elasticsearch is requested to update a given document, it uses the document's primary term and sequence number from the snapshot to ensure that the document has not been modified since the snapshot was taken.
- If the document has been modified, there will be a version conflict causing the document to not be updated
- The number of version conflicts will be returned under the "version_conflicts" key in the response

- If you want to proceed with the conflict then you can pass the conflicts=proceed parameter in the request.

Example:

#### Updating multiple documents with conflicts=proceed

```bash
POST /products/_update_by_query
{
  "conflicts": "proceed",
  "script": {
    "source": "ctx._source.in_stock --"
  },
  "query": {
    "match_all": {}
  }
}
```

```bash
GET /products/_search
{
  "query": {
    "match_all": {}
  }
}
```

#### Deleting multiple documents
```bash
POST /products/_delete_by_query
{
  "query": {
    "match_all": {}
  }
}
```

Response:
```json
{
  "took" : 15,
  "timed_out" : false,
  "total" : 3,
  "deleted" : 3,
  "batches" : 1,
  "version_conflicts" : 0,
  "noops" : 0,
  "retries" : {
    "bulk" : 0,
    "search" : 0
  },
  "throttled_millis" : 0,
  "requests_per_second" : -1.0,
  "throttled_until_millis" : 0,
  "failures" : [ ]
}
```

### Introduction to Bulk API

- Bulk API is used to perform multiple operations in a single request
- Bulk API accepts data formatted as newline-delimited JSON (NDJSON) specification
- Ex:
  action_and_meta_data\n
  optional_source\n
  action_and_meta_data\n
  optional_source\n
  ...

```bash
POST /_bulk
{ "index": { "_index": "products", "_id": 200 }}
{ "name": "Expresso Machine", "price": 199, "in_stock": 5}
{"create": { "_index": "products", "_id": 201 }}
{ "name": "Grinder Machine", "price": 250, "in_stock": 13}
```

Response:

```json
{
  "took" : 7,
  "errors" : false,
  "items" : [
    {
      "index" : {
        "_index" : "products",
        "_type" : "_doc",
        "_id" : "200",
        "_version" : 1,
        "result" : "created",
        "_shards" : {
          "total" : 3,
          "successful" : 1,
          "failed" : 0
        },
        "_seq_no" : 4,
        "_primary_term" : 4,
        "status" : 201
      }
    },
    {
      "create" : {
        "_index" : "products",
        "_type" : "_doc",
        "_id" : "201",
        "_version" : 1,
        "result" : "created",
        "_shards" : {
          "total" : 3,
          "successful" : 1,
          "failed" : 0
        },
        "_seq_no" : 5,
        "_primary_term" : 4,
        "status" : 201
      }
    }
  ]
}
```

> For running bulk query for documents under all indexes

```bash
POST /_bulk
{ "update": { "_index": "products", "_id": 200 }}
{ "doc": { "price": 234 }}
{ "delete": { "_index": "products", "_id": 200 }}
```

> For Running bulk query for documents under specific index

```bash
POST /products/_bulk
{ "update": { "_id": 200 }}
{ "doc": { "price": 234 }}
{ "delete": { "_id": 200 }}
```

NOTE:
* The HTTP Content-Type header is set to application/x-ndjson
* application/json is accepted as well but that's not the recommended way
* A failed action will not stop the rest of the actions from being processed
* The bulk API returns a response for each action
  * Inspect the item key to determine whether the action was successful or not
  * The errors are conveniently returned under the errors key


Bulk API examples:

Request:
```bash
POST /_bulk
{ "index": { "_index": "products", "_id": 200 }}
{ "name": "Expresso Machine", "price": 199, "in_stock": 5}
{"create": { "_index": "products", "_id": 201 }}
{ "name": "Grinder Machine", "price": 250, "in_stock": 13}
```

Response:


```json
{
  "took" : 7,
  "errors" : false,
  "items" : [
    {
      "index" : {
        "_index" : "products",
        "_type" : "_doc",
        "_id" : "200",
        "_version" : 1,
        "result" : "created",
        "_shards" : {
          "total" : 3,
          "successful" : 1,
          "failed" : 0
        },
        "_seq_no" : 4,
        "_primary_term" : 4,
        "status" : 201
      }
    },
    {
      "create" : {
        "_index" : "products",
        "_type" : "_doc",
        "_id" : "201",
        "_version" : 1,
        "result" : "created",
        "_shards" : {
          "total" : 3,
          "successful" : 1,
          "failed" : 0
        },
        "_seq_no" : 5,
        "_primary_term" : 4,
        "status" : 201
      }
    }
  ]
}
```


Request:
```bash
POST /_bulk
{ "update": { "_index": "products", "_id": 200 }}
{ "doc": { "price": 234 }}
{ "delete": { "_index": "products", "_id": 200 }}
```

Response:

```json
{
  "took" : 7,
  "errors" : false,
  "items" : [
    {
      "update" : {
        "_index" : "products",
        "_type" : "_doc",
        "_id" : "200",
        "_version" : 2,
        "result" : "updated",
        "_shards" : {
          "total" : 3,
          "successful" : 1,
          "failed" : 0
        },
        "_seq_no" : 6,
        "_primary_term" : 4,
        "status" : 200
      }
    },
    {
      "delete" : {
        "_index" : "products",
        "_type" : "_doc",
        "_id" : "200",
        "_version" : 3,
        "result" : "deleted",
        "_shards" : {
          "total" : 3,
          "successful" : 1,
          "failed" : 0
        },
        "_seq_no" : 7,
        "_primary_term" : 4,
        "status" : 200
      }
    }
  ]
}
```


## When to use Bulk API

- When we need to index a large number of documents
- When we need to update a large number of documents
- When we need to delete a large number of documents
- When we need to perform multiple operations in a single request
- When you need to perform a lot of write request in the same time
- The Bulk API is more efficient than sending individual write requests


1. Routing is used to resolve a document's shard
2. The bulk API supports optimistic concurrency control
  - Include the if_primary_term and if_seq_no parameters within the action metadata


## Mapping and Analysis

- Sometimes referred to as text analysis
- Applicable fo text fields/values
- Text values are analyzed when indexing the documents
- The result is stored in data structures that are efficient for searching etc.
- The _source object is not used when searching for documents
  - It contains the exact values specified when indexing a document


### Analyzer
- It consists of three building blocks
  - Character filters
    - It receives the original text and it adds, removes and changes characters 
    - It can have 0 or more character filters 
    - They are applied in the same order in which it is specified 
    - Used to preprocess the text before it is tokenized - optional
    - Ex: HTML stripping   -  removing HTML tags from the text
    - Ex: Replacing characters  - replacing characters with other characters. Ex: replacing & with and

  - Tokenizer : Analyzer contains 1 tokenizer 
    - Splits the text into tokens
    - 
    - Ex: Splitting text into words - 
    - Ex: Splitting text into sentences

  - Token filters - optional
    - Used to modify the tokens - lowercase, stemming, synonyms - before they are indexed
    - Ex: Lowercasing tokens  - converting all characters to lowercase. Ex: Hello -> hello
    - Ex: Removing stopwords  - words that are not useful for searching. Ex: a, an, the, is, are, etc.
    - Ex: Stemming tokens - reducing words to their root form. Ex: running, ran, run are all reduced to run



### Inverted Indices:

#### Intro
- It is a data structure that is used to efficiently search for text values
- A field's values are stored in one of the several data structures
  - The data structure depends on the field's data type
- Ensure efficient data access - e.g. searches
- Handled by apache lucene and not elasticsearch

### Detail:

- It is mapping between terms and which documents contain them
- Outside the context of analyzers, we use the terminology "terms"

- Terms are sorted alphabetically
- Each term is associated with a list of documents that contain the term
- Inverted indices contain more than just terms and document IDs
  - E.g - Information for relevance scoring
- One inverted index per text field
- Other data type uses BKD trees, for instance


Summary:

- Values for a text field are analyzed and the results are stored within an inverted index
- Each field has a dedicated inverted index
- An inverted index is a mapping between terms and which documents contain them
- Terms are sorted alphabetically for performance reasons
- Created and maintained by Apache lucene, not elasticsearch

- Inverted indices enable fast searches
- Inverted indices contains other data as well
    - E.g things used for relevance scoring
- Elasticsearch(apache lucene) uses other data structure as well
    - E.g BKD trees for numeric values, dates, and geospatial data

### Mapping

- Defines the structures of the document (fields and data types)
    - Also used to configure how values are indexed
- Similar to tables schema in a relational database
- Explicit mapping
    - We define field mappings ourselves
- Dynamic mapping
    - Elasticsearch generates field mapping for us


### Data types

- object data type
    - Used for any json object
    - Objects may be nested
    - Mapped using the properties parameter
    - Objects are not stored as objects in Apache lucene
      - Objects are transformed to ensure that we can index any valid JSON
      - In particular, objects are flattened
    - In the objects are arrays, then the arrays are flattened as well. 
      - For example: below json shows the array of objects
      -
        ```json
        "tags": [
        {
          "name": "electronics",
          "rank": 1
        },
        {
          "name": "trending",
          "rank": 2
        }
      ]
      ```
      - The above json will be flattened as below
      - "tags.name": ["electronics", "trending"]
      - "tags.rank": [1, 2]
      - The above flattening is done to ensure that we can search for any value in the array
      - But if we want to perform AND condition in search query then we need to use nested data type
      - If we want to perform OR condition in search query then we can use flattened data type

- Nested data type
      - Similar to the object data type, but maintains object relationships
          - Useful when indexing arrays of objects
      - Enables us to query objects independently
          - must use the nested query
      - Nested objects are stored as hidden documents

- Keyword data type
      - Used for exact matching of values
      - Typically used for filtering, aggregations, and sorting
      - E.g. Searching for articles with a status of PUBLISHED
      - For full-text search, use the text data type instead
          - e.g. searching the body text of an article

### Working of keyword data type
  
- keyword fields are analyzed with the keyword analyzer
- The keyword analyzer is a no-op analyzer
- It outputs the unmodified string as a single token
- * E.g. of keyword data type
      
  ```json
  {
    "name": "This is a test string for keyword data type",
    "price": 45,
    "in_stock": 3,
    "tags": ["electronics", "trending"]
  }
  ```
      
- The above json will be indexed as below
  
  ```json
  {
    "name": "This is a test string for keyword data type",
    "name.keyword": "This is a test string for keyword data type",
    "price": 45,
    "in_stock": 3,
    "tags": ["electronics", "trending"],
    "tags.keyword": ["electronics", "trending"]
  }
  ```

### Type Coercion

- Data types are inspected when indexing documents
      - They are validated, and some invalid values are rejected 
      - E.g. trying to index an object for a text field
      - Sometimes, providing the wrong data type is okay


Ex:

```json
{
  "_index" : "coercion_test",
  "_type" : "_doc",
  "_id" : "2",
  "_version" : 1,
  "_seq_no" : 1,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "price" : "5.6"
  }
}
```

### Understanding the _source key
- Contains the values that were supplied at the index time("7.4")
- * Not the values that are indexed(7.4)
- Search queries use indexed_values, not _source
- * BKD trees, inverted indices, etc
- _source does not reflect how values are indexed
- * E.g. the value "7.4" is indexed as 7.4
- * In this example, it might be either string or floating point

- Supplying a floating point for an integer field will truncate it to an Integer
- Coercion is not used for dynamic mapping
- * Supplying "7.4" for a new field will create a text mapping

- Always try to use the correct data type
- * Especially the first time you index a field

- Disabling coercion is a matter of preference
- * Enabled by default


### Arrays

- There is no such things as an array data type
- Any field may contain zero or more values
    - No configuration or mapping needed
    - Simply supply an array of values when indexing a document


> Ex:

```bash
POST /_analyze
{
  "text": ["Strings are simply", "merged together."],
  "analyzer": "standard"
}
```

Response:

```json
{
  "tokens" : [
    {
      "token" : "strings",
      "start_offset" : 0,
      "end_offset" : 7,
      "type" : "<ALPHANUM>",
      "position" : 0
    },
    {
      "token" : "are",
      "start_offset" : 8,
      "end_offset" : 11,
      "type" : "<ALPHANUM>",
      "position" : 1
    },
    {
      "token" : "simply",
      "start_offset" : 12,
      "end_offset" : 18,
      "type" : "<ALPHANUM>",
      "position" : 2
    },
    {
      "token" : "merged",
      "start_offset" : 19,
      "end_offset" : 25,
      "type" : "<ALPHANUM>",
      "position" : 3
    },
    {
      "token" : "together",
      "start_offset" : 26,
      "end_offset" : 34,
      "type" : "<ALPHANUM>",
      "position" : 4
    }
  ]
}
```

- Here, start_offset and end_offset are the positions of the tokens in the text
- position is the position of the token in the array

#### Constraint
- Array values should be of the same data type
- Coercion only works for fields that are already mapped
- Arrays may contain nested values
- Arrays are flattened during indexing

Note: Remember to use the nested data type for arrays of objects if you need to query the objects separately


> Index mapping

```bash
PUT /reviews
{
  "mappings": {
    "properties": {
      "rating": {"type": "float"},
      "content": {"type": "text"},
      "product_id": {"type": "integer"},
      "author": {
        "properties": {
          "first_name": {"type": "text"},
          "last_name": {"type": "text"},
          "email": {"type": "keyword"}
        }
      }
    }
  }
}
```

Sample document based on above mapping:

```bash
POST /reviews/_doc/1
{
  "rating": 4.5,
  "content": "I love this product!",
  "product_id": 1,
  "author": {
    "first_name": "John",
    "last_name": "Smith",
    "email": "johnsmith@abc.com"
  }
}
```


- `GET /reviews/_mapping`
- `GET /reviews/_mapping/field/author.email`
- `GET /reviews/_mapping/field/content`

```bash
PUT /review_dot_notation
{
  "mappings": {
    "properties": {
      "rating": {"type": "float"},
      "content": {"type": "text"},
      "product_id": {"type": "integer"},
      "author.first_name": {"type": "text"},
      "author.last_name": {"type": "text"},
      "author.email": {"type": "keyword"}
    }
  }
}
```


- `GET /review_dot_notation/_mapping`

```bash
PUT /reviews/_mapping
{
  "properties": {
    "created_at": {"type": "date"}
  }
}
```

GET /reviews/_mapping


### Default behavior of date fields

- Three supported formats
    - a date without time
      - Ex:
      ```json
      {
        "created_at": "2019-01-01"
      }
      ```
    - a date with time
      - Ex:
      ```json
      {
        "created_at": "2019-01-01T12:30:45"
      }
      ```
    - milliseconds since the epoch(long)
      - Ex:
      ```json
      {
        "created_at": 1546300800000
      }
      ```
- UTC timezone assumed if none is specified
- Dates must be formatted according to the ISO 8601 specification

### How date fields are stored

- Stored internally as milliseconds since the epoch(long)
- Any valid value that you supply at the index time is converted to a long value internally
- Dates are converted to UTC timezone
- The same date conversion happens for search queries, too


> Example with a date without time

```bash
PUT /reviews/_doc/2
{
  "rating": 4.5,
  "content": "I love this product!",
  "product_id": 1,
  "created_at": "2019-01-01"
  "author": {
    "first_name": "John",
    "last_name": "Smith",
    "email": "clay@abc.com"
}
```

> Example with a date with time

```bash
PUT /reviews/_doc/3
{
  "rating": 4.5,
  "content": "I love this product!",
  "product_id": 1,
  "created_at": "2019-01-01T12:30:45"
  "author": {
    "first_name": "John",
    "last_name": "Smith",
    "email": "john@abc.com"
  }
}
```

> Example with milliseconds since the epoch

```bash
PUT /reviews/_doc/4
{
  "rating": 4.5,
  "content": "I love this product!",
  "product_id": 1,
  "created_at": 1546300800000
  "author": {
    "first_name": "John",
    "last_name": "Smith",
    "email": "smith@abc.com"
  }
}
```

### Missing fields

- All fields in Elasticsearch are optional
- We can leave out a field while indexing documents
- E.g. unlike relational database where we need to allow NULL
- Some integrity checks need to be done at the application level
- * e.g. having required fields
- Adding a field mapping does not make a field required
- Searches automatically handle missing fields


### Mapping parameters

#### * format parameter

* - Used to customize the format of date fields
* - I recommend using the default format whenever possible
* - - "strict_date_optional_time||epoch_millis"
* - - "yyyy/MM/dd HH:mm:ss||yyyy/MM/dd"
* - - "yyyy/MM/dd HH:mm:ss||yyyy/MM/dd||epoch_millis"
* - - "yyyy/MM/dd HH:mm:ss||yyyy/MM/dd||epoch_millis||strict_date_optional_time"
* - - "yyyy/MM/dd HH:mm:ss||yyyy/MM/dd||epoch_millis||strict_date_optional_time||epoch_second"
* - Using Java's Dateformatter syntax
* - - E.g. "yyyy/MM/dd HH:mm:ss||yyyy/MM/dd||epoch_millis||strict_date_optional_time||epoch_second"
* - Using build-in formats
* - - e.g. "strict_date_optional_time||epoch_millis"
* - - e.g. "epoch_second"

#### * properties parameter

* - Used to define object mappings

* - - E.g. "properties": {"author": {"properties": {"first_name": {"type": "text"}}}}
* - Defines nested fields for object and nested fields

```bash
PUT /sales
{
  "mappings": {
    "properties": {
      "created_at": {
        "type": "date",
        "format": "yyyy/MM/dd HH:mm:ss||yyyy/MM/dd||epoch_millis||strict_date_optional_time||epoch_second"
      },
      "author": {
        "properties": {
          "first_name": {"type": "text"},
          "last_name": {"type": "text"},
          "email": {"type": "keyword"}
        }
      }
    }
  }
}
```

* - Example of nested fields

```bash
PUT /sales
{
  "mappings": {
    "properties": {
      "products": {
        "type": "nested",
        "properties": {
          "name": {"type": "text"},
          "price": {"type": "float"},
          "in_stock": {"type": "integer"}
        }
      }
    }
  }
}
```

#### * coerce parameter

* - Used to enable or disable coercion of values (enabled by default)
* - - E.g. "coerce": false

Ex:

```bash
PUT /coercion_test
{
  "mappings": {
    "properties": {
      "price": {
        "type": "integer",
        "coerce": false
      }
    }
  }
}
```

```bash
PUT /sales
{
  "settings: {
    "index.mapping.coerce": false
  },
  "mappings": {
    "properties": {
      "price": {
        "type": "integer",
        "coerce": true
      }
    }
  }
}
```

#### * doc_value parameter

* - Used to enable or disable doc values (enabled by default)
* - Elasticsearch makes use of several data structures to enable fast searches

* - - No single data structure is suitable for all use cases

* - Enabled indices are excellent for searching text
* - - They don't perform well for many other data access patterns

* - "doc_values" is another data structure used by apache lucene
* - - Optimized for a different data access pattern (document -> terms)

* - It is an "uninverted" inverted index
* - Used for sorting, aggregation, and scripting
* - An additional data structure, not a replacement
* - Elasticsearch automatically queries the appropriate data structure

* Disabling doc values reduces disk usage
* - But it also disables sorting, aggregations, and scripting
* - Also, slightly increases the indexing throughput

* Only disable doc_values if you won't use aggregation, sorting and scripting
* - E.g. for logging use cases
* Particularly useful for large indices; typically not worth it for small ones
* - E.g. 100 million documents with 10 fields // example of large index

* Cannot be changed without reindexing documents into new index
* - Use with caution, and try to anticipate how fields will be queried

>  doc_value parameter example
  
  ```bash
  PUT /sales
  {
    "mappings": {
      "properties": {
        "price": {
          "type": "integer",
          "doc_values": false
        }
      }
    }
  }
  ```

  #### * norms

  * Normalization factor used for relevance scoring
  * - Disabled by default
  * - - E.g. "norms": false

  * Often we don't want to filter results, but also ranks them

  * Norms can be disabled to save disk space
  * - Useful for fields that won't be used for relevance scoring
  * - The fields can still be used for filtering and aggregations


> norms example

```bash
PUT /sales
{
  "mappings": {
    "properties": {
      "price": {
        "type": "integer",
        "norms": false
      }
    }
  }
}
```

#### * index parameter

* Disbles indexing for a field
* Values are still stored within _source
* Useful if you won't use the field for search queries
* Saves disk space and slightly improves indexing throughput
* Often used for time series data
* Fields with indexing disabled can still be used for aggregations


> Examples: 

```bash
  PUT /server-metrics
  {
    "mappings": {
      "properties": {
        "cpu": {
          "type": "float",
          "index": false
        },
        "memory": {
          "type": "float",
          "index": false
        },
        "disk": {
          "type": "float",
          "index": false
        },
        "timestamp": {
          "type": "date"
        }
      }
    }
  }
```


#### * null_value parameter

* NULL values are not indexed by default and are not searchable
* Use this value to replace NULL values with a different value
* Only works with explicit null values
* The replacement must be of the same data type as the field
* Doesn't affect the values stored in _source

> null_value parameter example

```bash
PUT /sales
{
  "mappings": {
    "properties": {
      "partner_id": {
        "type": "keyword",
        "null_value": "NULL"
      }
    }
  }
}
```

#### * copy_to parameter

* Used to copy multiple field values into a "group field"
* Simply specify the name of the target field as the value
* E.g. first_name and last_name -> full_name
* values are copied, not terms/tokens
* - The analyzer of the target field is used for the values
* The target field is not part of _source


> Example of copy_to parameter

```bash
PUT /sales
{
  "mappings": {
    "properties": {
      "first_name": {
        "type": "text",
        "copy_to": "full_name"
      },
      "last_name": {
        "type": "text",
        "copy_to": "full_name"
      },
      "full_name": {
        "type": "text"
      }
    }
  }
}
``` 

```bash
POST /sales/_doc
{
  "first_name": "John",
  "last_name": "Smith"
}
```

### Updating existing field mappings

* Suppose that product IDs now include letters
* We need to change the product_id field's data type to either text or keyword
* - We won't use the field or full text searches
* - We will use it for filtering, so the keyword data type is ideal


Ex:

```bash
PUT /reviews/_mapping
{
  "properties": {
    "product_id": {"type": "keyword"}
  }
}
```

```bash
PUT /reviews/_mapping
{
  "properties": {
    "author": {
      "properties": {
        "email": {"type": "keyword"},
        "ignore_above": 256
      }
    }
  }
}
```

### Reindexing Documents with the Reindex API
```bash
PUT /reviews_new
{
  "mappings": {
    "properties": {
      "product_id": {"type": "keyword"},
      "author": {
        "properties": {
          "email": {"type": "keyword"},
          "ignore_above": 256
        },
        "first_name": {"type": "text"},
        "last_name": {"type": "text"}
      },
      "created_at": {
        "type": "date",
        "format": "yyyy/MM/dd HH:mm:ss||yyyy/MM/dd||epoch_millis||strict_date_optional_time||epoch_second"
      },
      "content": {"type": "text"},
      "rating": {"type": "float"}
      "product_id": {"type": "keyword"}
    }
  }
}
```

```bash
GET /reviews/_mapping
```

```bash
POST /_reindex
{
  "source": {
    "index": "reviews"
  },
  "dest": {
    "index": "reviews_new"
  }
}
```


```bash
GET /reviews_new/_search
{
  "query": {
    "match_all": {}
  }
}
```

```bash
GET /reviews_new/_delete_by_query
{
  "query": {
    "match_all": {}
  }
}
```

```bash
POST /_reindex
{
  "source": {
    "index": "reviews"
  },
  "dest": {
    "index": "reviews_new"
  },
  "script": """
      if(ctx._source.product_id != null) {
        ctx._source.product_id = ctx._source.product_id.toString();
      }
  """
}
```


### Batching and Throttling

- The Reindex APIs performs operations in batches
  - Just like the Update by query and delete by query APIs
  - It uses the Scroll API internally
  - This is how millions of documents can be reindexd efficiently

- Throttling can be configured to limit the performance impact
  - Useful for production clusters


- - The default batch size is 1000 documents

### Defining field aliases

- Field names can be changed when reindexing document
- - Not worth it for lots of documents
- An alternative is to use field aliases
- - Doesn't require documents to be reindexed
- Lets add one pointing from comment to content
- Aliases can be used within queries
- Aliases are defined with a field mapping


#### Creating the alias

PUT /reviews/_mapping
{
  "properties": {
    "comment": {
      "type": "alias",
      "path": "content"
    }
  }
}


#### Using the alias

GET /reviews/_search
{
  "query": {
    "match": {
      "content": "great"
    }
  }
}


GET /reviews/_search
{
  "query": {
    "match": {
      "comment": "great"
    }
  }
}


- Field alias can actually be updated
- - Only its target field though
- Simply perform a mapping update with a new path value
- Possible because aliases don't affect indexing
- - Its a query level construct


### Multi field mapping

In Elasticsearch, a multi-field mapping is a way to index a field multiple times with different configurations to support various search use cases. This is particularly useful when you want to apply different analyzers, data types, or settings to the same field.

#### key concepts involved in multi-field mapping:

#### 1. Field Mapping:

A field in Elasticsearch represents a unit of data. For instance, if you have a field named name in your document, it can be mapped in multiple ways using multi-field mapping.

#### 2. Sub-Fields:

When you define a multi-field mapping, you create sub-fields under the main field. Each sub-field has its own settings, such as the analyzer, data type, and index options.
#### 3. Use Cases:

#### 3.1 Full-Text Search vs. Keyword Search:

You might want to perform full-text searches on a text field using analyzers like standard or english. Simultaneously, you might need the same field for exact keyword searches without any analysis. Multi-field mapping allows you to achieve both functionalities.

#### 3.2 Sorting and Aggregations:

For a field like timestamp, you might want to index it as a date type for sorting and date-based aggregations. Additionally, you may want to index it as a keyword to perform exact matches.

```bash
PUT /multi-field-mapping
{
  "mappings": {
    "properties": {
      "description": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword"
          }
        }
      },
      "ingredients": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword"
          }
        }
      }
    }
  }
}
```

#### 4. Examples:
Here's a simplified example of a multi-field mapping for a name field:

```json
"name": {
  "type": "text",
  "fields": {
    "keyword": {
      "type": "keyword",
      "ignore_above": 256
    }
  }
}

```

#### 5. Mapping Configuration:
The configuration of a multi-field mapping depends on your specific use case. You can define sub-fields with different types, analyzers, and other settings based on how you intend to search and analyze the data.
Here's a basic example of using a multi-field mapping in an index mapping:

```json
{
  "mappings": {
    "properties": {
      "title": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword",
            "ignore_above": 256
          }
        }
      }
    }
  }
}

```

### Index Template

```bash
PUT /_template/access-logs
{
  "index_patterns": ["access-logs-*"],
  "settings": {
    "number_of_shards": 2,
    "index.mapping.coerce": false
  },
  "mappings": {
    "properties": {"
      "ip_address": {"type": "ip"},
      "@timestamp": {"type": "date"},
      "url.original": {"type": "keyword"},
      "http.request.referrer": {"type": "keyword"},
      "http.response.status_code": {"type": "long"},
      "request": {"type": "text"},
      "response": {"type": "integer"},
      "user_agent": {"type": "text"}
    }
  }
}
```


```bash
PUT /access-logs-2020-01-01
```

```bash
GET /access-logs-2020-01-01
```

#### Response
```json
{
  "access-logs-2020-01-01" : {
    "aliases" : { },
    "mappings" : {
      "properties" : {
        "@timestamp" : {
          "type" : "date"
        },
        "http" : {
          "properties" : {
            "request" : {
              "properties" : {
                "referrer" : {
                  "type" : "keyword"
                }
              }
            },
            "response" : {
              "properties" : {
                "status_code" : {
                  "type" : "long"
                }
              }
            }
          }
        },
        "ip_address" : {
          "type" : "ip"
        },
        "request" : {
          "type" : "text"
        },
        "response" : {
          "type" : "integer"
        },
        "url" : {
          "properties" : {
            "original" : {
              "type" : "keyword"
            }
          }
        },
        "user_agent" : {
          "type" : "text"
        }
      }
    },
    "settings" : {
      "index" : {
        "routing" : {
          "allocation" : {
            "include" : {
              "_tier_preference" : "data_content"
            }
          }
        },
        "mapping" : {
          "coerce" : "false"
        },
        "number_of_shards" : "2",
        "provided_name" : "access-logs-2020-01-01",
        "creation_date" : "1701105292704",
        "number_of_replicas" : "1",
        "uuid" : "YBfnueGOQVCdfhNiXg2BJQ",
        "version" : {
          "created" : "7150099"
        }
      }
    }
  }
}
```


#### Priorities of Index Templates

- A new index can match multiple index templates
- The index template with the highest priority is used
- An order parameter can be used to change the priority of index templates
  - The value is simply an integer
  - The default value is 0
  - Templates with lower values are merged first

#### Updating Index Templates

```bash
PUT /_template/access-logs
{
  "index_patterns": ["access-logs-*"],
  "settings": {
    "number_of_shards": 2,
    "index.mapping.coerce": false
  },
  "mappings": {
    "properties": {
      "ip_address": {"type": "ip"},
      "@timestamp": {"type": "date"},
      "url.original": {"type": "keyword"},
      "http.request.referrer": {"type": "keyword"},
      "http.response.status_code": {"type": "long"},
      "request": {"type": "text"},
      "response": {"type": "integer"},
      "user_agent": {"type": "text"}
    }
  }
}
```

#### Retrieving Index Templates

```bash
GET /_template/access-logs
```

#### Deleting Index Templates

```bash
DELETE /_template/access-logs
```


### Elastic Common Schema (ECS)

The Elastic Common Schema (ECS) is a standardized and extensible approach for organizing and naming fields in Elasticsearch indices. It is designed to make it easier to analyze data from diverse sources consistently. ECS provides a common vocabulary and structure for event fields, making it simpler to correlate and analyze data across different systems.

### Key Concepts of ECS:

1. Field Naming Convention:

Fields in ECS follow a standardized naming convention. For example, event.module, source.ip, user.name, etc. The structure helps in easily identifying the purpose of each field.

2. Categorization:

ECS categorizes fields into common groups like agent, client, server, user, source, destination, event, etc. This grouping makes it clear which aspect of an event each field represents.

3. Versioning:

ECS versions are used to track changes to the schema over time. This helps users adapt to new versions while maintaining backward compatibility.

4. Extensibility:

While ECS provides a common set of fields, it is extensible. Users can add custom fields for their specific use cases while still adhering to the ECS structure.


> Notes:

- A specification for field names and data types and how they should be mapped
- Before ECS there was no cohesion between field names and data types
- Ingesting logs from nginx would give different field names than Apache

- ECS is a specification, not a mapping template

- ECS means than common fields are named the same thing
  - Ex: timestamp, url, user_agent, etc
- Use case independent
  - E.g. web server logs, firewall logs, etc
 - Groups of fields are referred to as field sets
   - E.g. http, url, user_agent, etc


#### Uses of ECS 
- In ECS, documents are referred to as Events
  - ECS doesn't provide fields for non-events (E.G PRODUCTS)
- Mostly useful for standard events
  - Ex: web server logs, firewall logs, etc
- ECS is automatically handled by Elastic Stack products
  - Ex: if you ingest the logs via fielbeat then it will automatically use ECS

#### Example:

Here's a simple example of ECS in action for an HTTP server log:
```json
{
  "@timestamp": "2023-01-01T12:34:56.789Z",
  "event": {
    "module": "nginx",
    "category": "web"
  },
  "source": {
    "ip": "192.168.1.1",
    "port": 80
  },
  "destination": {
    "ip": "10.0.0.1",
    "port": 443
  },
  "http": {
    "request": {
      "method": "GET",
      "referrer": "https://example.com",
      "user_agent": {
        "original": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
      }
    },
    "response": {
      "status_code": 200,
      "body": {
        "bytes": 1024
      }
    }
  },
  "user": {
    "name": "john_doe",
    "id": "12345"
  },
  "ecs": {
    "version": "1.8.0"
  }
}
```

In this example:

* @timestamp: Represents the timestamp of the event.
* event.module and event.category: Categorize the event as related to Nginx and falling under the "web" category.
* source and destination: Indicate the source and destination of the event (IP addresses and ports).
* http.request and http.response: Contain details about the HTTP request and response.
* user: Contains information about the user making the request.
* ecs.version: Specifies the ECS version used.

