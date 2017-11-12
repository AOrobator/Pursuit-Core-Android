# Android Shared Preferences and Intents, Revisited

# Objectives

- Differences between RAM and Persistent Storage
- Utilize SharedPreferences and Intent Extras to store, recall, and exchange information

# Resources

- [Shared Preferences](https://developer.android.com/reference/android/content/SharedPreferences.html)
- [Android Storage Options](https://developer.android.com/guide/topics/data/data-storage.html#pref)
- [Shared Preferences Tutorial](https://developer.android.com/guide/topics/data/data-storage.html#pref)

# Lecture

Although we can use data structures in our apps, the data we store usually only lasts as long as the app, or activities within the app, are still active. One the activity is destroyed, so is the data. SharedPreferences allow us to save privitive data (and Strings too), well after the app has shut down.

## Shared Preferences

The Android SharedPreferences API allows developers to save key-value pairs of associated data (Maps, anyone?) in unique files that are accessible to activities/applications both throughout their lifecycles, as well as well after the phone has been shut down and restarted. SharedPreferences entries are usually used for storing app specific preferences, like sign-in information, whether a user wants to see instructions every time an app is loaded, etc.

One way to get/create a SharedPreferences file for your app, involves storing a reference to it within your activity:

```java
SharedPreferences sharedPrefs = getApplicationContext().getSharedPreferences("mySharedPrefs", MODE_PRIVATE);
```

We use ```getApplicationContext()``` because we want this data to be accessible to all of the activities that might run within this application's process. Then, we call the method ```getSharedPreferences("mySharedPrefs", MODE_PRIVATE)```, so that we can:
* First, get back a file associated with the String "mySharedPrefs"
* Second, if there is no file associated with that name, create one
* Third, make sure only this application has access to this data, since SharedPreferences are data collections which can potentially be accessed anywhere in the device, when given the right/wrong permissions

With this SharedPreferences object, we can now put key/value pairs, get key/value pairs, or replace key/value pairs of data for this application, whenever we want.

So, let's say we want to create an app that requires logging into it before we can use it. We'll need to create a login activity, to check if a user has registered. If they have, we can sign them in. If they've already registered, and signed in once, they might not want to have to sign in every time they open the app. We can give them the option to let the app "remember" their login information, so that the next time they open it up, they can simply press submit, with the user information already preloaded on the screen.

Here's the login activity's XML:

```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context="nyc.c4q.sharedprefstesting.MainActivity">

    <LinearLayout
        android:layout_weight="1"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_marginStart="60dp"
        android:layout_marginEnd="60dp">

        <TextView
            android:id="@+id/signin_textview"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:text="Please Sign In."/>

        <TextView
            android:id="@+id/username_textview"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Username:"/>

        <EditText
            android:id="@+id/username_edittext"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Enter Email Address"
            android:inputType="textWebEmailAddress"/>

        <TextView
            android:id="@+id/password_textview"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Password:"/>

        <EditText
            android:id="@+id/password_edittext"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Enter Password"
            android:inputType="textWebPassword"/>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:orientation="horizontal">

            <android.support.v7.widget.AppCompatCheckBox
                android:id="@+id/remember_me_checkbox"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Remember me"/>

        </LinearLayout>

        <Button
            android:id="@+id/submit_button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:text="Submit"/>

    </LinearLayout>

    <LinearLayout
        android:layout_weight="1"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:orientation="vertical">

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Not Registered?"
            android:gravity="center"/>

        <Button
            android:id="@+id/register_button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:text="Click to register"/>

    </LinearLayout>

</LinearLayout>
```

And this is what it should look like:

![](login_screen.PNG)

In our MainActivity.java file, we'll store references to our views, and our SharedPreferences file, so that we may interact with them:

```java
package nyc.c4q.sharedprefstesting;

import android.content.Intent;
import android.content.SharedPreferences;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;

public class MainActivity extends AppCompatActivity {

    private static final String SHARED_PREFS_KEY = "sharedPrefsTesting";
    private EditText username;
    private EditText password;
    private CheckBox checkBox;
    private Button submitButton;
    private Button registerButton;
    private SharedPreferences login;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        username = (EditText) findViewById(R.id.username_edittext);
        password = (EditText) findViewById(R.id.password_edittext);
        checkBox = (CheckBox) findViewById(R.id.remember_me_checkbox);
        submitButton = (Button) findViewById(R.id.submit_button);
        registerButton = (Button) findViewById(R.id.register_button);

        login = getApplicationContext().getSharedPreferences(SHARED_PREFS_KEY, MODE_PRIVATE);

        submitButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                
            }
        });

        registerButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
            
            }
        });
    }
}
```

If you'll notice, we have the String ```private static final String SHARED_PREFS_KEY = "sharedPrefsTesting";```, and we stored this String because we will be using it several times throughout our application - you'll see as we create the app further.

We then create/get a SharedPreferences reference, associated with the key "sharedPrefsTesting":

```login = getApplicationContext().getSharedPreferences(SHARED_PREFS_KEY, MODE_PRIVATE);```

We'll want to store the username and password entered into our EditTexts for future use ONLY if the checkbox next to "rememeber me" is ticked, and the "Submit" button has been clicked. We can do that by taking the SharedPreferences reference, and adding it to a ```SharedPreferences.Editor``` reference in the submit button's onClickListener. First, we check whether the checkbox has been ticked (```checkbox.isChecked()```), then we pass the ```SharedPreferences``` reference to the ```Editor```, because like Arrays and Strings, ```SharedPreferences``` are essentially immutable, and must be edited in a unique way:

```java
package nyc.c4q.sharedprefstesting;

import android.content.Intent;
import android.content.SharedPreferences;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;

public class MainActivity extends AppCompatActivity {

    private static final String SHARED_PREFS_KEY = "sharedPrefsTesting";
    private EditText username;
    private EditText password;
    private CheckBox checkBox;
    private Button submitButton;
    private Button registerButton;
    private SharedPreferences login;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        username = (EditText) findViewById(R.id.username_edittext);
        password = (EditText) findViewById(R.id.password_edittext);
        checkBox = (CheckBox) findViewById(R.id.remember_me_checkbox);
        submitButton = (Button) findViewById(R.id.submit_button);
        registerButton = (Button) findViewById(R.id.register_button);

        login = getApplicationContext().getSharedPreferences(SHARED_PREFS_KEY, MODE_PRIVATE);

        submitButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                SharedPreferences.Editor editor = login.edit();
                if (checkBox.isChecked()) {
                    editor.putString("username", username.getText().toString());
                    editor.putString("password", password.getText().toString());
                    editor.putBoolean("isChecked", checkBox.isChecked());
                    editor.commit();
                } else {
                    editor.putBoolean("isChecked", checkBox.isChecked());
                    editor.commit();
                }
            }
        });

        registerButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
            
            }
        });
    }
}
```

To store the values, we use a put method (very much like a Map), corresponding to its data type: ```int```, ```boolean```, ```String```, etc.:

```java
editor.putString("username", username.getText().toString());
editor.putString("password", password.getText().toString());
editor.putBoolean("isChecked", checkBox.isChecked());
```
