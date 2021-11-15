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
### fragment_notification.xml

Create a **fragment_notification** in the **layout** directory. This will be responsible for the layout of your notifications page. We will create a button which the user clicks to generate a notification.

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
 
    <Button
        android:id="@+id/btn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Send Notification" />
 
</RelativeLayout>
```

We then want to create another activity, named **after_notification.xml** this will open up in our app that is the user will be redirected to this page. Below is the code for the **after_notification.xml** file.

```

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".afterNotification">
 
    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Welcome To GeeksforGeeks"
        android:textSize="15sp"
        android:textStyle="bold" />
 
</RelativeLayout>
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
        
**getSystemService** is a class to notify the user of events that happen. This is how you tell the user that something has happened in the background. We then have to access the button and create an onClickListener for it.

```
        val btn = findViewById<Button>(R.id.btn)
        btn.setOnClickListener {

            val intent = Intent(this, afterNotification::class.java)
            val pendingIntent = PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT)
            val contentView = RemoteViews(packageName, R.layout.activity_after_notification

```
**pendingIntent** is an intent for future use. In this instance, after the notification is clicked the intent will come into play. *FLAG_UPDATE_CURRENT* specifies that if a previous **PendingIntent** already exists, then the current one will update it with the latest intent
```
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
                notificationChannel = NotificationChannel(channelId, description, NotificationManager.IMPORTANCE_HIGH)
                notificationChannel.enableLights(true)
                notificationChannel.lightColor = Color.GREEN
                notificationChannel.enableVibration(false)
                notificationManager.createNotificationChannel(notificationChannel)
 
                builder = Notification.Builder(this, channelId)
                        .setContent(contentView)
                        .setSmallIcon(R.drawable.ic_launcher_background)
                        .setLargeIcon(BitmapFactory.decodeResource(this.resources, R.drawable.ic_launcher_background))
                        .setContentIntent(pendingIntent)
            } else {
 
                builder = Notification.Builder(this)
                        .setContent(contentView)
                        .setSmallIcon(R.drawable.ic_launcher_background)
                        .setLargeIcon(BitmapFactory.decodeResource(this.resources, R.drawable.ic_launcher_background))
                        .setContentIntent(pendingIntent)
            }
            notificationManager.notify(1234, builder.build())
        }
    }
}
```

With this, we have now successfully created a **Notification** for our application. Note that the parameters listed in the above code are required and the absence of any single parameter could result in crashing or not starting the application. The content title, content text, small icon are customizable parameters but are mandatory also. One can change their values according to the requirement.

## References
Notifications in Android with Example. (2021, January 01). Retrieved from https://www.geeksforgeeks.org/notifications-in-kotlin/?ref=lbp

Otago-Polytechnic-Bit-Courses. (n.d.). IN721-mobile-application-development/07-view-model.md at master · otago-polytechnic-bit-courses/IN721-mobile-application-development. Retrieved November 15, 2021, from https://github.com/otago-polytechnic-bit-courses/IN721-mobile-application-development/blob/master/lecture-notes/07-view-model.md


       
