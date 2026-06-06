Other Resources:

* <a href="https://www.flaticon.com/free-icons/female" title="female icons">Female icons created by popcornarts - Flaticon</a>
* [Alibaba IconFont](https://www.iconfont.cn/)
* [Coolapk @沉默_9520](http://www.coolapk.com/u/25956307) — author of this app's icon

# Build Instructions

### Using Android Studio:
Create a new file named `local.properties` in the project root directory and add the following:
```
KEY_PATH=E\:\\Android\\key\\sign.jks (signing file)
KEY_PASSWORD= password
ALIAS_NAME= alias
ALIAS_PASSWORD= alias password
```



### Using GitHub Actions:
*source: [jing332's blog](https://www.cnblogs.com/jing332/p/17452492.html)*

Android apps must be cryptographically signed with a key, and that key must be kept private. Here's the workaround that allows you to use Github Actions to build an android project automatically. 

Building an Android project with Github Actions requires a signature, and the jks file cannot be saved privately, so you can convert it to base64 format and set security variables 

1. **Turn the key file into text.**
   ```
   openssl base64 < key.jks | tr -d '\r\n' | tee key.jks.base64.txt
   ```
   
   The `openssl base64` command above converts the binary .jks file into a long string of plain text characters. The `tr -d '\r\n'` part strips out any line breaks so it's one continuous blob. Line breaks would corrupt it when GitHub reads it back.
   
2. **Store the secrets where GitHub hides them.**
   
   GitHub [has a vault called "repository secrets"](https://github.com/your-username/tts-server-android/settings/secrets/actions) containing values that the build process can use but that never show up in logs and can't be read back by people browsing the repo. Paste four things in there:

   | secret name | description |
   |---|---|
   | ALIAS_NAME | *the alias* |
   | ALIAS_PASSWORD | *the alias password* |
   | KEY_PASSWORD | *the password* |
   | KEY_STORE | *the contents of the `sign.jks.base64.txt` file generated earlier* |
