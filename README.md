

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

# Attribution

**Original source:**

This project is adapted from the source by [jing332/tts-server-android](https://github.com/jing332/tts-server-android).

**Icons:**

* Icons from <a href="https://www.flaticon.com/free-icons/female" title="female icons">Flaticon</a>
* Icons from [Alibaba IconFont](https://www.iconfont.cn/)
* Icons from [Coolapk @沉默_9520](http://www.coolapk.com/u/25956307) — author of this app's icon

# MIT License

Copyright 2026 The DeadBranches Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE
