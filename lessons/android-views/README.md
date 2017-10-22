# Views in Android

## Objectives

- Explore Views
- Define the difference between ViewGroups and Widgets
- Identify View Vierarchies
- Utilize a number of different Views/ViewGroups

## Resources

- [Toasts](https://developer.android.com/guide/topics/ui/notifiers/toasts.html)
- [Layouts](https://developer.android.com/guide/topics/ui/declaring-layout.html)
- [Linear Layout](https://developer.android.com/guide/topics/ui/layout/linear.html)
- [Relative Layout](https://developer.android.com/guide/topics/ui/layout/relative.html)
- [Android API: TextView](https://developer.android.com/reference/android/widget/TextView.html)
- [Android API: EditText](https://developer.android.com/reference/android/widget/EditText.html)
- [Android API: Button](https://developer.android.com/reference/android/widget/Button.html)

# Lecture

According to the Android Docs:

- "All user interface elements in an Android app are built using ```View``` and ```ViewGroup``` objects. A ```View``` is an object that draws something on the screen that the user can interact with. A ```ViewGroup``` is an object that holds other ```View``` (and ```ViewGroup```) objects in order to define the layout of the interface."

- "Android provides a collection of both ```View``` and ```ViewGroup``` subclasses that offer you common input controls (such as buttons and text fields) and various layout models (such as a linear or relative layout)."

[Android Source Documentation](https://developer.android.com/guide/topics/ui/overview.html)

Essentially, ```View``` objects are anything which can be either seen or touched by the user. ```ViewGroups``` are also views, but their jobs are much more tailored to organizing view objects on the screen.

## Defining Views Programatically

There are multiple ways to place views on a screen. One way is by using pure java code in your activities:

```java
package nyc.c4q.surewhynot;

import android.graphics.drawable.GradientDrawable;
import android.support.v4.view.GravityCompat;
import android.support.v7.app.ActionBar;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.Gravity;
import android.view.View;
import android.widget.LinearLayout;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        LinearLayout.LayoutParams param = new LinearLayout.LayoutParams(
                ActionBar.LayoutParams.MATCH_PARENT,
                ActionBar.LayoutParams.MATCH_PARENT,
                1.0f);

        LinearLayout ll = new LinearLayout(getApplicationContext());
        ll.setLayoutParams(param);
        ll.setOrientation(LinearLayout.VERTICAL);
        setContentView(ll);

        TextView tv = new TextView(getApplicationContext());
        tv.setLayoutParams(param);
        tv.setText("Hello");
        tv.setGravity(Gravity.CENTER);

        TextView tv2 = new TextView(getApplicationContext());
        tv2.setLayoutParams(param);
        tv2.setText("Goodbye");
        tv2.setGravity(Gravity.CENTER);

        ll.addView(tv);
        ll.addView(tv2);
    }
}
```

Old-school Java GUI (Grafical User Interface) Frameworks developers like AWT and Swing use (use? from the 90's, but today? Still?), pure java code to instantiate and layout view objects on the screen. 

However, although this way is possible, it might not be ideal. There is another way to place these object on the screen in Android - with XML (eXtensible Markup Language).
