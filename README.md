# room
**Room Database in Kotlin: A Beginner's Guide**

Welcome to the beginner's guide to Room Database in Kotlin! Room is a part of the Android Jetpack library and provides an abstraction layer over SQLite to allow for more robust database access while harnessing the full power of SQLite.

## What is Room Database?

Room is an Android library that acts as an abstraction layer over SQLite database. It simplifies database interactions and provides compile-time checks which help catch errors early on, making your code more robust and maintainable.

## Why Use Room?

Room offers several benefits:

1. **Simplicity**: Room simplifies database operations by providing a high-level abstraction layer.
2. **Compile-time Verification**: Room provides compile-time checks for SQL queries, reducing the chance of runtime errors.
3. **Type Safety**: Room uses Kotlin's type-safe features to ensure that SQL queries are syntactically correct and avoid runtime errors.
4. **Integration with LiveData and Coroutines**: Room seamlessly integrates with LiveData and Coroutines, making it easy to handle asynchronous database operations.
5. **ORM (Object Relational Mapping)**: Room provides built-in support for mapping database tables to Kotlin objects, reducing boilerplate code.

## Getting Started

To use Room in your Kotlin project, follow these steps:

1. **Add Dependencies**: Add the Room dependencies to your `build.gradle` file.

```gradle
dependencies {
    def room_version = "2.4.0-alpha03"

    implementation "androidx.room:room-runtime:$room_version"
    kapt "androidx.room:room-compiler:$room_version"
}
```

2. **Define Entity Classes**: An entity represents a table in your database. Define Kotlin data classes annotated with `@Entity` to represent your database tables.

```kotlin
@Entity
data class User(
    @PrimaryKey val id: Int,
    val name: String,
    val age: Int
)
```

3. **Create Database**: Create an abstract class that extends `RoomDatabase` and define abstract methods to access your DAOs (Data Access Objects).

```kotlin
@Database(entities = [User::class], version = 1)
abstract class MyAppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
}
```

4. **Define DAOs**: DAOs are responsible for defining methods to interact with your database. Annotate your DAO interface with `@Dao`.

```kotlin
@Dao
interface UserDao {
    @Query("SELECT * FROM User")
    fun getAll(): List<User>

    @Insert
    fun insert(user: User)

    @Delete
    fun delete(user: User)
}
```

5. **Initialize Database**: Initialize your database instance using `Room.databaseBuilder()`.

```kotlin
val db = Room.databaseBuilder(
    applicationContext,
    MyAppDatabase::class.java, "my-database-name"
).build()
```

6. **Perform Database Operations**: Now you can perform database operations using the DAO methods.

```kotlin
val user = User(1, "John", 30)
db.userDao().insert(user)
val users = db.userDao().getAll()
```

## Conclusion

Congratulations! You've learned the basics of Room Database in Kotlin. With Room, you can easily manage your app's data persistence layer in a robust and efficient manner. Happy coding! 🚀
