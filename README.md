# Personal-JDBC-Utils
This is my personal jdbc utilities library to help me reduce retyping stuff mainly `(ie. Creating connection, closing connection)`.
The user is still responsible for setting the query parameters.

## Gradle
```groovy
repositories {
    jcenter()
}
dependencies {
  compile 'com.budinverse.utils:Personal-JDBC-Utils:0.1'
}

```

## How to use?

1. Create a Config.json file with the following details inside and put it at root directory of project. You should be able to 
use the library already.
```json
{
  "databaseName":"yourDatabaseName",
  "databaseUser":"yourDatabaseUsername",
  "databasePassword":"yourDatabasePassword"
}
```

2. INSERT/UPDATE/DELETE Statements
Assuming you have a Person class and you want to insert into the person table.
```kotlin
data class Person(val name:String, val age: Int)
.
.
.

/* Example */
fun insertPerson(person:Person) = manipulate("INSERT INTO person VALUES (?,?)",{
  it.setString(1,person.name)
  it.setInt(2,person.age)
})
```

3. Query Single Result.
Assume that there is an extension function that converts ResultSet to to Person object
```kotlin

/* Example */
fun getPersonByName(name:String) = query("SELECT * FROM person WHERE name = ?", {
  it.setString(1,name)
}, { it.toPerson() })

```

4. Query Multiple Results.
Multiple results returns and arraylist of said object
```kotlin

/* Example */
fun getPersons() = queryMulti("SELECT * FROM person WHERE name = ?", {
  it.setString(1,name)
}, { it.toPerson() })

```
