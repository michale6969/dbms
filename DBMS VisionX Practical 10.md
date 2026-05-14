# Assignment No. - 10

## Title

Aggregation and Indexing in MongoDB.

## Problem Statement

Design and execute MongoDB queries using aggregation and indexing techniques with suitable examples.

## Objective

- To learn concept of aggregation and indexing.
- To implement aggregation and indexing techniques in MongoDB.

## Theory

MongoDB is an open-source document database and leading NoSQL database. MongoDB is written in C++. This tutorial will give you great understanding on MongoDB concepts needed to create and deploy a highly scalable and performance-oriented database.

Aggregation operations process data records and return computed results. Aggregation operations group values from multiple documents together, and can perform a variety of operations on the grouped data to return a single result. In SQL, `count(*)` with `group by` is an equivalent of MongoDB aggregation.

### The aggregate() Method

For the aggregation in MongoDB, you should use `aggregate()` method.

#### Syntax

```javascript
db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
```

#### Example

In the collection, you can keep VisionX session analytics data like this:

```javascript
db.visionx_sessions.insertMany([
  {
    session_id: 501,
    device_code: "VX-ESP-01",
    operator: "pratik",
    session_state: "COMPLETE",
    frame_count: 3840,
    likes: 12
  },
  {
    session_id: 502,
    device_code: "VX-ESP-01",
    operator: "pratik",
    session_state: "ERROR",
    frame_count: 920,
    likes: 4
  },
  {
    session_id: 503,
    device_code: "VX-ESP-02",
    operator: "assistant",
    session_state: "COMPLETE",
    frame_count: 4100,
    likes: 8
  }
])
```

If you want to display how many VisionX sessions are handled by each operator:

```javascript
db.visionx_sessions.aggregate([
  {
    $group: {
      _id: "$operator",
      num_sessions: { $sum: 1 }
    }
  }
])
```

```text
[
  { _id: "pratik", num_sessions: 2 },
  { _id: "assistant", num_sessions: 1 }
]
```

SQL equivalent query for this use case:

```sql
SELECT operator, COUNT(*)
FROM visionx_sessions
GROUP BY operator;
```

### Pipeline Concept

In UNIX command, shell pipeline means the possibility to execute an operation on some input and use the output as the input for the next command and so on.

MongoDB also supports same concept in aggregation framework. There is a set of possible stages and each of those is taken as a set of documents as an input and produces a resulting set of documents (or the final resulting JSON document at the end of the pipeline). This can then in turn be used for the next stage and so on.

Following are the possible stages in aggregation framework:

- `$project`: Used to select some specific fields from a collection.
- `$match`: This is a filtering operation and thus this can reduce the amount of documents that are given as input to the next stage.
- `$group`: This does the actual aggregation as discussed above.
- `$sort`: Sorts the documents.
- `$skip`: With this, it is possible to skip forward in the list of documents for a given amount of documents.
- `$limit`: This limits the amount of documents to look at, by the given number starting from the current positions.
- `$unwind`: This is used to unwind document that are using arrays.

When using an array, the data is kind of pre-joined and this operation will be undone with this to have individual documents again. Thus with this stage we will increase the amount of documents for the next stage.

### Indexes

Indexes support the efficient resolution of queries. Without indexes, MongoDB must scan every document of a collection to select those documents that match the query statement. This scan is highly inefficient and requires MongoDB to process a large volume of data.

Indexes are special data structures that store a small portion of the data set in an easy-to-traverse form. The index stores the value of a specific field or set of fields, ordered by the value of the field as specified in the index.

### THE ensureIndex() METHOD

To create an index you need to use `ensureIndex()` method of MongoDB.

#### Syntax

```javascript
db.COLLECTION_NAME.ensureIndex({ KEY: 1 })
```

Here `KEY` is the name of the field on which you want to create index and `1` is for ascending order. To create index in descending order you need to use `-1`.

#### Example

```javascript
db.visionx_sessions.ensureIndex({ "device_code": 1 })
```

In `ensureIndex()` method you can pass multiple fields, to create index on multiple fields:

```javascript
db.visionx_sessions.ensureIndex({ "device_code": 1, "session_state": -1 })
```

Aggregation examples for MIN, PUSH, SUM, and AVG:

```javascript
db.visionx_sessions.aggregate([
  {
    $group: {
      _id: "$device_code",
      min_frames: { $min: "$frame_count" },
      total_frames: { $sum: "$frame_count" },
      avg_frames: { $avg: "$frame_count" },
      session_ids: { $push: "$session_id" }
    }
  }
])
```

## Conclusion

Thus we have studied and implemented aggregation function and indexing function.

## FAQ

1. Enlist various aggregation operations.
2. Explain MIN function with example.
3. Explain PUSH function with example.
4. Explain SUM and AVG function with example.
