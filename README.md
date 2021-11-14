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

### NotificationFragment

Create a **Notification** folder in the **UI** directory, then create **NotificationFragment** inside the **Notification** folder.

```
class NotifivationFragment : AppCompatActivity() {
 
    // declaring variables
    lateinit var notificationManager: NotificationManager
    lateinit var notificationChannel: NotificationChannel
    lateinit var builder: Notification.Builder
    private val channelId = "i.apps.notifications"
    private val description = "Test notification"
 
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
 
        notificationManager = getSystemService(Context.NOTIFICATION_SERVICE) as NotificationManager
```
        
**NotificationManager** is a class to notify the user of events that happen. This is how you tell the user that something has happened in the background.
        
       
