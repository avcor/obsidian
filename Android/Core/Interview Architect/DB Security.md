## What are you protecting against 
- Rooted phone 
- App reverse engineering 
## Options 
### Encrypt whole database 
- Use `SQLCipher`
- Even copy is useless without key 
- Transparent to room 
- Store key in Android Keystore System
	- Generate key in key store 
	- Use it to encrypt DB 
	- Store passphrase in Shared Preferences 
	- Decrypt at runtime 
#### Trade Offs
- Performance overhead encrypt and decrypt happens for every read/write   
- Impact on large data sets 
- Indexing is less efficient than plain `SQLite`
### Column level encryption 
#### Use 
- You need searchable fields 
- Only sensitive data needs protection 
- Use `@TypeConverter`
#### Trade offs
- Easy to mess up require manual transformation
- Cannot search encrypted fields easily 
- Partial Exposure 
## Overall Trade offs
Data is decrypted in RAM when used, rooted device has some risk