### 1 - Installing on phone
Using an emulator with Play Store support, find CTT app and install it.

### 2 - Extracting apk
using a shell
`adb shell
``pm list packages | grep ctt`` to find the class we're looking for.
``pm path <class>``
then
`adb pull <path>`

