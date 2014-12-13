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

Database
--------

### Contract

```java
public class DbContract {
    public static final int DATABASE_VERSION = 1;
    public static final String DATABASE_NAME = "database.sqlite";
    private static final String TEXT_TYPE = " TEXT";
    private static final String COMMA_SEP = ",";
    
    public static abstract class Person implements BaseColumns {
        public static final String TABLE_NAME = "person";
        public static final String COLUMN_NAME_FIRSTNAME = "firstname";
        public static final String SQL_CREATE_TABLE =
            "CREATE TABLE " + TABLE_NAME + " (" +
                _ID + " INTEGER PRIMARY KEY, " +
                    COLUMN_NAME_FIRSTNAME + TEXT_TYPE +
            ")";
        public static final String SQL_DELETE_TABLE = "DROP TABLE IF EXISTS " + TABLE_NAME;
    }
}
```

### Helper

```java
public class DbHelper extends SQLiteOpenHelper {
    public DbHelper(Context context) {
        super(context, DbContract.DATABASE_NAME, null, DbContract.DATABASE_VERSION);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL(DbContract.Person.SQL_CREATE_TABLE);
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL(DbContract.Person.SQL_DELETE_TABLE);
        onCreate(db);
    }
}
```

### Util Db class

```java
public class Db {
    public static SQLiteDatabase db;

    static void initialize(Context context) {
        DbHelper dbHelper = new DbHelper(context);
        db = dbHelper.getWritableDatabase();
    }

    static long insertPerson(String firstname) {
        ContentValues values = new ContentValues();
        values.put(DbContract.Person.COLUMN_NAME_FIRSTNAME, firstname);

        long id = db.insert(DbContract.Person.TABLE_NAME, null, values);
        return id;
    }
}
```

### Use in Activity !

```java
public class MainActivity extends Activity {
    //...
    protected void onCreate(Bundle savedInstanceState) {
        //...
        Db.initialize(getApplicationContext());
    }
    //...
    public void saveTheWorld(View view) {
        Db.insertPerson("Dany");
        Db.insertPerson("Licya");
    }
}
```
