## Transaction
- Room does not treat multiple table operations as a single unit.  Even if the 2 entities are "logically one" object in app, they are 2 separate rows in 2 separate table in db. 
- Without transaction if one row in table A is inserted and then error occurs before row inserted in table B then it will be half state in db.  
- Under the hood room db executes 2 separate queries one for parent and one for child. 
## One to One 
```kotlin
@Entity
data class User(@PrimaryKey val userId: Long, val name: String)

@Entity
data class LibraryCard(
    @PrimaryKey val cardId: Long, 
    val userOwnerId: Long
)

data class UserAndCard(
    @Embedded val user: User,
    @Relation(
        parentColumn = "userId",
        entityColumn = "userOwnerId"
    )
    val libraryCard: LibraryCard
)

@Transaction 
@Query("SELECT * FROM User")
fun getUsersWithCards(): List<UserAndCard>
```