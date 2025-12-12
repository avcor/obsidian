## Stable 
- **Promise** - It is a contract that tell the compose that the properties of the object or the object will not change without compose being notified. 
- A @Stable object might contain the mutable properties as long as they are Compose's observable state types like [[State#`MutableState`| mutable state]] or `SnapShotStateList`
- **Use** - when object have mutable properties internally, but those changes can be observed by Compose 

## Immutability 
- This is a stronger promise. It guarantee that nothing inside the object will ever change after it is created. If any part needs to change then completely new instance needs to be created and passed. 
- Compose then need to check reference and decide to skip or not.
- **Immutable Object cannot contain mutable fields**


## Why data class may not be Stable 
Data class is marked stable if 
- primary constructor property are marked with `val` 
- and type of every single property is also stable type 
### Pitfall
`val items: List<String>` List is not stable type even if it is read only. You as the consumer cannot modify it but still it is underlying content can be modified via another reference. 
**Therefore it is unstable unless marked explicitly**