更新Android Studio代码：

3 编写APP代码
a. 包含什么
out/target/common/obj/JAVA_LIBRARIES/framework_intermediates/classes.jar

How do I build the Android SDK with hidden and internal APIs available?
http://stackoverflow.com/questions/7888191/how-do-i-build-the-android-sdk-with-hidden-and-internal-apis-available

b. 怎么包含
Creating a module library and adding it to module dependencies
https://www.jetbrains.com/idea/help/configuring-module-dependencies-and-libraries.html

Creating a module library and adding it to module dependencies
1.Open the Project Structure dialog (e.g. Ctrl+Shift+Alt+S).
2.In the left-hand pane of the dialog, select Modules.
3.In the pane to the right, select the module of interest.
4.In the right-hand part of the dialog, on the Module page, select the Dependencies tab.
5.On the Dependencies tab, click add and select Jars or directories.
6.In the dialog that opens, select the necessary files and folders. These may be individual .class and .java files, directories and archives (.jar and .zip) containing such files as well as directories with Java native libraries (.dll, .so or .jnilib). Click OK.
7.If necessary, select the Export option and change the dependency scope.
8.Click OK in the Project Structure dialog.

编译错误
a. java.lang.OutOfMemoryError: GC overhead limit exceeded

Android Studio Google jar causing GC overhead limit exceeded error
http://stackoverflow.com/questions/25013638/android-studio-google-jar-causing-gc-overhead-limit-exceeded-error

解决办法：
Add this to your android closure in your build.gradle file:
dexOptions {
    javaMaxHeapSize "4g"
}

b. Too many field references
解决办法：
1.在project-app-src-build.gradle中修改：
1.1
在defaultConfig {
  // Enabling multidex support.
        multiDexEnabled true
}
1.2
dependencies {
  compile 'com.android.support:multidex:1.0.0'
}
2.在project-app-src-main-res-AndroidManifest.xml修改：
<application
        ...
        android:name="android.support.multidex.MultiDexApplication"
        ...
    </application>

Building Apps with Over 65K Methods
https://developer.android.com/tools/building/multidex.html

Configuring Your App for Multidex with Gradle
The Android plugin for Gradle available in Android SDK Build Tools 21.1 and higher supports multidex as part of your build configuration. Make sure you update the Android SDK Build Tools tools and the Android Support Repository to the latest version using the SDK Manager before attempting to configure your app for multidex.

Setting up your app development project to use a multidex configuration requires that you make a few modifications to your app development project. In particular you need to perform the following steps:

Change your Gradle build configuration to enable multidex
Modify your manifest to reference the MultiDexApplication class
Modify your app Gradle build file configuration to include the support library and enable multidex output, as shown in the following Gradle build file snippet:

android {
    compileSdkVersion 21
    buildToolsVersion "21.1.0"

    defaultConfig {
        ...
        minSdkVersion 14
        targetSdkVersion 21
        ...

        // Enabling multidex support.
        multiDexEnabled true
    }
    ...
}

dependencies {
  compile 'com.android.support:multidex:1.0.0'
}
Note: You can specify the multiDexEnabled setting in the defaultConfig, buildType, or productFlavor sections of your Gradle build file.

In your manifest add the MultiDexApplication class from the multidex support library to the application element.

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.android.multidex.myapplication">
    <application
        ...
        android:name="android.support.multidex.MultiDexApplication">
        ...
    </application>
</manifest>


