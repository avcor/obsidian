- The purpose of key store is store to protect encryption key.
- Key is stored inside hardware such as TEE (Trusted Execution Environment). These component are isolated form android itself. 

```text
	        Store

        "abc10"
            │
            ▼
   Android Keystore
   Encrypt using AES Key
            │
            ▼
      8FC2A97115
            │
            ▼
 SharedPreferences


-------------------------------

            Read

 SharedPreferences
      8FC2A97115
            │
            ▼
 Android Keystore
 Decrypt using AES Key
            │
            ▼
         "abc10"
```