/https://github.com/patrickfav/uber-apk-signer/releases/tag/v1.3.0 to sign apks.

``adb shell`` to initialize the shell, once Emulator is up and running, with app Hello inside.

``pm list packages | grep hello`` to find the class we're looking for.
Output: ``package:pt.ua.deti.hello

``pm path <path>``
Output: `` package:/data/app/~~EI0DDn45DGJT6a0bGxobLw==/pt.ua.deti.hello-xdcgBHDBEJP8SDrvzEQcCg==/base.apk
``
**needs to be su in adb shell beyond this point**


