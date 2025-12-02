
#  **MongoDB — Complete Beginner **


# **1. What is MongoDB? **

MongoDB is a **NoSQL database** that stores data as **documents**, not tables like SQL.

A document = JSON-like object:

```json
{
  "name": "poovarasan",
  "age": 28,
  "city": "chennai"
}
```

### Why this format?

Because today’s applications store:

* User profiles
* Logs
* Clicks
* Sensor data
* Metadata

All in **flexible and dynamic** formats.

Tables (SQL) are rigid—documents (MongoDB) are free-form.

### MongoDB is:

* **Schema-less** → no fixed structure
* **Horizontal scalable** → easy to distribute
* **Fast for read/write**
* **Best for microservices & cloud apps**

---

#  **2. SQL vs MongoDB (Deep Explanation)**

### SQL mindset:

* Everything is structured
* Tables must have defined columns
* Need JOINs to connect tables
* Harder to scale horizontally
* Great for banking, transactions

### MongoDB mindset:

* Data stored like JSON
* Structure can change anytime
* No JOINs—fields can embed other documents
* Easy to scale across multiple machines
* Great for applications with constantly changing data

### Real Example:

A user profile in SQL needs multiple tables:

* users
* address
* preferences

MongoDB stores everything **inside one document**.

---

#  **3. Database & Collection — What They Actually Are**

* **Database** = folder
* **Collection** = sub-folder
* **Document** = file inside the sub-folder

Example:

```
revision_db (DB)
 └── employees (Collection)
      └── {name:"sujith", age:25} (Document)
```

### Why MongoDB creates DB automatically?

Because it only creates DB **when data is inserted**.
No empty DBs → saves memory.

---

#  **4. Insertting Documents (Deep Explanation)**

A document is inserted using `insertOne()` or `insertMany()`.

MongoDB stores everything as **BSON**, not pure JSON.
BSON supports types like:

* Date
* Binary
* ObjectId

Example:

```js
db.employees.insertOne({name:"sujith", age:25})
```

MongoDB automatically generates:

```
"_id": ObjectId("...")
```

This is the primary key of MongoDB.

---

#  **5. Reading Data (find() Explanation)**

### How `find()` works internally:

* It scans documents
* Compares with filter
* Returns matching documents

### Structure:

```
find( filter_document )
```

Example:

```js
db.employees.find({city:"chennai"})
```

Meaning:

* Look at each document
* If city equals “chennai”, return it

If filter is `{}`, it returns **everything**.

---

#  **6. Query Operators — Deep Meaning**

### `$gt` (greater than)

```js
{age: {$gt: 25}}
```

Means:
**age > 25**

### `$lte` (less than or equal)

```js
{age: {$lte: 30}}
```

### `$in`

```js
{city: {$in:["chennai","madurai"]}}
```

Means:
Return documents where **city is one of these values**.

---

#  **7. Sorting — How it works**

```js
db.employees.find().sort({age: -1})
```

Meaning:

* Sort all documents by age
* -1 = descending
* 1 = ascending

MongoDB sorts in memory unless indexed.

---

#  **8. Limit — What is its purpose**

```js
db.employees.find().limit(3)
```

Used when:

* Data is large
* Only want top results
* APIs return paginated data

---

#  **9. Update — Deep Explanation**

Updates use two parts:

```
updateOne( filter , update_operation )
```

Example:

```js
{$set: {age:26}}
```

### Why `$set`?

Because without `$set`, MongoDB replaces entire document.

---

# **10. Delete — Full Logic**

### deleteOne()

Deletes only the first match.

### deleteMany()

Deletes all matches.

MongoDB does NOT delete collection automatically if empty.

---

#  **11. Aggregation Framework — Complete Deep Explanation**

Aggregation pipeline works like this:

```
[ Stage 1 ] → [ Stage 2 ] → [ Stage 3 ] → result
```

Each stage transforms data.

### Why do we need Aggregation?

Because normal queries can’t do:

* Grouping
* Summing
* Averaging
* Data reshaping

---

## ** Understanding `$group` deeply**

Structure:

```js
{$group: { _id: <field_to_group_by>, <new_field>: <operation> }}
```

### Why `_id`?

In `$group`, `_id` means **group key**.

MongoDB says:
“Group all documents where this field has the same value.”

Example:

```js
_id:"$city"
```

Meaning:

* Group all employees from “chennai”
* Group all from “madurai”
* Group all from “theni”

### Why `$` symbol?

`$` tells MongoDB:
“This is a field inside document.”

`"city"` = string
`"$city"` = field “city” of document

### `$sum: 1`

Means: count 1 for each document.

Example:

```js
total: {$sum:1}
```

Counts number of documents per group.

### `$avg:"$age"`

Means: average of the age field.

---

#  **12. Indexes — Deep Meaning**

Indexes are like **page numbers in a book**.

Without index:

* MongoDB reads entire book → slow → “COLLSCAN”.

With index:

* MongoDB jumps to the exact page → fast → “IXSCAN”.

### Creating index:

```js
db.employees.createIndex({city:1})
```

### What does `1` mean?

Index sort direction:

* 1 = ascending
* -1 = descending

---

#  **13. Compound Index — Real Meaning**

Compound index:

```js
{city:1, age:1}
```

This means:

* First sort/group by city
* Inside city, sort by age

Used when queries use multiple fields.

---

#  **14. Query Plan (Explain) — Deep Meaning**

`explain("executionStats")` shows how MongoDB runs your query.

### COLLSCAN

Means: scanned all documents (slow)

### IXSCAN

Means: used index (fast)

Key fields:

* `totalDocsExamined`
* `totalKeysExamined`
* `stage`

---

#  **15. Backup & Restore — Deep Explanation**

### Backup:

`mongodump` exports database in BSON format.

### Restore:

`mongorestore` reconstructs database.

### Namespace mapping:

`--nsFrom="a.*" --nsTo="b.*"`

Renames database during restore.

---

#  **16. Users & Authentication — Deep Meaning**

MongoDB uses RBAC (Role Based Access Control):

* user
* role
* permission

### Create user:

```js
db.createUser({
  user:"root",
  pwd:"12345",
  roles:["root"]
})
```

### Why `--authenticationDatabase admin`?

Because MongoDB stores users inside **admin DB**.

---

#  **17. Mongod.conf — Important Sections**

Location:

```
/etc/mongod.conf
```

Important fields:

### storage.dbPath

Where your data lives.

### net.port

Default 27017.

### security.authorization

Enables auth.

---

#  **18. Storage Engine — Deep Meaning**

MongoDB uses **WiredTiger**:

* Multi-threaded
* Fast
* Compression
* Checkpoints

Better than older MMAPv1.

---

# **19. MongoDB Internal Rules**

✔ Writes are durable
✔ Index makes reads faster
✔ Aggregation runs in stages
✔ MongoDB only creates DB/collection on insert
✔ ObjectId is unique identifier
✔ BSON is internal format
✔ `$` symbol means “this is a field”

