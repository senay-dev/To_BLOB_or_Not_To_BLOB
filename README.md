# To_BLOB_or_Not_To_BLOB
# Choosing an Efficient way of Storing User Profile Pictures


# `User` table schema
`DESCRIBE USER;`
| Field    | Type        | Null | Key | Default | Extra          |
|----------|-------------|------|-----|---------|----------------|
| user_id  | int         | NO   | PRI | NULL    | auto_increment |
| username | varchar(45) | NO   |     | NULL    |                |
| password | varchar(45) | NO   |     | NULL    |                |
| image    | ??       | YES  |     | NULL    |                |


## Task

Compare storing an image in the SQL database vs storing it in a file system, in our case in the cloud, and store an ID in the SQL table as a reference to the data

## Methods

Based on a Microsoft research study "To BLOB or Not To BLOB: Large Object Storage in a Database or a Filesystem?" by van Ingen et. al., they concluded **"if objects are larger than one megabyte on average, NTFS has a clear advantage over SQL Server. If the objects are under 256 kilobytes, the database has a clear advantage."**


## Data Type of our image column

Given a profile picture of a user is generally less than 256 KB the most efficient way to store the table will be saving the image as a `blob`.

## CREATE Statement of the User Table
`CREATE TABLE user 
(
  user_id int NOT NULL AUTO_INCREMENT,
  username varchar(45) NOT NULL,
  password varchar(45) NOT NULL,
  image blob,
  PRIMARY KEY (user_id)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
`

## Final Schema of User Table
| Field    | Type        | Null | Key | Default | Extra          |
|----------|-------------|------|-----|---------|----------------|
| user_id  | int         | NO   | PRI | NULL    | auto_increment |
| username | varchar(45) | NO   |     | NULL    |                |
| password | varchar(45) | NO   |     | NULL    |                |
| image    | blob        | YES  |     | NULL    |                |



# References
Russell Sears, Catharine Van Ingen, Jim Gray (2007).
To BLOB or Not To BLOB: Large Object Storage in a Database or a Filesystem?
https://arxiv.org/abs/cs/0701168
