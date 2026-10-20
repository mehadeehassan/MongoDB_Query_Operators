### Doc Link
[MongoDB Query and Operators](https://docs.google.com/document/d/1gJ1U0Koi1PzxXpa_HBQR5-iQ6w0bhXE2SIF8DJBE64A/edit?tab=t.0)



# MongoDB Operators & Queries

Job Portal (Bdjobs / LinkedIn-এর মতো) থিমের ২০টি fake job document নিয়ে MongoDB operator প্র্যাকটিস।

## সূচিপত্র

1. [Fake Data তৈরি](#1-fake-data-তৈরি)
2. [Comparison Operators](#2-comparison-operators)
3. [Logical Operators](#3-logical-operators)
4. [Element & Type Operators](#4-element--type-operators)
5. [Array Query Operators](#5-array-query-operators)
6. [Update Operators](#6-update-operators)
7. [Projection & Sorting](#7-projection--sorting)
8. [Aggregation Pipeline](#8-aggregation-pipeline)
9. [Advanced Aggregation](#9-advanced-aggregation)
10. [Module Summary & Capstone](#10-module-summary--capstone)
11. [Cheat Sheet](#11-cheat-sheet)
12. [Known Gotchas](#12-known-gotchas)

---

## 1. Fake Data তৈরি

`jobs` collection-এ ২০টি ডকুমেন্ট ইনসার্ট করুন। পুরো মডিউলে এই ডেটাই ব্যবহার হবে।

```js
db.jobs.insertMany([
  { "title": "Software Engineer", "company": "TechCorp Bangladesh", "location": "Dhaka", "salary": 75000, "experience": 3, "skills": ["JavaScript", "Node.js", "MongoDB"], "isRemote": false, "applicants": 120, "posted": "2024-01-15T00:00:00.000Z", "status": "active", "department": "Engineering" },
  { "title": "Frontend Developer", "company": "Digital Solutions", "location": "Chittagong", "salary": 55000, "experience": 2, "skills": ["React", "CSS", "JavaScript"], "isRemote": true, "applicants": 85, "posted": "2024-02-10T00:00:00.000Z", "status": "active", "department": "Engineering" },
  { "title": "Data Analyst", "company": "InsightHub", "location": "Dhaka", "salary": 60000, "experience": 4, "skills": ["Python", "SQL", "Excel"], "isRemote": false, "applicants": 200, "posted": "2024-01-20T00:00:00.000Z", "status": "active", "department": "Analytics" },
  { "title": "DevOps Engineer", "company": "CloudBase Ltd", "location": "Sylhet", "salary": 90000, "experience": 5, "skills": ["Docker", "Kubernetes", "AWS"], "isRemote": true, "applicants": 45, "posted": "2024-03-01T00:00:00.000Z", "status": "closed", "department": "Infrastructure" },
  { "title": "UI/UX Designer", "company": "CreativeMinds", "location": "Dhaka", "salary": 50000, "experience": 2, "skills": ["Figma", "Adobe XD", "Sketch"], "isRemote": false, "applicants": 150, "posted": "2024-02-25T00:00:00.000Z", "status": "active", "department": "Design" },
  { "title": "Backend Developer", "company": "ServerStack", "location": "Dhaka", "salary": 80000, "experience": 4, "skills": ["Python", "Django", "PostgreSQL"], "isRemote": true, "applicants": 95, "posted": "2024-01-05T00:00:00.000Z", "status": "active", "department": "Engineering" },
  { "title": "Project Manager", "company": "ManagePro BD", "location": "Dhaka", "salary": 95000, "experience": 7, "skills": ["Agile", "Scrum", "Jira"], "isRemote": false, "applicants": 60, "posted": "2024-03-10T00:00:00.000Z", "status": "active", "department": "Management" },
  { "title": "QA Engineer", "company": "BugFree Tech", "location": "Rajshahi", "salary": 45000, "experience": 1, "skills": ["Selenium", "JIRA", "Testing"], "isRemote": false, "applicants": 30, "posted": "2024-02-15T00:00:00.000Z", "status": "active", "department": "Quality" },
  { "title": "Machine Learning Engineer", "company": "AIVentures", "location": "Dhaka", "salary": 120000, "experience": 6, "skills": ["Python", "TensorFlow", "ML"], "isRemote": true, "applicants": 75, "posted": "2024-03-05T00:00:00.000Z", "status": "active", "department": "AI" },
  { "title": "Database Administrator", "company": "DataKeep BD", "location": "Dhaka", "salary": 70000, "experience": 5, "skills": ["MySQL", "MongoDB", "Redis"], "isRemote": false, "applicants": 40, "posted": "2024-01-30T00:00:00.000Z", "status": "closed", "department": "Engineering" },
  { "title": "Mobile Developer", "company": "AppFactory", "location": "Chittagong", "salary": 65000, "experience": 3, "skills": ["Flutter", "React Native", "Dart"], "isRemote": true, "applicants": 110, "posted": "2024-02-20T00:00:00.000Z", "status": "active", "department": "Mobile" },
  { "title": "Cybersecurity Analyst", "company": "SecureNet BD", "location": "Dhaka", "salary": 85000, "experience": 4, "skills": ["Ethical Hacking", "Firewalls", "SIEM"], "isRemote": false, "applicants": 25, "posted": "2024-03-08T00:00:00.000Z", "status": "active", "department": "Security" },
  { "title": "Technical Writer", "company": "DocsFirst", "location": "Remote", "salary": 40000, "experience": 2, "skills": ["Markdown", "Technical Writing", "Git"], "isRemote": true, "applicants": 55, "posted": "2024-02-05T00:00:00.000Z", "status": "active", "department": "Documentation" },
  { "title": "Cloud Architect", "company": "SkyInfra", "location": "Dhaka", "salary": 130000, "experience": 8, "skills": ["AWS", "Azure", "GCP"], "isRemote": true, "applicants": 35, "posted": "2024-01-25T00:00:00.000Z", "status": "active", "department": "Infrastructure" },
  { "title": "React Developer", "company": "WebWorks BD", "location": "Dhaka", "salary": 58000, "experience": 2, "skills": ["React", "Redux", "TypeScript"], "isRemote": false, "applicants": 180, "posted": "2024-03-12T00:00:00.000Z", "status": "active", "department": "Engineering" },
  { "title": "HR Manager", "company": "PeopleFirst BD", "location": "Dhaka", "salary": 55000, "experience": 5, "skills": ["Recruitment", "HR Policies", "Payroll"], "isRemote": false, "applicants": 70, "posted": "2024-02-28T00:00:00.000Z", "status": "active", "department": "HR" },
  { "title": "Network Engineer", "company": "NetConnect BD", "location": "Khulna", "salary": 62000, "experience": 3, "skills": ["Cisco", "Networking", "Firewall"], "isRemote": false, "applicants": 20, "posted": "2024-01-18T00:00:00.000Z", "status": "closed", "department": "Infrastructure" },
  { "title": "Blockchain Developer", "company": "ChainTech BD", "location": "Dhaka", "salary": 110000, "experience": 5, "skills": ["Solidity", "Web3.js", "Ethereum"], "isRemote": true, "applicants": 15, "posted": "2024-03-15T00:00:00.000Z", "status": "active", "department": "Blockchain" },
  { "title": "Business Analyst", "company": "Analyse Pro", "location": "Dhaka", "salary": 68000, "experience": 4, "skills": ["Excel", "PowerBI", "SQL"], "isRemote": false, "applicants": 90, "posted": "2024-02-12T00:00:00.000Z", "status": "active", "department": "Analytics" },
  { "title": "Intern Developer", "company": "StartupHub BD", "location": "Dhaka", "salary": 15000, "experience": 0, "skills": ["HTML", "CSS", "JavaScript"], "isRemote": false, "applicants": 350, "posted": "2024-03-20T00:00:00.000Z", "status": "active", "department": "Engineering" }
])
```

সফল হলে: `acknowledged: true, insertedCount: 20`

### ভেরিফিকেশন

```js
db.jobs.countDocuments()   // 20
db.jobs.findOne()          // প্রথম ডকুমেন্ট
```

---

## 2. Comparison Operators

| Operator | অর্থ |
|---|---|
| `$eq` | সমান |
| `$ne` | সমান না |
| `$gt` | বড় |
| `$gte` | বড় বা সমান |
| `$lt` | ছোট |
| `$lte` | ছোট বা সমান |

### `$eq` — শুধু Dhaka-র চাকরি

```js
db.jobs.find({ location: { $eq: "Dhaka" } })
// সংক্ষেপে (একই কাজ)
db.jobs.find({ location: "Dhaka" })
```

> `$eq` MongoDB-এর default behavior, তাই `{ field: value }` লিখলেও একই কাজ হয়।

### `$ne` — Dhaka ছাড়া বাকি সব

```js
db.jobs.find({ location: { $ne: "Dhaka" } })
```

### `$gt` — ৭০ হাজারের বেশি বেতন

```js
db.jobs.find({ salary: { $gt: 70000 } })
```

### `$gte` — ৭০ হাজার বা তার বেশি

```js
db.jobs.find({ salary: { $gte: 70000 } })
```

### `$lt` — ৫০ হাজারের কম

```js
db.jobs.find({ salary: { $lt: 50000 } })
```

### `$lte` — ৫০ হাজার বা কম

```js
db.jobs.find({ salary: { $lte: 50000 } })
```

### একাধিক Comparison Operator একসাথে

```js
// ৫০ হাজার থেকে ৯০ হাজারের মধ্যে
db.jobs.find({ salary: { $gte: 50000, $lte: 90000 } })

// ৩ বছরের বেশি experience এবং ৬০ হাজারের বেশি বেতন
db.jobs.find({ experience: { $gt: 3 }, salary: { $gt: 60000 } })
```

> একই ফিল্ডে একাধিক শর্ত AND হিসেবে কাজ করে।

---

## 3. Logical Operators

### `$and` — সব শর্ত সত্য হতে হবে

```js
db.jobs.find({
  $and: [
    { location: "Dhaka" },
    { salary: { $gt: 70000 } }
  ]
})

// implicit $and
db.jobs.find({ location: "Dhaka", salary: { $gt: 70000 } })
```

> একই ফিল্ডে দুটো শর্ত দিতে হলে `$and` লাগে (বা একই অবজেক্টে operator মিলিয়ে লিখতে হয়)। আলাদা ফিল্ডে হলে implicit `$and`-ই যথেষ্ট।

### `$or` — যেকোনো একটা শর্ত সত্য হলেই হবে

```js
// Dhaka অথবা Chittagong
db.jobs.find({
  $or: [
    { location: "Dhaka" },
    { location: "Chittagong" }
  ]
})

// বেতন ১ লাখের বেশি অথবা Remote
db.jobs.find({
  $or: [
    { salary: { $gt: 100000 } },
    { isRemote: true }
  ]
})
```

### `$not` — শর্তের বিপরীত

```js
// ৫০ হাজারের বেশি নয় (৫০ হাজার বা কম)
db.jobs.find({ salary: { $not: { $gt: 50000 } } })
```

> `$not` সবসময় operator expression-এর ভেতরে ব্যবহার হয়, সরাসরি ভ্যালুর সাথে না।

### `$nor` — সব শর্ত মিথ্যা হতে হবে

```js
// Dhaka-তেও না, Remote-ও না
db.jobs.find({
  $nor: [
    { location: "Dhaka" },
    { isRemote: true }
  ]
})
```

---

## 4. Element & Type Operators

এগুলো ভ্যালু তুলনা করে না — ফিল্ড আছে কিনা বা ডেটার ধরন কী, সেটা চেক করে।

### `$exists`

```js
db.jobs.find({ salary: { $exists: true } })
db.jobs.find({ salary: { $exists: false } })
```

প্র্যাকটিসের জন্য salary ছাড়া একটা ডকুমেন্ট:

```js
db.jobs.insertOne({
  title: "Unpaid Intern",
  company: "StartupXYZ",
  location: "Dhaka",
  experience: 0
})

db.jobs.find({ salary: { $exists: false } })  // শুধু Unpaid Intern
```

### `$type`

```js
db.jobs.find({ salary: { $type: "number" } })
db.jobs.find({ skills: { $type: "array" } })
db.jobs.find({ posted: { $type: "date" } })
```

**Common BSON Types**

| Type | Code | বর্ণনা |
|---|---|---|
| double | 1 | দশমিক সংখ্যা |
| string | 2 | টেক্সট |
| object | 3 | embedded document |
| array | 4 | অ্যারে |
| boolean | 8 | true/false |
| date | 9 | তারিখ |
| null | 10 | null |
| int | 16 | পূর্ণসংখ্যা |

> ডেটা ভ্যালিডেশন ও মিশ্র ডেটা ক্লিনআপে কাজে লাগে।

---

## 5. Array Query Operators

### `$in` — যেকোনো একটা ম্যাচ করলেই হবে

```js
db.jobs.find({ skills: { $in: ["Python", "JavaScript"] } })
db.jobs.find({ location: { $in: ["Dhaka", "Chittagong", "Sylhet"] } })
```

### `$nin` — লিস্টের কোনোটাই থাকবে না

```js
db.jobs.find({ skills: { $nin: ["Python", "JavaScript"] } })
```

### `$all` — সবগুলো থাকতে হবে

```js
db.jobs.find({ skills: { $all: ["Python", "SQL"] } })
```

> `$in` = যেকোনো একটা, `$all` = সবগুলো।

### `$size` — অ্যারের exact সাইজ

```js
db.jobs.find({ skills: { $size: 3 } })
```

> `$size` range (greater/less than) সাপোর্ট করে না। সেক্ষেত্রে `$expr` + `$size` বা aggregation ব্যবহার করুন।

### `$elemMatch` — অ্যারের একটি এলিমেন্টে একাধিক শর্ত

```js
db.jobs.insertOne({
  title: "Senior Developer",
  company: "BigTech",
  interviews: [
    { round: 1, score: 85, passed: true },
    { round: 2, score: 70, passed: false }
  ]
})

db.jobs.find({
  interviews: {
    $elemMatch: { score: { $gt: 80 }, passed: true }
  }
})
```

> `$elemMatch` ছাড়া শর্তগুলো আলাদা আলাদা এলিমেন্টে মিললেও ডকুমেন্ট ম্যাচ করতো। `$elemMatch` নিশ্চিত করে **একই এলিমেন্টে** সব শর্ত পূরণ হয়েছে।

---

## 6. Update Operators

### `$set`

```js
db.jobs.updateOne(
  { title: "Software Engineer", company: "TechCorp Bangladesh" },
  { $set: { salary: 80000 } }
)

// একাধিক ফিল্ড
db.jobs.updateOne(
  { title: "Software Engineer" },
  { $set: { salary: 80000, status: "hiring", updatedAt: new Date() } }
)
```

### `$inc`

```js
db.jobs.updateOne({ title: "Data Analyst" }, { $inc: { applicants: 10 } })
db.jobs.updateOne({ title: "Data Analyst" }, { $inc: { applicants: -5 } })
```

### `$push`

```js
db.jobs.updateOne(
  { title: "Frontend Developer" },
  { $push: { skills: "TypeScript" } }
)

// একাধিক আইটেম
db.jobs.updateOne(
  { title: "Frontend Developer" },
  { $push: { skills: { $each: ["TypeScript", "GraphQL"] } } }
)
```

### `$pull`

```js
db.jobs.updateOne(
  { title: "UI/UX Designer" },
  { $pull: { skills: "Sketch" } }
)
```

### `$addToSet` — duplicate ছাড়া যোগ

```js
db.jobs.updateOne(
  { title: "Frontend Developer" },
  { $addToSet: { skills: "TypeScript" } }
)
```

> `$push` duplicate যোগ করতে পারে, `$addToSet` পারে না।

---

## 7. Projection & Sorting

### Projection

```js
// Include
db.jobs.find({}, { title: 1, company: 1, salary: 1 })
db.jobs.find({}, { title: 1, company: 1, salary: 1, _id: 0 })

// Exclude
db.jobs.find({}, { _id: 0, applicants: 0 })
```

> Include ও Exclude একসাথে ব্যবহার করা যায় না (`_id` ব্যতিক্রম)।

### Sorting

`1` = ascending, `-1` = descending

```js
db.jobs.find({}, { title: 1, salary: 1, _id: 0 }).sort({ salary: -1 })

// মাল্টি-ফিল্ড
db.jobs.find().sort({ location: 1, salary: -1 })
```

### `limit()` ও `skip()` — Pagination

```js
db.jobs.find().limit(5)
db.jobs.find().skip(5).limit(5)   // Page 2 (প্রতি পেজে ৫টা)

db.jobs.find(
  { status: "active" },
  { title: 1, salary: 1, company: 1, _id: 0 }
).sort({ salary: -1 }).skip(5).limit(5)
```

---

## 8. Aggregation Pipeline

এক স্টেজের আউটপুট পরের স্টেজের ইনপুট — assembly line-এর মতো।

### `$match`

```js
db.jobs.aggregate([
  { $match: { status: "active" } }
])
```

> `$match` সাধারণত pipeline-এর শুরুতে দিন, ডেটা কমে গেলে পরের স্টেজ দ্রুত হয় (এবং index ব্যবহার করা যায়)।

### `$group`

```js
// প্রতি শহরে কতটা চাকরি
db.jobs.aggregate([
  { $group: { _id: "$location", totalJobs: { $sum: 1 } } }
])

// প্রতি শহরে বেতনের পরিসংখ্যান
db.jobs.aggregate([
  { $group: {
    _id: "$location",
    avgSalary: { $avg: "$salary" },
    maxSalary: { $max: "$salary" },
    minSalary: { $min: "$salary" },
    totalJobs: { $sum: 1 }
  }}
])
```

**Accumulators:** `$sum` · `$avg` · `$max` · `$min` · `$push`

### `$project`

```js
db.jobs.aggregate([
  { $project: { title: 1, company: 1, _id: 0 } }
])

// calculated field
db.jobs.aggregate([
  { $project: {
    title: 1,
    salary: 1,
    monthlySalary: "$salary",
    annualSalary: { $multiply: ["$salary", 12] }
  }}
])
```

### Match + Group + Project + Sort

```js
db.jobs.aggregate([
  { $match: { status: "active" } },
  { $group: {
    _id: "$department",
    avgSalary: { $avg: "$salary" },
    jobCount: { $sum: 1 }
  }},
  { $project: {
    department: "$_id",
    avgSalary: { $round: ["$avgSalary", 0] },
    jobCount: 1,
    _id: 0
  }},
  { $sort: { avgSalary: -1 } }
])
```

---

## 9. Advanced Aggregation

### Setup: `companies` collection

```js
db.companies.insertMany([
  { name: "TechCorp Bangladesh", founded: 2015, employees: 500, industry: "Software" },
  { name: "Digital Solutions", founded: 2018, employees: 120, industry: "Web" },
  { name: "AIVentures", founded: 2020, employees: 80, industry: "AI/ML" },
  { name: "CloudBase Ltd", founded: 2017, employees: 200, industry: "Cloud" },
  { name: "CreativeMinds", founded: 2019, employees: 50, industry: "Design" }
]);
```

### `$lookup` — Join (SQL JOIN-এর মতো)

```js
db.jobs.aggregate([
  {
    $lookup: {
      from: "companies",
      localField: "company",
      foreignField: "name",
      as: "companyDetails"
    }
  },
  { $project: { title: 1, salary: 1, companyDetails: 1, _id: 0 } },
  { $limit: 5 }
])
```

> `companyDetails` অ্যারে হিসেবে আসে; flat করতে `$unwind` ব্যবহার করুন।

### `$unwind` — অ্যারে flat করা

```js
db.jobs.aggregate([
  {
    $lookup: {
      from: "companies",
      localField: "company",
      foreignField: "name",
      as: "companyDetails"
    }
  },
  { $unwind: "$companyDetails" },
  {
    $project: {
      title: 1,
      salary: 1,
      "companyDetails.industry": 1,
      "companyDetails.employees": 1,
      _id: 0
    }
  }
])
```

> `$unwind` ডিফল্টভাবে খালি/অনুপস্থিত অ্যারের ডকুমেন্ট বাদ দেয়। রাখতে চাইলে `{ $unwind: { path: "$companyDetails", preserveNullAndEmptyArrays: true } }`।

### `$facet` — একসাথে একাধিক analysis

```js
db.jobs.aggregate([
  { $match: { status: "active" } },
  {
    $facet: {
      salaryBuckets: [
        { $bucket: {
          groupBy: "$salary",
          boundaries: [0, 30000, 60000, 90000, 150000],
          default: "Other",
          output: { count: { $sum: 1 }, avgSalary: { $avg: "$salary" } }
        }}
      ],
      byLocation: [
        { $group: { _id: "$location", total: { $sum: 1 } } },
        { $sort: { total: -1 } }
      ],
      byDepartment: [
        { $group: { _id: "$department", avgSalary: { $avg: "$salary" } } },
        { $sort: { avgSalary: -1 } },
        { $limit: 5 }
      ]
    }
  }
])
```

> Dashboard-এর সব ডেটা একটাই কুয়েরিতে। তবে `$facet`-এর আউটপুট একটাই ডকুমেন্ট এবং ১৬MB BSON লিমিটের ভেতরে থাকতে হয়।

---

## 10. Module Summary & Capstone

| বিষয় | Operators |
|---|---|
| Comparison | `$eq` `$ne` `$gt` `$gte` `$lt` `$lte` |
| Logical | `$and` `$or` `$not` `$nor` |
| Element & Type | `$exists` `$type` |
| Array | `$in` `$nin` `$all` `$size` `$elemMatch` |
| Update | `$set` `$inc` `$push` `$pull` `$addToSet` |
| Projection & Sorting | include/exclude, `sort()`, `limit()`, `skip()` |
| Aggregation | `$match` `$group` `$project` |
| Advanced Aggregation | `$lookup` `$unwind` `$facet` |

### Capstone Query

**Scenario:** HR Team-এর রিপোর্ট — Dhaka বা Remote-এর active চাকরি, ৩+ বছর experience, department অনুযায়ী গড় বেতন, মোট jobs ও সর্বোচ্চ applicants, গড় বেতন অনুযায়ী sorted।

```js
db.jobs.aggregate([
  // Step 1: ফিল্টার
  { $match: {
    $or: [{ location: "Dhaka" }, { isRemote: true }],
    status: "active",
    experience: { $gte: 3 }
  }},

  // Step 2: Department অনুযায়ী group
  { $group: {
    _id: "$department",
    avgSalary: { $avg: "$salary" },
    totalJobs: { $sum: 1 },
    maxApplicants: { $max: "$applicants" },
    topJob: { $first: "$title" }
  }},

  // Step 3: আউটপুট সাজানো
  { $project: {
    department: "$_id",
    avgSalary: { $round: ["$avgSalary", 0] },
    totalJobs: 1,
    maxApplicants: 1,
    topJob: 1,
    _id: 0
  }},

  // Step 4: গড় বেতন অনুযায়ী sort
  { $sort: { avgSalary: -1 } }
])
```

---

## 11. Cheat Sheet

| Category | Operators |
|---|---|
| Comparison | `$eq` `$ne` `$gt` `$gte` `$lt` `$lte` |
| Logical | `$and` `$or` `$not` `$nor` |
| Element | `$exists` `$type` |
| Array | `$in` `$nin` `$all` `$size` `$elemMatch` |
| Update | `$set` `$inc` `$push` `$pull` `$addToSet` |
| Aggregation | `$match` `$group` `$project` `$sort` `$limit` `$skip` `$lookup` `$unwind` `$facet` |

### পরবর্তী ধাপ

- MongoDB Indexes — কুয়েরি দ্রুত করা
- Mongoose ODM — Node.js-এর সাথে ব্যবহার
- MongoDB Atlas — Cloud Database
- Transactions
- Schema Validation

---

## 12. Known Gotchas

মূল নোটের কিছু জায়গা প্র্যাকটিসের সময় ভিন্ন ফল দেবে:

1. **`posted` ফিল্ড string, Date নয়।** `insertMany`-তে `"2024-01-15T00:00:00.000Z"` string হিসেবেই সেভ হয়, তাই `{ posted: { $type: "date" } }` কিছুই ফেরত দেবে না। Date হিসেবে ইনসার্ট করতে `new Date("2024-01-15T00:00:00.000Z")` ব্যবহার করুন, অথবা পরে কনভার্ট করুন:
   ```js
   db.jobs.updateMany(
     { posted: { $type: "string" } },
     [{ $set: { posted: { $toDate: "$posted" } } }]
   )
   ```
2. **Extra ডকুমেন্ট।** `Unpaid Intern` ও `Senior Developer` ইনসার্ট করলে `countDocuments()` ২২ হয়ে যায়। `$not: { $gt: 50000 }`, `$nin` ইত্যাদি `salary`/`skills` না থাকা ডকুমেন্টও ম্যাচ করে।
3. **`$nor` উদাহরণের ফলাফল।** `Technical Writer`-এর `location` হলো `"Remote"` (শহর নয়), আর Chittagong/Sylhet-এর চাকরিগুলো `isRemote: true`। তাই `$nor: [{location: "Dhaka"}, {isRemote: true}]` শুধু Rajshahi (QA Engineer) ও Khulna (Network Engineer) ফেরত দেয়।
4. **`$set` উদাহরণে `status: "hiring"`** ডেটা বদলে দেয়; পরে `status: "active"` ফিল্টারে ওই ডকুমেন্ট বাদ পড়বে।
5. **Capstone-এ `topJob` ভুল।** `$first: "$title"` গ্রুপের প্রথম ডকুমেন্টের title দেয়, সর্বোচ্চ applicant-এর job নয় (কারণ আগে sort করা নেই)। সঠিক উপায়:
   ```js
   { $sort: { applicants: -1 } },              // $group-এর আগে
   { $group: {
       _id: "$department",
       avgSalary: { $avg: "$salary" },
       totalJobs: { $sum: 1 },
       maxApplicants: { $max: "$applicants" },
       topJob: { $first: "$title" }            // এখন সর্বোচ্চ applicant-এর title
   }}
   ```
   MongoDB 5.2+ হলে `$top: { sortBy: { applicants: -1 }, output: "$title" }`-ও ব্যবহার করা যায়।
6. **Pagination।** বড় collection-এ `skip()` ধীর হয়ে যায়; production-এ range-based (`_id` বা sort key ধরে) pagination ভালো।