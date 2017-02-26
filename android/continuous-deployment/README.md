

# Google Play

*  There are three "channels": alpha, beta, and production.
-  


> **Tip:**
>
> Any changes to your listing in the Google Play Console can take hours to process.  Until it is, you may not be able to make other changes to the listing.

# Managing Android Tooling for CI

* https://github.com/makinacorpus/android-archetypes/wiki/Getting-started%3A-Building-Android-apps-with-Jenkins-CI
* the `android` command-line tool obtains metadata from a set of XML files.

    ```bash
    android list sdk --extended
    Refresh Sources:
      Fetching https://dl.google.com/android/repository/addons_list-2.xml
      Validate XML
      Parse XML
      Fetched Add-ons List successfully
      Refresh Sources
      Fetching URL: https://dl.google.com/android/repository/repository-11.xml
      Validate XML: https://dl.google.com/android/repository/repository-11.xml
      Parse XML:    https://dl.google.com/android/repository/repository-11.xml
      ...
    Packages available for installation or update: 24
    ----------
    id: 1 or "platform-tools"
         Type: PlatformTool
         Desc: Android SDK Platform-tools, revision 24.0.1
    ----------
    id: 2 or "build-tools-24.0.0"
         Type: BuildTool
         Desc: Android SDK Build-tools, revision 24
    ----------
    id: 3 or "android-19"
         Type: Platform
         Desc: Android SDK Platform 19
               Revision 4
    ...
    ```
* Install a library from the command-line (e.g. during a CI script):

    ```bash
    android update sdk --no-ui --all --filter <some-id-string-from-above>
    ```