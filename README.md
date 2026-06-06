Other Resources:

* <a href="https://www.flaticon.com/free-icons/female" title="female icons">Female icons created by popcornarts - Flaticon</a>
* [Alibaba IconFont](https://www.iconfont.cn/)
* [Coolapk @沉默_9520](http://www.coolapk.com/u/25956307) — author of this app's icon

# Build

### Android Studio:
Create a new file named `local.properties` in the project root directory and add the following:
```
KEY_PATH=E\:\\Android\\key\\sign.jks (signing file)
KEY_PASSWORD= password
ALIAS_NAME= alias
ALIAS_PASSWORD= alias password
```



### GitHub Actions:
> For full details, see https://www.cnblogs.com/jing332/p/17452492.html

Use Git Bash to Base64-encode the signing file without line breaks: `openssl base64 < key.jks | tr -d '\r\n' | tee key.jks.base64.txt`

Add the following four repository secrets:
> Go to: https://github.com/your-username/tts-server-android/settings/secrets/actions
* `ALIAS_NAME` — the alias
* `ALIAS_PASSWORD` — the alias password
* `KEY_PASSWORD` — the password
* `KEY_STORE` — the contents of the `sign.jks.base64.txt` file generated earlier
