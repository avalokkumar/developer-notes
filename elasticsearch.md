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


### Introduction to dynamic mapping

Dynamic mapping in Elasticsearch is the automatic process of defining the mapping for fields based on the data that is indexed. When you index a document and there is no predefined mapping for the index, Elasticsearch dynamically creates the mapping based on the data it encounters.

Here's an example to illustrate dynamic mapping:

Let's say you start indexing documents in an index without a predefined mapping. The first document may look like this:

```json
{
  "user": "John Doe",
  "age": 30,
  "location": {
    "lat": 40.7128,
    "lon": -74.0060
  }
}
```

In this case, Elasticsearch will dynamically create a mapping for the index based on the structure of this document. The mapping might look like:

```json
{
  "mappings": {
    "properties": {
      "user": {
        "type": "text"
      },
      "age": {
        "type": "long"
      },
      "location": {
        "properties": {
          "lat": {
            "type": "float"
          },
          "lon": {
            "type": "float"
          }
        }
      }
    }
  }
}

```

#### Note: 
- Elasticsearch ignores the long values for keyword mappings

> Ex:

```bash
PUT /my-index/_doc
{
  "tags": ["electronics", "trending"],
  "price": 45,
  "in_stock": 3,
  "created_at": "2019-01-01"
}
```

> Dynamically created mapping

```json
{
  "my-index" : {
    "mappings" : {
      "properties" : {
        "created_at" : {
          "type" : "date"
        },
        "in_stock" : {
          "type" : "long"
        },
        "price" : {
          "type" : "long"
        },
        "tags" : {
          "type" : "text",
          "fields" : {
            "keyword" : {
              "type" : "keyword",
              "ignore_above" : 256
            }
          }
        }
      }
    }
  }
}
```


### Combining explicite and dynamic mapping

- Explicit mapping takes precedence over dynamic mapping

```bash
PUT /people
{
  "mappings": {
    "properties": {
      "first_name": {"type": "text"}
    }
  }
}
```


```bash
GET /people/_mapping
```


```bash
PUT /people
{
  "mappings": {
    "dynamic": false,
    "properties": {
      "first_name": {"type": "text"}
    }
  }
}
```

```bash
POST /people/_doc
{
  "first_name": "John",
  "last_name": "Doe"
}
```

```bash
GET /people/_mapping
```
  
```bash
GET /people/_search
{
  "query": {
    "match": {
      "first_name": "John"
    }
  }
}
```

```bash
GET /people/_search
{
  "query": {
    "match": {
      "last_name": "Doe"
    }
  }
}
```

```bash
DELETE /people
```


#### Note:
- Setting dynamic to false
  - New Fields are ignored and not rejected
  - Doesn't affect existing fields
  - They are not indexed but part of _source object
- No inverted index is created for the last_name field
  - Querying the field gives no results
- Fields cannot be indexed without a mapping
  - When enabled, dynamic mapping creates one before indexing values
- New fields must be mapped explicitly



#### Strict mapping

```bash
PUT /people
{
  "mappings": {
    "dynamic": "strict",
    "properties": {
      "first_name": {"type": "text"}
    }
  }
}
```

```bash
POST /people/_doc
{
  "first_name": "John",
  "last_name": "Doe"
}
```

> Error

```json
{
  "error" : {
    "root_cause" : [
      {
        "type" : "strict_dynamic_mapping_exception",
        "reason" : "mapping set to strict, dynamic introduction of [last_name] within [_doc] is not allowed"
      }
    ],
    "type" : "strict_dynamic_mapping_exception",
    "reason" : "mapping set to strict, dynamic introduction of [last_name] within [_doc] is not allowed"
  },
  "status" : 400
}
```



### Dynamic Templates

```bash
PUT /dynamic_templates_test
{
  "mappings": {
    "dynamic_templates": [
      {
        "integer": {
          "match_mapping_type": "long",
          "mapping": {
            "type": "integer"
          }
        }
      }
    ]
  }
}
```


#### match and unmatch parameters

- Used to specify conditions for field names
- Field names must match the conditions specified by the match parameter
- unmatch is used to exclude fields that were matched by match parameter
- Both parameters support patterns with wildcards (*)
  - Hard coding field names wouldn't make any sense


#### path_match and path_unmatch

- These parameters evaluate the full field path
  -  i.e not just the field names
- This is the dot notation that you saw earlier
  - e.g. name.first_name
- wildcards are also supported



```bash
PUT /test_index
{
  "mappings": {
    "dynamic_templates": {
      "no_doc_values": {
        "match_mapping_type": "*",
        "mapping": {
          "type": "{dynamic_type}",
          "doc_values": false
        }
      }
    }
  }
}
```


- The purpose of above template is to set index parameter to false
- This example of disabling indexing could be used for timeseries data
- This is a common optimization for timeseries data where we don't need to filter on specific values but rather aggregate on time intervals
- Another optimization for timeseries data is to disable norms.



#### Index template vs dynamic templates

- Index templates apply mappings and index settings for matching indices
  - This happens when indicies are created and their names match a pattern

- Dynamic templates are evaluated when new fields are encountered
  - and dynamic mapping is enabled
  - The specific field mapping is added if the template condition match

- Index templates define fixed mappings, dynamic templates are dynamic


### Mapping recommendation

- Dynamic mapping is convenient, but often not a good idea in production
- Save disk space with optimized mappings when storing many documents
- Set dynamic to 'strict', and not 'false'
  - Setting it to false will enable us to add fields for which there are no mappings. The fields are then simply ignored in terms of indexing. Unexpected results


#### Mapping of text fields
- Don' always map strings as both text and keyword
  - Typically only one is needed
  - Each mapping requires disk space

- Do you need to perform full text searches on the field?
  - If yes, map it as text
  - If no, map it as keyword


#### Disable coercion
- Always use correct data type whenever possible
- Coercion is enabled by default
- - Supplying a floating point for an integer field will truncate it to an Integer
- - Supplying a string for an integer field will attempt to parse it as an integer
- - Supplying a string for a date field will attempt to parse it as a date


#### Use appropriate numeric data types
- For the whole numbers, integers data type might be enough
- - long can store larger numbers but requires more disk space

- For decimal numbers, float data type might be precise enough
- - double can store larger numbers but requires 2x disk space

#### Mapping parameters
- Set doc_values to false if you don't need sorting or aggregations and scripting
- Set norms to false if you don't need relevance scoring
- Set index to false if you don't need to search on the field values
- - You can still use the field for aggregations and Sorting. e.g. for time series data

- Probably only worth the effort when storing lots of documents
- - Otherwise it's probably an over complication
- Worst case scenario, you will need to reindex your documents



### Stemming and stop words


#### Stemming

- Stemming is the process of reducing a word to its root form
- - e.g. "running" -> "run", "swimming" -> "swim"


#### Stop words

- Words that are filtered out before or after processing of natural language data
- -  Common words such as "the", "a", "an", "in", "at", "on", "is", "are", "were", "was", "will", "would", "can", "could", "should", "of", "for", "to", "from", "with", "without", "and", "or", "not", "but", "this", "that", "these", "those", "my", "your", "his", "her", "their", "our", "its", "about", "after", "before", "between", "under", "over", "above", "below", "up", "down", "again", "then", "once", "here", "there", "where", "why", "how", "all", "any", "both", "each", "few", "more", "most", "other", "some", "such", "no", "nor", "too", "very", "same", "so", "than", "too", "very", "s", "t", "can", "will", "just", "don", "should", "now", etc

- They provide little to no value for search queries and also for relevance scoring
- Fairly common to remove such words
- - Less common in elasticsearch today than in the past
- - The relevance algorithm has been improved significantly
- Not removed by default and generally not recommended to remove it

---

### Analyzers and Search Queries

- Analyzers are used to process text before indexing
- - They are also used to process search queries


In Elasticsearch, analyzers and search queries are fundamental components for handling and searching data. Let's explore each concept:

### Analyzers in Elasticsearch:

An analyzer in Elasticsearch is a process that converts text into terms. It consists of three main parts: character filters, tokenizers, and token filters. Analyzers play a crucial role in breaking down text into individual terms, and they are essential for efficient searching.

#### Example Analyzer:

Here's a simple example of creating a custom analyzer named "my_analyzer" in Elasticsearch using the RESTful API:

```json
PUT /my_index
{
  "settings": {
    "analysis": {
      "analyzer": {
        "my_analyzer": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": ["lowercase", "my_synonym_filter"]
        }
      },
      "filter": {
        "my_synonym_filter": {
          "type": "synonym",
          "synonyms": ["quick, fast"]
        }
      }
    }
  }
}
```

In this example:
- We create an index named "my_index" with a custom analyzer named "my_analyzer."
- The analyzer uses the standard tokenizer and applies lowercase filtering.
- Additionally, we define a synonym filter to replace "quick" with "fast."

### Search Queries in Elasticsearch:

Search queries in Elasticsearch are used to retrieve data from the index. Elasticsearch supports a variety of queries for different use cases, such as term queries, match queries, bool queries, and more.

#### Example Search Query:

Here's an example of a simple search query using the RESTful API:

```json
GET /my_index/_search
{
  "query": {
    "match": {
      "description": "quick brown fox"
    }
  }
}
```

In this example:
- We search for documents in the "my_index" index where the "description" field contains the phrase "quick brown fox."

#### Combining Analyzer and Search Query:

You can use the custom analyzer created earlier in the search query:

```json
GET /my_index/_search
{
  "query": {
    "match": {
      "description": {
        "query": "Quick Fox",
        "analyzer": "my_analyzer"
      }
    }
  }
}
```

In this example:
- We specify the custom analyzer "my_analyzer" to analyze the search query, allowing it to match synonyms like "fast" for "quick."


---

### Built in analyzers

#### Standard Analyzers

- Split texts at word boundaries and removes punctuation
- - Done by the standard tokenizer
- Lowercases letters with lowercase token filter
- Contains the stop token filter (disable by default)


#### Simple Analyzers

- Similar to standard analyzers
- - Split into tokens when encountering anything else than letters
- Lowercase letters with the lowercase tokenizer
- - Unusual and a performance hack

#### White space analyzers

- Splits text into tokens whenever it encounters whitespace
- Does not lowercase letters

#### Keyword analyzers

- No-op analyzers that leaves the input text intact
- - It simply outputs it as a single token
- Used for keyword fields by default
- - Used for exact matching

#### Pattern analyzers

- Uses a regular expression to split text into tokens
- - It should match whatever should split the text into tokens
- - The regular expression is defined by the pattern parameter
- - The default pattern is \W+
- - - This means that the text is split whenever it encounters a non-word character
- - - This is similar to the simple analyzer

- This analyzer is very flexible
- Lowercase letters by default



### Creating a Custom Analyzers

```bash
PUT /analyzer_test
{
  "settings": {
    "analysis": {
      "analyzer": {
        "my_custom_analyzer": {
            "type": "custom",
            "char_filter": ["html_strip"],
            "tokenizer": "standard",
            "filter": ["lowercase", "my_synonym_filter", "stop", "lowercase", "asciifolding"]
        }
      }
    }
  }
}
```


```bash
POST /_analyze
{
  "analyzer": "standard",
  "text": "I&am;m in a <em>good</em> mood"
}
```


```bash
POST /_analyze
{
  "char_filter": ["html_strip"],
  "text": "I&am;m in a <em>good</em> mood"
}
```


#### Using Custom Analyzer

```bash
POST /analyzer_test/_analyze
{
  "analyzer": "my_custom_analyzer",
  "text": "I&am;m in a <em>good</em> mood"
}
```


#### Creating a Custom Analyzer for danish language stop words

```bash
PUT /analyzer_test
{
  "settings": {
    "analysis": {
      "filter": {
        "danish_stop": {
            "type": "stop",
            "stopwords": "_danish_"
          },
        }
      }
      "analyzer": {
        "my_custom_analyzer": {
            "type": "custom",
            "char_filter": ["html_strip"],
            "tokenizer": "standard",
            "filter": [
              "danish_stop", 
              "lowercase", 
              "my_synonym_filter", 
              "stop", 
              "lowercase", 
              "asciifolding"
            ]
        }
      }
    }
  }
}
```


### Updating Analyzers

#### Creating analyzer_test index

```bash
PUT /analyzer_test
{
  "settings": {
    "analysis": {
      "analyzer": {
        "my_custom_analyzer": {
          "type": "custom",
          "char_filter": ["html_strip"],
          "tokenizer": "standard",
          "filter": ["lowercase", "my_synonym_filter", "stop", "lowercase", "asciifolding"]
        }
      }
    }
  }
}
```

Ex:

```bash
PUT /analyzer_test/_mapping
{
  "properties": {
    "description": {
      "type": "text",
      "analyzer": "my_custom_analyzer"
    }
  }
}
```

```bash

POST /analyzer_test/_doc
{
  "description": "Is that Peter's book?"
}
```

```bash
GET /analyzer_test/_search
{
  "query": {
    "match": {
      "description": {
        "query": "that",
        "analyzer": "keyword" //This will override the default analyzer
      }
    }
  }
}
```

```bash
POST /analyzer_test/_close
```

```bash
PUT /analyzer_test/_settings
{
  "analysis": {
    "analyzer": {
      "my_custom_analyzer": {
        "type": "custom",
        "char_filter": ["html_strip"],
        "tokenizer": "standard",
        "filter": ["lowercase", "my_synonym_filter", "stop", "lowercase", "asciifolding"]
      }
    }
  }
}

```

```bash
POST /analyzer_test/_open
```

```bash
GET /analyzer_test/_settings
```

```bash
```

```bash
POST /analyzer_test/_analyze
{
  "analyzer": "my_custom_analyzer",
  "text": "I&am;m in a <em>good</em> mood"
}
```


#### Summary:

- Analyzers can be updated
- Pay attension to existing documents
- - They were analyzed with the old version of the analyzer
- - Reindex documents to avoid inconsistencies
- Try to get analyzers right from the start before indexing documents
- - Not always possible. in which case you know what to do

---

## Searching the data

### Introduction to Searching

- Searching is the process of retrieving documents from an index
- - It is done using queries
- - Queries are sent to the _search endpoint
- - The response contains the documents that match the query


### Query DSL

```bash
GET /products/_search
{
  "query": {
    "match_all": {}   // this query will match all documents in the index
  }
}
```

> Response

```json
{
  "took" : 3, // represents the time it took to execute the query
  "timed_out" : false,  // represents whether the query timed out
  "_shards" : { // represents the number of shards that were searched
    "total" : 1,  // represents the total number of shards that were searched
    "successful" : 1, // represents the number of shards that were successfully searched
    "skipped" : 0,  // represents the number of shards that were skipped
    "failed" : 0  // represents the number of shards that failed
  },
  "hits" : {  // represents the search results
    "total" : { // represents the total number of documents that match the query
      "value" : 1,  // represents the total number of documents that match the query
      "relation" : "eq" // represents the relation between the value and the total number of documents that match the query
    },
    "max_score" : 1.0,  // represents the maximum score of the documents that match the query
    "hits" : [  // represents the documents that match the query
      {
        "_index" : "products",  // represents the index of the document
        "_type" : "_doc", // represents the type of the document
        "_id" : "100",  // represents the ID of the document
        "_score" : 1.0, // represents the score of the document
        "_source" : { // represents the source of the document
          "name" : "Toaster", 
          "price" : 45,
          "in_stock" : 3
        }
      }
    ]
  }
}
```


### Term level queries

- One group of Elasticsearch queries is called term level queries
- Term level queries are used to search for exact values (filtering)
- - E.g. searching for documents where the price is 45 or finding products where brand name is "Sony"
- Term level queries are not analyzed
- - The search value is used exactly as is for inverted index lookups
- Can be used with data types such as keyword, numbers, dates, etc



> Example of term level queries

```bash
GET /products/_search
{
  "query": {
    "term": {
      "brand": "Sony"
    }
  }
}
```


### Searching for terms

```bash
GET /products/_search
{
  "query": {
    "term": {
      "tag.keyword": "vegetable"
    }
  }
}
```

> In the above query, documents will be matched if the tag.keyword field contains the exact term "vegetable".


#### Booleans

```bash
GET /products/_search
{
  "query": {
    "term": {
      "is_active": true
    }
  }
}
```


#### Numbers

```bash
GET /products/_search
{
  "query": {
    "term": {
      "price": 45
    }
  }
}
```

#### Dates

```bash
GET /products/_search
{
  "query": {
    "term": {
      "created_at": "2023-01-01"
    }
  }
}
```


#### Timestamp

```bash
GET /products/_search
{
  "query": {
    "term": {
      "created_at": "2023-01-01T12:34:56"
    }
  }
}
```

#### Shorthand Syntax

```bash
GET /products/_search
{
  "query": {
    "term": {
      "tags.keyword": "Vegetable"
    }
  }
}
```

#### Explicit Syntax

```bash
GET /products/_search
{
  "query": {
    "term": {
      "tags.keyword": {
        "value": "Vegetable"
      }
    }
  }
}

```

#### Term level query search with case insensitivity

```bash
GET /products/_search
{
  "query": {
    "term": {
      "tags.keyword": {
        "value": "vegetable",
        "case_insensitive": true
      }
    }
  }
}
```

#### Term query for multiple values

```bash
GET /products/_search
{
  "query": {
    "terms": {
      "tags.keyword": ["vegetable", "fruit"]
    }
  }
}
```

> In the above query, a document will be matched if the tags.keyword field contains either "vegetable" or "fruit".


> Summary:
- Used too query several different data types
- - Keyword, numbers, dates, etc
- Case Sensitive by default
- - A case_insensitive parameter was added in v7.1.0
- Use the term query to search for multiple terms



### Retreiving documents by IDs

```bash
GET /products/_search
{
  "query": {
    "ids": {
      "values": ["100", "101", "102"]
    }
  }
}
```


### Range Searches

- Range queries are used to search for a range of values
- - E.g. searching for products where the price is between 20 and 50
- Range queries can be used with data types such as numbers, dates, etc
- - They can also be used with text fields, but the results might not be as expected

#### Querying numeric ranges
  
```bash
GET /products/_search
{
  "query": {
    "range": {
      "price": {
        "gte": 20,
        "lte": 50
      }
    }
  }
}
```

SQL equivalent

```sql
SELECT * FROM products WHERE price >= 20 AND price <= 50
```


#### Different Parameters

- gte: Greater than or equal to
- gt: Greater than
- lte: Less than or equal to
- lt: Less than
- - The parameters can be used in combination
- - - E.g. gte and lte, gt and lt, etc


#### Querying dates


- Dates without time

```bash
GET /products/_search
{
  "query": {
    "range": {
      "created_at": {
        "gte": "2023-01-01",
        "lte": "2023-01-31"
      }
    }
  }
}
```

- Dates with time

```bash
GET /products/_search
{
  "query": {
    "range": {
      "created_at": {
        "gte": "2023-01-01T12:34:56",
        "lte": "2023-01-31T12:34:56"
      }
    }
  }
}
```

#### Specifying a date format

```bash
GET /products/_search
{
  "query": {
    "range": {
      "created_at": {
        "gte": "2023-01-01",
        "lte": "2023-01-31",
        "format": "yyyy-MM-dd"
      }
    }
  }
}
```

- Default date format
  - yyyy-MM-dd'T'HH:mm:ss.SSSZ | yyyy-MM-dd HH:mm:ss.SSS | YYYY/MM/dd | epoch_millis
  - - This is the default date format used by Elasticsearch
  - - It is used when the format parameter is not specified


#### Specifying a UTC offset

```bash
GET /products/_search
{
  "query": {
    "range": {
      "created_at": {
        "gte": "2023-01-01",
        "lte": "2023-01-31",
        "format": "yyyy-MM-dd",
        "time_zone": "+01:00"
      }
    }
  }
}
```

- In above query, we specify the time_zone parameter to "+01:00" to specify the UTC offset. 
- This is useful when the date is stored in UTC and you want to search for documents based on a specific time zone.
- Elastic search will compare the date with the UTC offset specified in the time_zone parameter.


#### Summary
- Range queries are used to search for a range of values
- - E.g. searching for products where the price is between 20 and 50
- Range queries can be used with data types such as numbers, dates, etc
Specify one or more of the gt, gte, lt, and lte parameters
- Dates are automatically handled for the date fields
- - You can specify the date format and the UTC offset
- - Custom formats can be used


### Prefixes, Wildcards and Regular expressions

- Term level queries are used to search for exact values
- - Query non-analyzed values with queries that are not analyzed
- There are a few exceptions
- - Query by prefix, wildcard, and regular expression
- - Remember to still query keyword fields with keyword queries

#### Prefix queries

```bash
GET /products/_search
{
  "query": {
    "prefix": {
      "name.keyword": {
        "value": "Toast"
      }
    }
  }
}
```

- It will match documents where the name.keyword field starts with "Toast"
- - E.g. "Toaster", "Toasting Machine", etc


#### Wildcard queries

- Wildcard queries are used to search for a pattern in a field 
- - They can be used to search for a pattern in text fields


**Patterns and Terms**

- The wildcard query supports two special characters: * and ?
- - The * character matches zero or more characters
- - The ? character matches exactly one character
- - E.g. "Toa*" will match "Toaster", "Toasting Machine", etc
- - E.g. "Toa?er" will match "Toaster", "Toaster", etc


```bash
GET /products/_search
{
  "query": {
    "wildcard": {
      "name.keyword": {
        "value": "Toa*"
      }
    }
  }
}
```

- It will match documents where the name.keyword field contains the pattern "Toa*"
- - E.g. "Toaster", "Toasting Machine", etc

```bash
GET /products/_search
{
  "query": {
    "wildcard": {
      "name.keyword": {
        "value": "Past?"
      }
    }
  }
}
```

- It will match documents where the name.keyword field contains the pattern "Past?" 
- - E.g. "Pasta", "Paste", etc

> Note: Avoid placing the wildcard character at the beginning of a query. It will slow down the query significantly and causes performance issues.


### Regular expression queries

- Regular expression queries are used to search for a pattern in a field
- The regex query matches terms that match a regular expression
- Regular expressions are used for matching strings
- Allows more complex queries than the wildcard query

- - They can be used to search for a pattern in text fields
- - They are more powerful than prefix and wildcard queries
- - They are also slower and can cause performance issues


#### Regular expression examples

* Patterns
  - The regex query supports regular expressions
  - Bee(t|r)+
  - - This pattern will match "beet", "beer", "beetroot

```bash
GET /products/_search
{
  "query": {
    "regexp": {
      "name.keyword": {
        "value": "Bee(t|r)+"
      }
    }
  }
}
```

* Patterns II
  - Bee[a-zA-Z]
  - - This pattern will match "beet", "beer", "beetroot

```bash
GET /products/_search
{
  "query": {
    "regexp": {
      "name.keyword": {
        "value": "Bee[a-zA-Z]"
      }
    }
  }
}
```

#### Engine comparisons

Other engines       Apache Lucene
- ^Beer             Beer.*
- Beer$             .*Beer
- Bee[a-zA-Z]+$     Bee[a-zA-Z]+.*

> Note: All the queries are case sensitive by default. You can use the case_insensitive parameter to make the queries case insensitive.


### Querying by field existance

* How empty values are indexed
- NULL -  N/A
- [] -  N/A
- "" -  ""


#### Reasons for no indexed value
- Empty value provided (NULL or [])
- - The value null_value parameter is an exception for NULL values
- No value was provided for the field
- The index mapping parameter is set to false for the field
- The values length is greater than the ignore_above parameter
- Malformed value with the ignore_malformed mapping parameter is set to true


#### Inverting the query

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "must_not": {
        "exists": {
          "field": "tags.keyword"
        }
      }
    }
  }
}
```

**SQL equivalent**

```sql
SELECT * FROM products WHERE tags IS NULL
```

> The above query will match documents where values of the tags.keyword field does not exist in the index documents.


#### Summary
- The exists query matches fields that have an indexed value
- Field values are only indexed if they are considered non-empty
- - NULL or [] are not indexed and are empty values
- The exists query can be inverted by using the bool query's must_not occurance



### Intro to Full Text Queries

- Term level queries are used for exact matching on structured data
- Full term queries are used for searching on unstructured text data
- - E.g. Website content, news articles, emails, chats, transcripts, etc
- - Often used for long texts
- Full text queries are analyzed


#### Query

```
GET /products/_search
{
  "query": {
    "match": {
      "body": "SHARDING"
    }
  }
}
```

> SHARDING -> Analyzer -> sharding

**Inverted index**

Term -> Document #1
- sharding -> 1
- shard -> 1
- distributed -> 1
- system -> 1


#### Full text queries vs term level queries
- Full text queries are used for searching on unstructured text data
- - E.g. Website content, news articles, emails, chats, transcripts, etc

- Term level queries are used for exact matching on structured data
- - E.g. Searching for products where the price is 45 or finding products where brand name is "Sony"

- The main difference is full text queries are analyzed and term level queries are not and are therefore used for exact matching

- Don't use full text queries on keyword fields
- - That compares analyzed value with non-analyzed value


#### Summary
- Full text queries are used for searching on unstructured text data
- Use full text queries to search unstuctured text data
- - E.g. Website content, news articles, emails, chats, transcripts, etc
- Full text queries are not used for exact matching
- - They match values that include a term, often being one of many
- Full text queries are analyzed in the same way as the fields that are queried


### Intro to match query

- The match query is the most commonly used full text query
- Matches documents that contains one or more of the specified terms
- The search term is analyzed and the result is looked up in the field's inverted index


> Sample search query

```bash
GET /products/_search
{
  "query": {
    "match": {
      "name": "PASTA CHICKEN" //searches in inverted index with values "pasta" OR "chicken"
    }
  }
}
```

> The above query will match documents where the name field contains the terms "pasta" or "chicken".



```bash
GET /products/_search
{
  "query": {
    "match": {
      "name": {
        "query": "PASTA CHICKEN", //searches in inverted index with values "pasta" AND "chicken",
        "operator": "AND"
      }
    }
  }
}
```

> The above query will match documents where the name field contains the terms "pasta" and "chicken".


#### Summary
- The match query is the fundamental query in elasticsearch
- Used for most full text searches
- Powerful and flexible when using advanced parameters
- Supports most data types
- - Text, keyword, numbers, dates, etc
- - Recommendation: Use term level queries if you know the input value
- If the analyzer outputs multiple terms, at least one must match by default
- - This can be changed by setting the operator parameter to "AND"
  


### Intro to Relevant Scoring

- The match query returns documents in order of relevance
- - The relevance score is calculated for each document
- - The score is based on how well the document matches the query

- With full text search, we don't just care about if the term matches. We also care about how well it matches

For Ex:

> Query

```bash
GET /products/_search
{
  "query": {
    "match": {
      "name": "PASTA CHICKEN"
    }
  }
}
```

### Matching documents

```json
{
  "name": "Pasta Penna",
  "_score": 3.2876821
}

{
  "name": "Chicken Pasta",
  "_score": 4.2876821
}

{
  "name": "Pasta with Chicken",
  "_score": 2.2876821
}

{
  "name": "Chicken",
  "_score": 1.2876821
}
```

> Query Results (Sorted by _score)

```json
{
  "name": "Chicken Pasta",
  "_score": 4.2876821
}

{
  "name": "Pasta with Chicken",
  "_score": 4.0876821
}

{
  "name": "Pasta Penna",
  "_score": 3.2876821
}

{
  "name": "Chicken",
  "_score": 1.2876821
}
```


#### Summary
- Query results are sorted by relevance score (_score metadata field)
- - A floating point number of how well the document matches the query
- Documents matching term level queries are generally scored 1.0
- - Either a document matches or it doesn't
- Full text queries are not for exact matching
- - How well a document matches is now a factor


### Searching multiple fields

- The match query can be used to search multiple fields


```bash
GET /products/_search
{
  "query": {
    "multi_match": {
      "query": "PASTA CHICKEN",
      "fields": ["name", "description"]
    }
  }
}
```

```bash
GET /products/_search
{
  "query": {
    "multi_match": {
      "query": "PASTA CHICKEN",
      "fields": ["name", "description"],
      "type": "cross_fields"
    }
  }
}
```

```bash
GET /products_new/_search
{
  "query": {
    "match_all": {}
  }
}
```

```bash
GET /products_new/_search
{
  "query": {
    "multi_match": {
      "query": "kitchen",
      "fields": ["name", "tags"]
    }
  }
}
```


Response:


```json
{
  "took" : 6,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 6,
      "relation" : "eq"
    },
    "max_score" : 1.1921031,
    "hits" : [
      {
        "_index" : "products_new",
        "_type" : "_doc",
        "_id" : "upcJuI0BZW6NGeIagL6j",
        "_score" : 1.1921031,
        "_source" : {
          "name" : "Kitchen Blender",
          "price" : 1510,
          "in_stock" : 51,
          "tags" : [
            "appliances"
          ]
        }
      },
      {
        "_index" : "products_new",
        "_type" : "_doc",
        "_id" : "-erslo0Bh1-Bhwq-ibeF",
        "_score" : 0.29624987,
        "_source" : {
          "name" : "Toaster",
          "price" : 45,
          "in_stock" : 3,
          "tags" : [
            "kitchen",
            "appliances"
          ]
        }
      }
    ]
  }
}
```


> Note: A very useful feature of multi search is adjusting the relevant score of the fields. For example, you can give more weight to the name field than the description field.

Example:

```bash
GET /products_new/_search
{
  "query": {
    "multi_match": {
      "query": "kitchen",
      "fields": ["name^3", "tags"] // this means that the name field is 3 times more important than the description field
    }
  }
}
```

#### How the multi match query works

- The elastic search internally creates a query for each field
- - It then combines the results of the queries

For ex:

```bash
GET /products_new/_search
{
  "query": {
    "multi_match": {
      "query": "kitchen",
      "fields": ["name", "tags"]
    }
  }
}
```

- The above query will create a query for the name field and a query for the tags field
- The results of the queries are then combined and the documents are sorted by relevance score

The internally converted query:

```bash
GET /products_new/_search
{
  "query": {
    "match": {
      "name": "kitchen"
    }
  }
}
```

```bash
GET /products_new/_search
{
  "query": {
    "match": {
      "tags": "kitchen"
    }
  }
}
```


#### Specifying the tie breaker

- By default, the multi match query uses the best matching field(one field) to calculate the relevance score
- We can "reward" documents where multiple fields match the   tie_breaker parameter
- - Each field's score is multiplied by the tie_breaker parameter. The default value is 0.3. The result is then added to the final score
- - The tie_breaker parameter is a floating point number between 0 and 1
- - A value of 0 means that the best matching field is used
- - A value of 1 means that all matching fields are used equally

> Example:

```bash
GET /products_new/_search
{
  "query": {
    "multi_match": {
      "query": "kitchen",
      "fields": ["name", "tags"],
      "tie_breaker": 0.3
    }
  }
}
```

#### Summary
- The multi match query performs full text search on multiple fields
- - A document matches if at least one field matches
- The individual fields can be relevance boosted by modifying the field name (e.g. name^3)
- - It creates a query for each field and combines the results
- By default, the best matching field is used to calculate the relevance score
- - Can be configured with the type parameter
- The tie_breaker parameter is used to reward documents where multiple fields match
- - The default value is 0.3
- - A value of 0 means that the best matching field is used
- - A value of 1 means that all matching fields are used equally


### Phrase Searches

- The match query is used to search for documents that contain one or more of the specified terms


Ex:

* Query #1

```bash
GET /products/_search
{
  "query": {
    "match": {
      "name": "Fanta Zero"
    }
  }
}
```

* Query #2

```bash
GET /products/_search
{
  "query": {
    "match": {
      "name": "Zero Fanta"
    }
  }
}
```

* Query #3

```bash
GET /products/_search
{
  "query": {
    "match": {
      "description": "Fanta Zero"
    }
  }
}
```

> Output JSON

```json
{
  "name": "Fanta Zero",
  "description": "Like the regular Fanta, but with zero sugar"
}
```


* Phrase searches has many similarities with the match query. 
* A Phrase is a sequence of one or more words. Such as "Browse the web" or "Search for a product".
* In elastic search, we use match_phrase query to search for phrases. When doing so, the order of the words in the phrase matters which differs from how the match query works.


#### Examples to illustrate the difference between match and match_phrase queries

* Query #1

```bash
GET /products/_search
{
  "query": {
    "match": {
      "name": "Fanta Zero"
    }
  }
}
```

* Query #2

```bash
GET /products/_search
{
  "query": {
    "match_phrase": {
      "name": "Fanta Zero"
    }
  }
}
```

- The match_phrase query is analyzed same as the match query usually with the standard analyzer
- - The match_phrase query is used to search for a sequence of words in a field. The order of the words in the phrase matters and the phrase must match exactly with the field value in the inverted index.


#### How match_phrase query works

- The match_phrase query is used to search for a sequence of words in a field
- The elasticsearch keeps track of the position of each term in the field value in the inverted index. This allows the match_phrase query to search for phrases in the field values.
- This information is recorded during the analysis process by default
- When a string is indexed into a text field, the analyzer will record the position of each term in the field value
- Specifically this task is taken care by analyzer and tokenizer
- These positions are then stored within the inverted index fields positions

Ex: 

```bash

GET /products/_search
{
  "query": {
    "match_phrase": {
      "description": "Elasticsearch guide"
    }
  }
}
```

["elasticsearch", "guide"] -> [1, 2]

- The above query will match documents where the description field contains the phrase "Elasticsearch guide".


#### Summary
- The match_phrase query is used to search for a sequence of words in a field
- The order of the words in the phrase matters
- Terms must appear in the field in the same order as the phrase
- The standard token analyzer's tokenizer records the position of each term in the field value
- - These positions are then stored within the inverted index fields positions 
- - This allows the match_phrase query to search for phrases in the field values


### Leaf vs Compund Queries

- Leaf queries searches for values and are independent queries
- - E.g `term` and `match` queries
- Compund queries wrap other queries to produce a result
- - A compound query can be nested inside another compound query


## Querying with boolean logic

> Example 1

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "name": "Fanta Zero"
          }
        },
        {
          "match": {
            "description": "sugar"
          }
        }
      ]
    }
  }
}
```

> Example 2

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "name": "Fanta Zero"
          }
        },
        {
          "match": {
            "description": "sugar"
          }
        }
      ],
      "should": [
        {
          "match": {
            "tags": "sugar"
          }
        }
      ],
      "must_not": [
        {
          "match": {
            "tags": "diet"
          }
        }
      ]
    }
  }
}
```

> Example 3

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "name": "Fanta Zero"
          }
        },
        {
          "match": {
            "description": "sugar"
          }
        }
      ],
      "should": [
        {
          "term": {
            "tags.keyword": "sugar"
          }
        },
        {
          "match": {
            "tags": "sugar"
          }
        },
        {
          "match": {
            "name": "sweet"
          }
        },
        {
          "match": {
            "description": "sweet"
          }
        }
      ],
      "minimum_should_match": 1
    }
  }
}
```


> Sample Queries

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tags.keyword": "Alcohol"
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "tags.keyword": "Wine"
          }
        }
      ],
      "should": [
        {
          "term": {
            "tags.keyword": "Beer"
          }
        },
        {
          "match": {
            "name": "Beer"
          }
        },
        {
          "match": {
            "description": "Beer"
          }
        }
      ]
    }
  }
}
```

> Return Documents:

```json
{
  "name": "Beer",
  "description": "A cold beer is the best thing on a hot day",
  "tags": ["Alcohol", "Beer"]
}

{
  "name": "Beer",
  "description": "cold beer can be refreshing",
  "tags": ["Alcohol", "Beer"]
}

{
  "name": "Beer",
  "description": "its beer time",
  "tags": ["Alcohol", "Beer"]
}
```

**Important thing about should clause**
- If a bool query only contains should clauses, at least one must match
- Useful if we want something to match and reward matching documents
- - If nothing were required to match, we would get irrelevant results
- If a query exists for must, must_not, or filter, no should clause is required to match
- - Any should clauses are only used to boost relevance scores
- should clauses are optional
- "minimum_should_match": 1 can be used to require at least one should clause to match
- "percentage" can be used to require a percentage of should clauses to match
- - E.g. "minimum_should_match": 75%

> Example:

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "tags.keyword": "Alcohol"
          }
        },
        {
          "match": {
            "name": "Wine"
          }
        }
      ]
    }
  }
}
```

### The filter occurrence type
- A filter clause is used to filter documents and does not affect the relevance score
- A Query clause must match and affects the relevance score
- Similar to the must occurence type
- Ignores relevance score
- - This improves the performance of the query
- Query results can be cached and reused


Occurrence                         Description

must                    -          Query clauses are required to match and will contribute to the relevance score

filter                  -          Query clauses are required to match but will not contribute to the relevance score

must_not                -          Query clauses are required not to match and will not contribute to the relevance score. Query clauses may therefore be cached and improve performance

should                  -          Query clauses are not required to match but will contribute to the relevance score. Behaviour can be controlled with the minimum_should_match parameter





- Required ot match? 
* must - yes
* filter - yes
* must_not - no
* should - conditional

- Affects relevance score?
* must - yes
* filter - no
* must_not - no
* should - yes

- Can be cached?
* must - no
* filter - yes
* must_not - yes
* should - no



### SQL Query
wher (tags IN ("Beer") or names LIKE %Beer% AND in_stock <= 100)

### Corresponding Elastic Search Query using `filter`

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "tags.keyword": "Beer"
          }
        },
        {
          "match": {
            "name": "Beer"
          }
        }
      ],
      "filter": {
        "range": {
          "in_stock": {
            "lte": 100
          }
        }
      }
    }
  }
}
```

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "tags.keyword": "Beer"
          }
        },
        {
          "match": {
            "name": "Beer"
          }
        }
      ],
      "filter": {
        "range": {
          "in_stock": {
            "lte": 100
          }
        }
      }
    }
  }
}
```


## Query Execution Context

* Answer two questions
- - Does this document match? (yes/no)
- - How well does this document match (`_score` metadata field)

* Query results are sorted by `_score` descendingly
- - The most relevant document appears at the top

### Identifying the query context

```bash
GET /products/_search
{
  "query": {    //it indicates that the query clauses nested in this key are executed in a query context meaning documents are rated based on relevance
    "match": {
      "name": "Fanta Zero"
    }
  }
}
```

### Filter query context
* Only answers the question "Does this document match? (yes/no)"
- - No relevance scores are calculated

* Used to filter data, typically on structured data (dates, numbers, keywords)
- - Relevance scoring is irrelevant if we want to filter out documents

* Improves performance
- - No resources are spent calculating relevance scores
- - Query results can be cached

### Changing the execution context

```bash
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "name": "Fanta Zero"
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "tags.keyword": "Diet"
          }
        }
      ],
      "filter": [
        {
          "range": {
            "price": {
              "lte": 100
            }
          }
        }
      ],
      "should": [
        {
          "match": {
            "description": "sugar"
          }
        }
      ]
      ]
    }
  }
}
```


* In situations where we don't need relevance scoring, its a good optimization to move query clauses from "must" to "filter" or "must_not" to "filter"
* Its sometimes possible to change the execution context
- - Only a few query support it

* Typically done with the `bool` query and `filter` aggregation
* Queries that support this generally have a filter parameter


Summary:
* The query execution context calculates relevance scores
* The filter execution context does not calculate relevance scores
- - Used for filtering data, typically with structured data (e.g by date)
* The filter execution context improves performance
- - No resources spent calculating relevance scores
- - Queries can be cached
* Only a few queries support changing the execution context
- - Look for a `filter` parameter


## Boosting query
- The bool query enables us to increase relevance scores with should

* What if we want to decrease relevance scores for some documents?
- - This can be done with the `boosting` query

```bash
GET /products/_search
{
  "size": 20,
  "query": {
    "match": {
      "name": "juice"
    }
  }
}
```

> The above query will match documents where the name field contains the term "juice" and the results will be sorted by relevance score.

### Boosting query example

```bash
GET /product/_search
{
  "size": 20,
  "query": {
    "boosting": {
      "positive": {
        "match": {
          "name": "juice"
        }
      },
      "negative": {
        "term": {
          "tags.keyword": "diet"
        }
      },
      "negative_boost": 0.2 // this means that the negative query will have 20% less relevance score than the positive query
    }
  }
}
```


### Example 2

```bash
GET /products/_search
{
  "size": 20,
  "query": {
    "boosting": {
      "positive": {
        "match_all": {}
      },
      "negative": {
        "term": {
          "tags.keyword": "diet"
        }
      },
      "negative_boost": 0.2
    }
  }
}
```


### Example 3 - Increase relevance scoring of recipe containing pasta

```bash
GET /products/_search
{
  "size": 20,
  "query": {
    "bool" : {
      "must": [
        {"match_all": {}}
      ]
    },
    "should": [
      {
        "term": {
          "ingredients.name.keyword": "Pasta"
        }
      }
    ]
  }
}
```

### Example 4 - Reduce the relevance score of recipes containing bacon


```bash
GET /recipes/_search
{
  "query": {
    "boosting": {
      "positive": {
        "match_all": {}
      },
      "negative": {
        "term": {
          "ingredients.name.keyword": "Bacon"
        }
      },
      "negative_boost": 0.5
    }
  }
}
```


### Summary

- The bool query can increase the relevance score with should
- The boosting query can decrease relevance scores with negative
- - Document must match the positive query clause
- - Document that match the negative query clause will have a lower relevance score
- - Use `match_all` query for positive if you don't want to filter documents
- - Can be used with any query (including compound queries, such as bool)


## Disjunction Max (dis_max)

* dis_max query is used to search for documents that contain one or more of the specified terms

```bash
GET /products/_search
{
  "query": {
    "dis_max": {
      "queries": [
        {
          "match": {
            "name": "Fanta Zero"
          }
        },
        {
          "match": {
            "description": "sugar"
          }
        }
      ],
      "tie_breaker": 0.3
    }
  }
}
```

> Score calculation using tie breaker

* Documents:

{
  "name": "Fanta Zero",
  "description": "Like the regular Fanta, but with zero sugar"
}

* Score Calculation

- name: 2.46
- description: 5.653

- 2.46 + 5.653 * 0.3 = 4.0876821 // this is the final score of the document

> This query will match documents where the name field contains the term "Fanta Zero" or the description field contains the term "sugar". The tie_breaker parameter is used to reward documents where multiple fields match. The value lies between 0 and 1. A value of 0 means that the best matching field is used and a value of 1 means that all matching fields are used equally.

* Documents:

{
  "name": "Fanta Zero", (2.46)
  "description": "Like the regular Fanta, but with zero sugar" (5.653)
}


### Summary
- The `dis_max` query is a compound query
- - A document matches if at least one leaf query matches
- The best matching matching query clause's relevance score is used for a document's _score
- tie_breaker can be used to "reward" documents that match multiple queries
- `multi_match` queries are often translated into dis_max queries internally
