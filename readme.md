# 1. What is PostgreSQL?

## উত্তর :

PostgreSQL একটি শক্তিশালী, ওপেন-সোর্স অবজেক্ট-রিলেশনাল ডাটাবেস সিস্টেম । PostgreSQL রিলেশনাল এবং নন-রিলেশনাল উভয় ধরণের কোয়েরি করতে পারে , যা এটিকে বিভিন্ন অ্যাপ্লিকেশনের জন্য উপযুক্ত করে তোলে। এটি SQL ভাষা ব্যবহার করে ডাটাবেজে সাথে যোগাযোগ করে।

### PostgreSQL ব্যবহার

- টেবিল তৈরি করে সেখানে তথ্য সংরক্ষণ করতে পারি।
- তথ্য খুঁজে বের করতে পারি।
- প্রয়োজনে তথ্য আপডেট বা মুছেও ফেলতে পারি।

# 2. Explain the Primary Key and Foreign Key concepts in PostgreSQL.

## উত্তর :

### Primary Key

Primary Key হলো যেকোনো টেবিলের একটি গুরুত্বপূর্ণ কলাম , যার মাধ্যমে প্রতিটি row বা রেকর্ডকে আলাদাভাবে শনাক্ত করা যায়। এই কলাম সবসময় unique এবং NOT NULL হতে হবে।

উদাহরণ: Student Table

```
| StudentID | Email          | Phone       |
|-----------|----------------|-------------|
| 1         | rafi@mail.com  | 013000000   |
```

এখানে `Student` টেবিলের `StudentID` কলাম কলাম হচ্ছে **Primary Key** কারণ এটি আমাদের প্রতিটি row কে ইউনিকভাবে সনাক্ত করে

### Foreign Key

Foreign Key হলো এমন একটি কলাম যেটি এক টেবিলের প্রাইমারি key-কে অন্য টেবিলে রেফার করে। এটি মূলত দুইটি টেবিলের মধ্যে সম্পর্ক তৈরি করতে ব্যবহৃত হয়।

উদাহরণ: Result Table

```
| ResultID | StudentID (Foreign Key) | Grade |
|----------|--------------------------|-------|
| 101      | 1                        | A     |
| 102      | 2                        | B+
```

এখানে `Results` টেবিলের `StudentID` কলাম একটি **Foreign Key** । এটির মাধ্যমে আমরা দুটি টেবিলের মধ্যে সম্পর্ক তৈরি করতে পারতেছি

# 3. What is the difference between the VARCHAR and CHAR data types?

## VARCHAR – SQL String Data Type :

- এটি একটি স্ট্রিং টাইপ যেখানে আমরা বলে দিতে পারি সর্বোচ্চ কতটি ক্যারেক্টার রাখা যাবে

- যদি নির্ধারিত সীমার চেয়ে বেশি ক্যারেক্টার দিই তাহলে `error` দিবে।

- কিন্তু যদি কম ক্যারেক্টার দিই তাহলে কোনো `error` দিবে না, ঠিক যেটুকু আছে সেটুকুই গ্রহণ করবে।

### Example:

```
CREATE TABLE students (
  name VARCHAR(50)
)
```

## CHAR – SQL String Data Type:

- এটি একটি স্ট্রিং টাইপ যেখানে যতগুলো ক্যারেক্টার নির্ধারণ করা হয় PostgreSQL ততটুকু জায়গা ধরে রাখে।

- যদি ইনসার্ট করার সময় ক্যারেক্টার সংখ্যা কম হয় তাহলে ফাঁকা স্পেস দিয়ে বাকি অংশ পূরণ করে।

- তাই CHAR সব সময় নির্দিষ্ট দৈর্ঘ্যের স্ট্রিং ধারণ করে, চাইলেও তার কম জায়গা নেবে না।

### Example:

```
 CREATE TABLE users (
    gender CHAR(10)
);

```

# 4. What is the significance of the JOIN operation, and how does it work in PostgreSQL?

## উত্তর :

JOIN হলো SQL-এর এমন একটি শক্তিশালী অপারেশন, যার সাহায্যে আমরা দুই বা ততোধিক টেবিলের মধ্যে সম্পর্ক তৈরি করে একসাথে ডেটা আনতে পারি। আমরা সাধারণত ডেটাবেসে সব তথ্য এক টেবিলে রাখি না। বরং, আলাদা টেবিলে আলাদা ধরনের তথ্য রাখি। এই JOIN না থাকলে, একাধিক টেবিল থেকে ডেটা একসাথে পাওয়া অত্যন্ত কঠিন হয়ে যেত।

## How does JOIN work in PostgreSQL?

PostgreSQL-এ JOIN করার সময় সাধারণত common column ব্যবহার করে ডেটা দেখানো হয়।

### students টেবিল:

```
| id  | name  |
| --- | ----- |
| 1   | Mim   |
| 2   | Rafi  |
```

### Courses টেবিল:

```
| id  | student_id (FK) | course_name |
| --- | --------------- | ----------- |
| 1   | 1               | React       |
| 2   | 2               | Node.js     |
```

### PostgreSQL JOIN syntax:

```
SELECT students.name, courses.course_name
FROM students
JOIN courses
ON students.id = courses.student_id;
```

এখানে students.id এবং courses.student_id এর মাধ্যমে PostgreSQL দুই টেবিলকে JOIN করেছে। JOIN অপারেশনের ক্ষেত্রে সাধারণত আমরা foreign key ব্যবহার করে থাকি।

# 5. How can you modify data using UPDATE statements?

## উত্তর :

আমরা যখন ডেটাবেজে থাকা কোন তথ্য পরিবর্তন করতে চাই, তখন UPDATE স্টেটমেন্ট ব্যবহার করি। UPDATE করার সময় WHERE clause ব্যবহার করতে হবে। যদি ব্যবহার না করি তাহলে পুরো টেবিলের সব row আপডেট হয়ে যাবে

### UPDATE Syntax:

```
UPDATE table_name
   SET column1 = value1
WHERE condition;
```

### UPDATE Example:

`students টেবিল`

```
| id | name  |
| -- | ----- |
| 1  | Mukit |
| 2  | Rafi  |

```

Mukit এর নাম পরিবর্তন করে `Md. Mukit Hasan` করতে তাহলে update কোড হবে:

```
UPDATE students
  SET name = 'Md. Mukit Hasan'
WHERE id = 1;
```
