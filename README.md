Android DirectoryChooser
========================

A simple directory chooser you can integrate into your Android app.

This version of the library depends on
[ActionBarSherlock](http://actionbarsherlock.com/) for compatibility with
Android down to API version 7. The [master branch][2], however, has no external
dependency, but requires V11+ to work.

You can download the sample app from the Play Store:

[![Download from Google Play](http://developer.android.com/images/brand/en_generic_rgb_wo_45.png)][3]

Based on the DirectoryChooser from the excellent
[AntennaPod App](https://github.com/danieloeh/AntennaPod) by danieloeh.

![DirectoryChooser Sample Screenshot][1]

Roadmap
-------

 * 1.0: Publish to Maven Central
 * 2.0: Asynchronous directory chooser

Usage
-----

For a full example see the `sample` app in the
[repository](https://github.com/passy/Android-DirectoryChooser/tree/master/sample).

### Dependencies

Check out this repository and add it as a library project.

    git checkout https://github.com/passy/Android-DirectoryChooser.git

Import the project into your favorite IDE and add
`android.library.reference.1=/path/to/Android-DirectoryChooser/library` to your
`project.properties`.

#### Maven

The library is also awailable on Sonatype:

*Release*

    <dependency>
      <groupId>net.rdrei.android.dirchooser</groupId>
      <artifactId>library</artifactId>
      <version>0.1</version>
      <type>apklib</type>
    </dependency>

*Snapshot*

    <dependency>
      <groupId>net.rdrei.android.dirchooser</groupId>
      <artifactId>library</artifactId>
      <version>1.0-SNAPSHOT</version>
      <type>apklib</type>
    </dependency>

(not yet released)

### Manifest

You need to declare the `DirectoryChooserActivity` and request the
`android.permission.WRITE_EXTERNAL_STORAGE` permission.

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
...
<application>
    <activity android:name="net.rdrei.android.dirchooser.DirectoryChooserActivity" />
</application>
```

### Activity

To choose a directory, start the activity from your app logic:

```java
final Intent chooserIntent = new Intent(this, DirectoryChooserActivity.class);

// Optional: Allow users to create a new directory with a fixed name.
chooserIntent.putExtra(DirectoryChooserActivity.EXTRA_NEW_DIR_NAME,
                       "DirChooserSample");

// REQUEST_DIRECTORY is a constant integer to identify the request, e.g. 0
startActivityForResult(chooserIntent, REQUEST_DIRECTORY);
```

Handle the result in your `onActivityResult` method:

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    if (requestCode == REQUEST_DIRECTORY) {
        if (resultCode == DirectoryChooserActivity.RESULT_CODE_DIR_SELECTED) {
            handleDirectoryChoice(data
                .getStringExtra(DirectoryChooserActivity.RESULT_SELECTED_DIR));
        } else {
            // Nothing selected
        }
    }
}
```

License
-------

```text
Copyright 2013 Pascal Hartig

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

Thanks
------

Sample App icon by [Frank Souza](http://franksouza183.deviantart.com/).

 [1]: https://raw.github.com/passy/Android-DirectoryChooser/master/media/screenshot_phone.png
 [2]: https://github.com/passy/Android-DirectoryChooser/tree/master
 [3]: https://play.google.com/store/apps/details?id=net.rdrei.android.dirchooser.sample
