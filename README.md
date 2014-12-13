Android Cheatsheet
==================

Add action to ``Button``
---------------------------

```xml
<Button android:onClick="sendMessage" />
```
```java
public void sendMessage(View view) {
    //...
}
```

Start an ``Activity``
-----------------

```java
public class MyActivity1 extends Activity {
    //...
    public void startActivity2(View view) {
        Intent intent = new Intent(this, MyActivity2.class);
        intent.putExtra("key", "value");
        startActivity(intent);
    }
    //...
}
```
```java
public class MyActivity2 extends Activity {
    //...
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        Intent intent = getIntent();
        String value = intent.getStringExtra("key");
        //...
    }
    //...
}
```

### Activity lifecycle

![activity lifecycle](https://developer.android.com/images/training/basics/basic-lifecycle-create.png)

Class ``R``
-----------

```java
public void example() {
    
    // R.id;
    EditText edit = (EditText) findViewById(R.id.editText);
    
    // R.layout;
    setContentView(R.layout.activity_displaymessage);
    
    // R.menu;
    MenuInflater inflater = getMenuInflater();
    inflater.inflate(R.menu.main_activity_actions, menu);
    
    // R.string (translation)
    String hello = getResources().getString(R.string.hello_world)
    textView.setText(R.string.hello_world);
    
    // R.style;
}
```

Theme
-----

### Generic theme

```xml
<!-- AndroidManifest.xml -->
<application android:theme="@android:style/Theme.Holo" ... />
```

### Custom theme:
```xml
<!-- AndroidManifest.xml -->
<application android:theme="@style/AppTheme" ... />
```
```xml
<!-- res/values/styles.xml -->
<resources>
    <style name="AppTheme" parent="@android:style/Theme.Holo">
        <item name="android:windowActionBarOverlay">true</item>
    </style>
</resources>
```

Translation
-----------

Default traduction:
```xml
<!-- res/values/styles.xml -->
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">My Application</string>
</resources>
```

FR traduction:
```xml
<!-- res/values-fr/styles.xml -->
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">Mon application/string>
</resources>
```
