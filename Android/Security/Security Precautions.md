## 1. Enable Proguard / R8
- R8 is being mostly used currently 
- It Obfuscate the code which make reverse engineering harder. 
- 
## 2. API Keys 
- Try not to ship application with API keys in code because they can still be accessed with obfuscation, because it still be visible as plain string text. 
- Store sensitive data in C/C++ files using NDK. Later on You can call it from code.  
	- Key in no longer available in [[Java Byte Code]] 
	- But Key still exist in memory and call be exposed using memory dumping or intercepting Http request.
- NDK is not similar to [[Java Byte Code]] because C++ is compiled directly to Native ARM/x86 machine code (`.so` libraries). 
*Note - Instead of storing string store it as Bytes* 

## 3. Firebase Security Rules 
- When you build the app, firebase SDK put the url & api key in java code as plain text.
- This is dangerous as api key is exposed and can used to destroy db or have attack on service. 
- For this to prevent we need to have to security rules for db 
- Restrict api key access to app's package name and SHA-1 certificate. 
### How does SHA validated 
- Google SDK interacts with Play Service internally through IPC. 
- Then Play service check through Google Server, and communication protocol is proprietary.
## 4. HTTPS 
- Use only HTTPS connections. 
- Disable HTTP connection in `network-security.xml` by making `clear-text-communication` as false
## 5. Sensitive info on Share Preference 
- Use [[Android Key Store]] to store any sensitive data
- Encrypt before storing 
*Note - these things are not 100% protected anyone with root access or frida can read value from memory after decryption.*
### How to prevent (Banking apps do) 
- Android Key Store for encryption keys. 
- Encrypted values in local storage
- Short lived access token 
- Refresh tokens with server side control 
- Developer Mode or Debug mode detection 
- Play Integrity 
- Automatic logout when integrity check fails 
- Avoid storing secrets longer than necessary 
- SSL Pining

## 6. Logcat 
- Disable logs on release builds 

## 7. Use Internal Storage 
- Use internal storage for files which is sandboxed per app. They are stored by using `MODE_PRIVATE`. 
- On Uninstall files are also deleted. 
- You can encrypt the data before storing. 
## 8. Do not use Broadcast 
- Do not use broadcast component to send sensitive information, because other apps can register it and listen to it. 
- Use `LocalBroadcastManager`
## 9. Web View 
- They are vulnerable to XSS attacks. 
- Do not enable Javascript Interface unless webpage is trusted. 
## 10. Protect Service and Content Providers 
- For service use exported flag false in manifest file 
- Same for content providers 
## 11. Payments 
- Avoids payments on rooted device 