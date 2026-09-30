``` kotlin
@Entity(  
    foreignKeys = [  
        ForeignKey(  
            entity = User::class,  
            parentColumns = ["userId"],  
            childColumns = ["userOwnerId"]  
        )  
    ]  
)  
data class Marks(  
    @PrimaryKey(autoGenerate = true)  
    val id: Int,  
    val marks: Int,  
    val subject: String,  
    val userOwnerId: Long,  
)

data class UserAndMarks(  
    @Embedded val user: User,  
    @Relation(  
        parentColumn = "userId",  
        entityColumn = "userOwnerId"  
    ) val marks: List<Marks>  
)

@Transaction  
@Query("SELECt * FROM User")  
suspend fun getUserWithMarks(): List<UserAndMarks>
```

