[[timetrackerER.excalidraw]]

## Creating Tables
```sql
CREATE DATABASE timetracker;
```

```sql
CREATE TABLE companies (id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(32));
```

```sql
CREATE TABLE users (id INT PRIMARY KEY AUTO_INCREMENT, username VARCHAR(32), password VARCHAR(32), email VARCHAR(32), company_id INT);
```

```sql
CREATE TABLE projects (id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(32), company_id INT);
```

```sql
CREATE TABLE tasks (id INT PRIMARY KEY AUTO_INCREMENT, status VARCHAR(32), project_id INT);
```

```sql
CREATE TABLE trackings (id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(32), description VARCHAR(32), start_time DATETIME, end_time DATETIME, isRunning BOOL, user_id INT);
```


## Adding FK- Constraints

```sql
ALTER TABLE users  
ADD FOREIGN KEY (company_id) REFERENCES companies(id);
```

```sql
ALTER TABLE projects 
ADD FOREIGN KEY (company_id) REFERENCES companies(id);
```

```sql
ALTER TABLE tasks  
ADD FOREIGN KEY (project_id) REFERENCES projects(id);
```

```sql
ALTER TABLE trackings 
ADD FOREIGN KEY (user_id) REFERENCES users(id);
```

---

## Insert Testdummy
```sql
INSERT INTO companies (name) VALUES ("admin AG");
```

```sql
INSERT INTO users (username, password, email, company_id)
	VALUES("admin","admin","admin@gmx.at",1);
```

```sql
INSERT INTO projects (name, company_id)
	VALUES("dummyprojekt",1);
```

```sql
INSERT INTO tasks (status, project_id)
	VALUES("in dummyprogress",1);
```

```sql
INSERT INTO trackings (name, description, start_time, end_time, isRunning, user_id)
VALUES("dummynametracking","dummydescription",
'2022-04-24 15:00:00', '2022-04-24 16:00:00 AM', false,2);
```