# 
First, you need to declare the developer information on the device

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

Change.txt
```text
- The file contains the changes used during the Gradle or CI build process; currently supports Vietnamese and English.
- The file does not distinguish between CRLF and LF and will be converted to LF.
- The file must contain 3 \n\n\n to separate the two languages, starting with Vietnamese and then /n/n/n English for the system to process. In addition, the Vietnamese information must be different from the English content...
 + Bundle build process
  > pwsh ./tools/bundle.ps1
  > app.gradle.kts will build the bundle and process changelog.txt (English) and changelogvi.txt (Vietnamese) which contain all changes by appending them, together with release.xml containing [...]
  > During this process, change.json is also created in assets (./app/main/assets) to store the current change information.
 + APK build process
  > pwsh ./tools/build.ps1
  > Similar to the bundle, the apk will additionally process the manifest file, write change information into the file to serve as update signaling and build repo.json
  > Sync files from the CI server to the Public server (vnapps.com/apps)
- Note: if Change.txt is emptied or left unchanged, change log processing will skip the current build version.
The app needs to process assets and the manifest to retrieve this information (before or after build) to display if necessary.
To release a bundle, it is recommended to copy the available content from release.xml to help users better understand the app changes.
```

push.ps1
```text
Most commits do not need or do not want to publish changes; push.ps1 is used for quick code backup or to quickly push to CI.
Change.txt provides major changes; changes made during commits may not be necessary.
Use /c "start pwsh ./push.ps1" for a physical key (F12) or for the IDE toolbar.
```
