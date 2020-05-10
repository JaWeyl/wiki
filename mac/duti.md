# Set default application for file types

Run ```brew install duti```

- First you need the *identifier* of the application you want to set as default, e.g. for Visual Code

  ```/usr/libexec/PlistBuddy -c 'Print CFBundleIdentifier' /Applications/Visual\ Studio\ Code.app/Contents/Info.plist```
- Next you need the *Uniform Type Identifiers [UTI](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/understanding_utis/understand_utis_conc/understand_utis_conc.html)* of the entities you want to open with the aforementioned application, e.g.:

  ```mdls output.tif | grep "kMDItemContentType"``` returns ```public.tiff```
- Now set the default application for this UTI

  ```duti -s com.microsoft.VSCode public.plain-text all```