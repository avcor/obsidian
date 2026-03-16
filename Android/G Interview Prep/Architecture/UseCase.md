- Use Case is a class that represents a single specific business task. It sits between [[ViewModel]] and [[Repository]].
- It act as an Interceptor. 
- Encapsulate business rule. 
- Coordinate multiple repositories.

UI -> ViewModel -> UseCase -> Repository 
## Characteristics 
- Should be pure or near pure 
- Should be tested without UI 
- Should express behavior not mechanics 
## Why use them 
- **Single Responsibility** - ViewModel does not become 1000 line object. God Object 
- **Reusability** - It can be used in multiple ViewModel 
- **Testing** - You can test business logic in pure Kotlin without needing Android-specific dependencies 
## When not to use 
- **The pass through problem** -  If UseCase just call repository and thus nothing. Just let the ViewModel call the repository. 
- **Logic that belongs in domain model** - If logic is purely about data e.g. `user.getFullName()`, put that inside `User` data class.  Use case are for orchestrating actions.
