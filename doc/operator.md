MongoDB offers a wide range of operators for querying and manipulating documents in a collection. These operators allow you to filter, sort, project, update, and perform various other actions on your data. Below is an overview of the key operators in MongoDB, divided into categories based on their usage.

### 1. **Comparison Operators**

These operators are used to compare values in queries.

- **`$eq`**: Matches values that are equal to the specified value.
  ```javascript
  db.collection.find({ age: { $eq: 25 } });
  ```

- **`$ne`**: Matches values that are **not** equal to the specified value.
  ```javascript
  db.collection.find({ age: { $ne: 25 } });
  ```

- **`$gt`**: Matches values that are greater than the specified value.
  ```javascript
  db.collection.find({ age: { $gt: 25 } });
  ```

- **`$gte`**: Matches values that are greater than or equal to the specified value.
  ```javascript
  db.collection.find({ age: { $gte: 25 } });
  ```

- **`$lt`**: Matches values that are less than the specified value.
  ```javascript
  db.collection.find({ age: { $lt: 25 } });
  ```

- **`$lte`**: Matches values that are less than or equal to the specified value.
  ```javascript
  db.collection.find({ age: { $lte: 25 } });
  ```

- **`$in`**: Matches values that are within the specified array.
  ```javascript
  db.collection.find({ age: { $in: [20, 25, 30] } });
  ```

- **`$nin`**: Matches values that are **not** within the specified array.
  ```javascript
  db.collection.find({ age: { $nin: [20, 25, 30] } });
  ```

### 2. **Logical Operators**

Logical operators are used to combine multiple query conditions.

- **`$and`**: Matches documents that satisfy all conditions.
  ```javascript
  db.collection.find({ $and: [{ age: { $gte: 25 } }, { city: "New York" }] });
  ```

- **`$or`**: Matches documents that satisfy at least one of the conditions.
  ```javascript
  db.collection.find({ $or: [{ age: { $gte: 25 } }, { city: "New York" }] });
  ```

- **`$nor`**: Matches documents that do not satisfy any of the conditions.
  ```javascript
  db.collection.find({ $nor: [{ age: { $lt: 25 } }, { city: "New York" }] });
  ```

- **`$not`**: Inverts the effect of a query condition.
  ```javascript
  db.collection.find({ age: { $not: { $lt: 25 } } });
  ```

### 3. **Element Operators**

These operators are used to query based on the type or existence of a field.

- **`$exists`**: Matches documents where a field exists or does not exist.
  ```javascript
  db.collection.find({ age: { $exists: true } });
  db.collection.find({ age: { $exists: false } });
  ```

- **`$type`**: Matches documents where the field is of a specified BSON type.
  ```javascript
  db.collection.find({ age: { $type: "int" } });
  ```

### 4. **Evaluation Operators**

These operators are used for evaluating expressions in queries.

- **`$regex`**: Performs regular expression matching.
  ```javascript
  db.collection.find({ name: { $regex: /^J/ } });  // Matches names starting with "J"
  ```

- **`$text`**: Performs a text search on a text-indexed field.
  ```javascript
  db.collection.find({ $text: { $search: "MongoDB" } });
  ```

- **`$where`**: Matches documents based on a JavaScript expression.
  ```javascript
  db.collection.find({ $where: "this.age > 25" });
  ```

### 5. **Array Operators**

These operators are used for querying array values.

- **`$all`**: Matches documents where the value of a field is an array that contains all the specified elements.
  ```javascript
  db.collection.find({ tags: { $all: ["mongodb", "database"] } });
  ```

- **`$elemMatch`**: Matches documents where at least one element in an array matches the specified query.
  ```javascript
  db.collection.find({ scores: { $elemMatch: { score: { $gt: 80 }, subject: "Math" } } });
  ```

- **`$size`**: Matches documents where the array field is of the specified size.
  ```javascript
  db.collection.find({ tags: { $size: 3 } });
  ```

### 6. **Update Operators**

These operators are used for updating documents.

- **`$set`**: Sets the value of a field.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $set: { age: 30 } });
  ```

- **`$unset`**: Removes a field from a document.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $unset: { age: "" } });
  ```

- **`$inc`**: Increments the value of a field by a specified amount.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $inc: { age: 1 } });
  ```

- **`$mul`**: Multiplies the value of a field by a specified amount.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $mul: { price: 1.1 } });
  ```

- **`$rename`**: Renames a field.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $rename: { oldFieldName: "newFieldName" } });
  ```

- **`$push`**: Adds an element to an array.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $push: { tags: "MongoDB" } });
  ```

- **`$pull`**: Removes an element from an array.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $pull: { tags: "MongoDB" } });
  ```

- **`$addToSet`**: Adds an element to an array only if it does not already exist.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $addToSet: { tags: "MongoDB" } });
  ```

- **`$pop`**: Removes the first or last element of an array.
  ```javascript
  db.collection.updateOne({ _id: 1 }, { $pop: { tags: 1 } });  // Removes the last element
  db.collection.updateOne({ _id: 1 }, { $pop: { tags: -1 } });  // Removes the first element
  ```

### 7. **Aggregation Operators**

These operators are used within the aggregation framework to process and transform data.

- **`$match`**: Filters documents based on specified criteria.
  ```javascript
  db.collection.aggregate([{ $match: { age: { $gte: 25 } } }]);
  ```

- **`$group`**: Groups documents by a specified identifier and applies aggregation operations like `$sum`, `$avg`, `$max`, `$min`, etc.
  ```javascript
  db.collection.aggregate([
    { $group: { _id: "$city", totalAge: { $sum: "$age" } } }
  ]);
  ```

- **`$sort`**: Sorts the documents in the pipeline by specified fields.
  ```javascript
  db.collection.aggregate([{ $sort: { age: -1 } }]);
  ```

- **`$project`**: Projects specific fields of a document to include or exclude them from the result.
  ```javascript
  db.collection.aggregate([{ $project: { name: 1, age: 1 } }]);
  ```

- **`$limit`**: Limits the number of documents passed to the next stage in the pipeline.
  ```javascript
  db.collection.aggregate([{ $limit: 5 }]);
  ```

- **`$skip`**: Skips the first N documents in the aggregation pipeline.
  ```javascript
  db.collection.aggregate([{ $skip: 10 }]);
  ```

### Conclusion

MongoDB provides a wide variety of operators for querying, updating, and manipulating documents. By leveraging these operators, you can build powerful queries and perform complex data transformations to meet your application's requirements. The most commonly used operators are comparison operators, logical operators, and update operators, but you can explore additional functionality with aggregation operators and more advanced features depending on your needs.