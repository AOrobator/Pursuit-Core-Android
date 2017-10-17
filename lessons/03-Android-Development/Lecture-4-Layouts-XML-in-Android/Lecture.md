## Title: Android Layouts
Tags: android, xml, layouts, widgets, toasts

--

## Objectives

- Learn how activity layouts are built in XML.
- Practice positioning child views in LinearLayout.
- Practice configuring XML attributes for common view widgets.
- Learn how to make a Toast.

--

## XML Layouts

A **layout** defines the visual structure for a user interface. There are two ways to create Android layouts:

1. As an XML resource file. 

2. Programmatically by instantiating layout elements at runtime. 

But use XML to:
- Separate logic from presentation 
- Easily visualize the structure of your UI.

---

## Referencing a Layout in an Activity

```java
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main_layout);
    // R: resource directory
    // layout: layout sub-directory
    // main_layout: file named main_layout.xml
}
```

---

## Layouts: Views

The basic building block for user interface is a **View** object which is created from the View class and occupies a rectangular area on the screen and is responsible for drawing and event handling.

View is the base class for widgets, which are used to create interactive UI components like buttons, text fields, etc.

The **ViewGroup** is a subclass of **View** and provides invisible container that hold other Views or other ViewGroups and define their layout properties.

---

## Layouts: Views

In the layout code below, `LinearLayout` is a ViewGroup while `TextView` and `Button` are Views

ViewGroups can contain other ViewGroups or Views as children while Views cannot have any children.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:orientation="vertical" >
    <TextView android:id="@+id/text"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="Hello, I am a TextView" />
    <Button android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Hello, I am a Button" />
</LinearLayout>
```

---

## Common Layout Types

- **Linear Layout** 
LinearLayout is a view group that aligns all children in a single direction, vertically or horizontally.

- **Relative Layout** 
RelativeLayout is a view group that displays child views in relative positions.

- **Table Layout** 
TableLayout is a view that groups views into rows and columns.

- **Absolute Layout** 
AbsoluteLayout enables you to specify the exact location of its children.

- **Frame Layout** 
The FrameLayout is a placeholder on screen that you can use to display a single view.

- **List View**
ListView is a view group that displays a list of scrollable items.

- **Grid View**
GridView is a ViewGroup that displays items in a two-dimensional, scrollable grid.

---

## Intentionally left blank

---

## Common Layout Types

How many do you remember?


What are some use cases you can think of them?

---

## Linear Layout

By far the easiest to understand. Just stack all my children one after the other.

Create a linear layout with a TextView, and a Button

---

## Common Layout Attributes

**android:id** 
This is the ID which uniquely identifies the view.

**android:layout_width** 
This is the width of the layout.

**android:layout_height** 
This is the height of the layout

**android:layout_marginTop**
This is the extra space on the top side of the layout.

**android:layout_marginBottom** 
This is the extra space on the bottom side of the layout.

You can guess **android:layout_marginLeft** and **android:layout_marginRight**

**android:layout_gravity** 
This specifies how child Views are positioned.

**android:layout_weight**  
This specifies how much of the extra space in the layout should be allocated to the View.

**android:layout_x**  
This specifies the x-coordinate of the layout.

**android:layout_y** 
This specifies the y-coordinate of the layout.

**android:layout_width** 
This is the width of the layout.

**android:layout_width** 
This is the width of the layout.

**android:paddingLeft**
This is the left padding filled for the layout.

You can guess **android:paddingRight**, **paddingTop** and **paddingBottom**

---

## Tweek and Feel the attributes

Experiment with these attributes in the [Android Layouts app](https://github.com/C4Q/AC-Android-Apps/tree/master/AndroidLayoutsXML)

Mess with the designer and see how the code updates.

---

## Programmatically Update Attributes

Example: To update the `android:text` attribute

```
textView.setText("hello world");
```

Hands on In IntelliJ


--

## Exercises

For each of the following exercises, create a new XML resource file in your `res/layout` directory (e.g. `exercise_one.xml`). You can test each layout by changing the `setContentView(R.layout.exercise_one)` line in your `MainActivity.java` file and running the app.

> **Question 1:**) 

1) Create new XML resource file `exercise_one.xml`. Add a `LinearLayout` as the root element, with orientation set to vertical.

2) Add three `TextViews` as child views to the `LinearLayout`. Give them ids. For all three, set `layout_width` and `layout_height` to `wrap_content` and set the text to `TextView One`, `TextView Two` and `TextView Three` respectively. Set the background color to `#ff0000`, `#ffff00` and `#0000ff` respectively. Run the app and observe the layout.

3) Add 40dp padding to each of the `TextViews`. Run the app and observe the layout.

4) Add 40dp margin to each of the `TextViews`. Run the app and observe the layout.

5) Change the layout gravity on the top `TextView` to top. Change the layout gravity on the middle `TextView` to center. Change the layout gravity on the bottom `TextView` to bottom. Run the app and observe the layout.

6) Remove the layout gravity attributes from the `TextViews`. Change the gravity on the `LinearLayout` to bottom. Run the app and observe the layout.

---

## Exercises

> **Question 2:**

1) Create new XML resource file `exercise_two.xml`. Add a `LinearLayout` as the root element, with orientation set to horizontal.

2) Add three `Buttons` as child views to the `LinearLayout`. Give them ids. For all three, set `layout_width` to 0dp and `layout_height` to `match_parent`. For all three, set the `layout_weight` to 1. Set the text to `Button One`, `Button Two` and `Button Three` respectively. Set the background colors to [different colors of you choice](http://www.w3schools.com/colors/colors_picker.asp). Run the app and observe the layout.

3) In your activity's Java file, use `findViewById()` to get a reference to each of the buttons. Set click listeners on each of the buttons that display a Toast with the button's text.


---

## Summary

* Views are building blocks of Android Layouts

* ViewGroups contain other ViewGroups and Views

* There are common attributes across views and they can be customized

* Views can be modified programmatically


