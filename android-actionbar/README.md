# Action Bar for Android

![ActionBar for Android](http://markupartist.com/images/actionbar.png "ActionBar for Android")

This projects aims to provide a reusable action bar component. The action bar pattern is well documented at [Android Patterns](http://www.androidpatterns.com/uap_pattern/action-bar).

The action bar component is an [Library Project](http://developer.android.com/guide/developing/eclipse-adt.html#libraryProject). This means that there's no need to copy-paste resources into your own project, simply add the action bar component as a reference to any project.

Need icons to your action bar? Olof Brickarp has ported some of [Androids native icons to vector format](http://www.yay.se/2011/02/native-android-icons-in-vector-format/).

## Usage

### In your layout

    <com.markupartist.android.widget.ActionBar
	    android:id="@+id/actionbar"
	    app:title="@string/some_title"
	    style="@style/ActionBar"
        />

The use of `app:title` is optional, it's also possible to assign the title using the `setTitle` programmatically on the `ActionBar`. To be able to use the more convenient `app:title` the application namespace must be included in the same manner as the android namespace is. Please refer to the layout other.xml in the example project for a full example. Again, note that it's the application namespace and *not* the actionbar namespace that must be referred like `xmlns:app="http://schemas.android.com/apk/res/you.application.package.here"`.

### In your activity

    ActionBar actionBar = (ActionBar) findViewById(R.id.actionbar);
    // You can also assign the title programmatically by passing a
    // CharSequence or resource id.
    //actionBar.setTitle(R.string.some_title);
    actionBar.setHomeAction(new IntentAction(this, HomeActivity.createIntent(this), R.drawable.ic_title_home_default));
    actionBar.addAction(new IntentAction(this, createShareIntent(), R.drawable.ic_title_share_default));
    actionBar.addAction(new ToastAction());

### Custom actions

ActionBar comes with a convenient IntentAction that makes it easy to create action out of Intents. To create custom actions simply implement the Action interface and build your own like the Toast example below.

    private class ToastAction implements Action {

        @Override
        public int getDrawable() {
            return R.drawable.ic_title_export_default;
        }

        @Override
        public void performAction(View view) {
            Toast.makeText(OtherActivity.this,
                    "Example action", Toast.LENGTH_SHORT).show();
        }

    }

### Handle on click on the title

To handle on clicks on the title pass a `android.view.View.OnClickListener` to the method `setOnTitleClickListener` on the action bar. The `View` that is passed in `onClick` is the `TextView` that the title is assigned to.

    actionBar.setOnTitleClickListener(new OnClickListener() {
        public void onClick(View v) {
            // Your code here
        }
    });

### Customization

Since the ActionBar is an Libary Project all resources will be merged to the project that referencing the ActionBar. The values in the main project will always be used before the default values of the ActionBar.

If you don't like the default colors that is defined in the [colors.xml](https://github.com/johannilsson/android-actionbar/blob/master/actionbar/res/values/colors.xml) file simply override the default values in the main projects colors.xml file. To create a blue ActionBar create a colors.xml file that looks something like the one below. Note that we don't override the values for actionbar_background_item_pressed_start and ctionbar_background_item_pressed_end since we decided to stick with the default values.

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <color name="actionbar_separator">#3A5FCD</color>
        <color name="actionbar_background_start">#3A5FCD</color>
        <color name="actionbar_background_end">#27408B</color>
    </resources> 

The same can be done with the drawables, layouts and everything else that is located in the ActionBar project.

## Contributions

* ohhorob, https://github.com/ohhorob
* denravonska, https://github.com/denravonska
* rpdillon, https://github.com/rpdillon
* RickardPettersson, https://github.com/RickardPettersson

### Want to contribute?

GitHub has some great articles on [how to get started with Git and GitHub](http://help.github.com/) and how to [fork a project](http://help.github.com/forking/).

Contributers are recommended to fork the app on GitHub (but don't have too). Create a feature branch, push the branch to git hub, press Pull Request and write a simple explanation.

One fix per commit. If say a a commit closes the open issue 12. Just add `closes #12` in your commit message to close that issue automagically.

All code that is contributed must be compliant with [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0.html).

## Code Style Guidelines

Contributers are recommended to follow the Android [Code Style Guidelines](http://source.android.com/source/code-style.html) with exception for line length that I try to hold to 80 columns where possible.

In short that is;

* Indentation: 4 spaces, no tabs.
* Line length: 80 columns
* Field names: Non-public, non-static fields start with m.
* Braces: Opening braces don't go on their own line.
* Acronyms are words: Treat acronyms as words in names, yielding XmlHttpRequest, getUrl(), etc.
* Consistency: Look at what's around you!

Have fun and remember we do this in our spare time so don't be to serious :)

## License
Copyright (c) 2010 [Johan Nilsson](http://markupartist.com)

Licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)

