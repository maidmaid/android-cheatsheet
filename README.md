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
    
    // Other
    R.string; // strings for translation
    R.style;
}
```
