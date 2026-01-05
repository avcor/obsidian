similar to [[remember]] uses **Saved State Mechanism ([[Save Instance#`onSavedInstanceState(outState Bundle)`]])** to persist state across process death 

- Saves value into [[SavedStateRegistry]]
- Uses bundle under the hood 
- Restore values after 
	- [[Configuration & Process death#Process death]]
	- [[Configuration & Process death#Configuration Changes]]

## why exist 
Compose does not automatically saves like view used to. 
## Limitation
- Only works for primitive type 
- Limited to bundle size. Will silently fail if bundle is too large. 
- 