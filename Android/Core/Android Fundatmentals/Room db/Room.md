- It is an abstraction over SQLite.
- It provides 
	- Compile time verification of SQL queries
	- Reduces boiler plate 
	- Integrate well with jetpack components like `liveData` and [[Flow]]
## Components 
- Entity - represents a table in database 
- DAO (Data Access Object) - provides an interface to access the database 
- Data base class - Main access point for the connection to your app's  db. 
## Annotations 
- `@Entity`
- `@PrimaryKey`
- `@ColumnInfo` - customize column name 
- `@Ignore` - tells room not to persist field 
- `@`[[#Transactions]] - ensure a method is executed within a single transaction 
- `@TypeConverters` - Used to store custom types like data or list 
- `@Embedded` - Flattens the object. Takes all the fields of the object, and adds column into that object. 
- `@Relation`

## Transactions
- It all or nothing for data 
- A system crash or simple error in middle of process could leave database in half finished state. 
- It guarantees [[ACID]] properties 

## Junction 
It tells room how tables are connect in many  - many relationship. 