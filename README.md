Android DirectoryChooser
========================

A simple directory chooser you can integrate into your Android app.

This version of the library has no additional dependencies, but requires Android
v11+ to work. There is, however, [a pre-v11-branch][2] that supports down to v7
using ActionBarSherlock.

You can download the sample app from the Play Store:

[![Download from Google Play](http://developer.android.com/images/brand/en_generic_rgb_wo_45.png)][3]

Based on the DirectoryChooser from the excellent
[AntennaPod App](https://github.com/danieloeh/AntennaPod) by danieloeh.

![DirectoryChooser Sample Screenshot][1]

Roadmap
-------

 * 1.1: Provide AAR packages
 * 2.0: Fragment-based alternative

Usage
-----

For a full example see the `sample` app in the
[repository](https://github.com/passy/Android-DirectoryChooser/tree/master/sample).

### Dependencies

Check out this repository and add it as a library project.

```console
$ git checkout https://github.com/passy/Android-DirectoryChooser.git
```

Import the project into your favorite IDE and add
`android.library.reference.1=/path/to/Android-DirectoryChooser/library` to your
`project.properties`.

#### Maven

Library releases are available on Maven Central, snapshots can be retrieved
from Sonatype:

*Release (SDK 11+)*

**Groovy**

```groovy
compile 'net.rdrei.android.dirchooser:library:1.1@aar'
```

**Maven**

```xml
<dependency>
  <groupId>net.rdrei.android.dirchooser</groupId>
  <artifactId>library</artifactId>
  <version>1.1</version>
  <type>aar</type>
</dependency>
```

*Release (SDK 7+)*

(There is no official SDK 7+ support onwards from 1.1.)

```xml
<dependency>
  <groupId>net.rdrei.android.dirchooser</groupId>
  <artifactId>library</artifactId>
  <version>1.0-pre-v11</version>
  <type>apklib</type>
</dependency>
```


*AAR Snapshot (SDK 11+)*

```groovy
compile 'net.rdrei.android.dirchooser:library:1.1-SNAPSHOT@aar'
```

*APK Snapshot (SDK 11+)*

```xml
<dependency>
  <groupId>net.rdrei.android.dirchooser</groupId>
  <artifactId>library</artifactId>
  <version>1.1-SNAPSHOT</version>
  <type>apklib</type>
</dependency>
```

*Snapshot (SDK 7+)*

```xml
<dependency>
  <groupId>net.rdrei.android.dirchooser</groupId>
  <artifactId>library</artifactId>
  <version>1.1-pre-v11-SNAPSHOT</version>
  <type>apklib</type>
</dependency>
```

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

Apps using this
---------------

<table>
    <tr>
        <td>
            <a href="https://play.google.com/store/apps/details?id=net.rdrei.android.scdl2">
                <img src="https://lh6.ggpht.com/u6DlMjd2bCJ0OUAcUEe89rlLyg0Hv16x_vDHrCjCgRZCyyoaF4wiDsTDVT4YDxyaSw=w150-rw"
                    title="Downloader for SoundCloud"
                    alt="Downloader for SoundCloud">
                <div>Downloader for SoundCloud</div>
            </a>
        </td>
        <td>
            <a href="https://play.google.com/store/apps/details?id=de.j4velin.wallpaperChanger">
                <img src="https://lh6.ggpht.com/Sz46BVptRkjMyeOBxaUip66CMhnKk5MYxZZlxkwCXL3_Ue_ITvQ3_cunU1cYI1FPaQ=w150-rw"
                    title="Wallpaper Changer"
                    alt="Wallpaper Changer">
                <div>Wallpaper Changer</div>
            </a>
        </td>
    </tr>
</table>

To add your own app, please send a pull request.

Releasing
---------

*Preparation*

To release a new snapshot on Maven Central, add your credentials to
`~/.me/settings.xml` (you get them from http://oss.sonatype.org):

```xml
<settings>
  <servers>
    <server>
      <id>sonatype-nexus-snapshots</id>
      <username>somestring</username>
      <password>somepassword</password>
    </server>
    <server>
      <id>sonatype-nexus-staging</id>
      <username>somestring</username>
      <password>somepassword</password>
    </server>
  </servers>
</settings>

```

*Staging*

To upload a new snapshot, just run gradle, followed by maven deploy:

```
gradle build && mvn clean deploy
```

*Release*

```
gradle build
mvn release:clean
mvn release:prepare
mvn release:perform
```

Alternatively to the last step:

```
mvn gpg:sign-and-deploy-file -Durl=https://oss.sonatype.org/service/local/staging/deploy/maven2/ -DrepositoryId=sonatype-nexus-staging -DpomFile=library/target/library-x.x.pom -Dfile=library/build/libs/library-x.x.aar -Dpackaging=aar
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
 [2]: https://github.com/passy/Android-DirectoryChooser/tree/pre-v11
 [3]: https://play.google.com/store/apps/details?id=net.rdrei.android.dirchooser.sample
