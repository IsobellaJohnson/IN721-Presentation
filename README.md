# **Android Notifications**

# Overview 
**Notifications** are a message your Android device displays outside the application's UI. The purpose of notifications are to provide the user with information about your app including reminders and communication from other users. **Notifications** appear in different places on the device in different formats, including in the status bar, notification drawer and on the apps icon.

# Set up notifications

Go to **build.gradle (Module)** & make sure you have the **Notification** dependency:

```
    implementation "androidx.core:core:$core_version"
```

also, make sure you set the core version as such:
```
    val core_version = "1.6.0"
```

