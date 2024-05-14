Let's break down each of your queries with basic SQL examples:

### 1. How to Create a Table

To create a simple table named `Users` that stores user information:

```sql
CREATE TABLE Users (
    id INT PRIMARY KEY,
    username VARCHAR(50),
    email VARCHAR(100)
);
```

### 2. How to Insert into It

To insert a new record into the `Users` table:

```sql
INSERT INTO Users (id, username, email)
VALUES (1, 'john_doe', 'john.doe@example.com');
```

### 3. Creating Relationships

#### One-to-One Relationship

For a one-to-one relationship between `Users` and `Profiles`:

```sql
CREATE TABLE Profiles (
    id INT PRIMARY KEY,
    userId INT UNIQUE,
    bio TEXT,
    FOREIGN KEY (userId) REFERENCES Users(id)
);
```

Here, `userId` in `Profiles` is a foreign key that references `id` in `Users`, ensuring a one-to-one relationship through the `UNIQUE` constraint.

#### Many-to-Many Relationship

For a many-to-many relationship between `Students` and `Courses`, you need a join table, e.g., `Enrollments`:

```sql
CREATE TABLE Students (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE Courses (
    id INT PRIMARY KEY,
    title VARCHAR(100)
);

CREATE TABLE Enrollments (
    studentId INT,
    courseId INT,
    PRIMARY KEY (studentId, courseId),
    FOREIGN KEY (studentId) REFERENCES Students(id),
    FOREIGN KEY (courseId) REFERENCES Courses(id)
);
```

### 4. JOIN Queries

#### LEFT JOIN

Returns all records from the left table (`Users`), and the matched records from the right table (`Profiles`). The result is NULL on the right side if there is no match.

```sql
SELECT Users.username, Profiles.bio
FROM Users
LEFT JOIN Profiles ON Users.id = Profiles.userId;
```

#### INNER JOIN

Returns records that have matching values in both tables.

```sql
SELECT Students.name, Courses.title
FROM Enrollments
INNER JOIN Students ON Enrollments.studentId = Students.id
INNER JOIN Courses ON Enrollments.courseId = Courses.id;
```

#### RIGHT JOIN

Returns all records from the right table (`Profiles`), and the matched records from the left table (`Users`). The result is NULL on the left side if there is no match.

```sql
SELECT Users.username, Profiles.bio
FROM Users
RIGHT JOIN Profiles ON Users.id = Profiles.userId;
```

These examples cover basic SQL operations for table creation, data insertion, establishing relationships between tables, and performing different types of JOIN operations to query related data.