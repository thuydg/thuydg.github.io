---
layout: blog
title: AndroidManifest.xml and all about it!
category: blog
tags: [android]
summary: What I interested in AndroidManifest and how it work
image: http://www.leadinge.co.jp/common/img/androids.gif
---

# What is Android Manifest

In the root directory and store basic info about app structures and its settings.

* names the Java package for the application<a unique identifier for the application.>
* components of the application — the activities, services, broadcast receivers, and content providers that the application is composed of. It names the classes that implement each of the components and publishes their capabilities (for example, which Intent messages they can handle).
* processes will host application components.
* permissions the application must have in order to access protected parts of the API and interact with other applications.
* permissions that others are required to have in order to interact with the application's components.
* It lists the Instrumentation classes that provide profiling and other information as the application is running. (removed before the application is published)
* It declares the minimum level of the Android API that the application requires.
* It lists the libraries that the application must be linked against.


{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>

<manifest>

    <uses-permission />
    <permission />
    <permission-tree />
    <permission-group />
    <instrumentation />
    <uses-sdk />
    <uses-configuration />  
    <uses-feature />  
    <supports-screens />  
    <compatible-screens />  
    <supports-gl-texture />  

    <application>

        <activity>
            <intent-filter>
                <action />
                <category />
                <data />
            </intent-filter>
            <meta-data />
        </activity>

        <activity-alias>
            <intent-filter> . . . </intent-filter>
            <meta-data />
        </activity-alias>

        <service>
            <intent-filter> . . . </intent-filter>
            <meta-data/>
        </service>

        <receiver>
            <intent-filter> . . . </intent-filter>
            <meta-data />
        </receiver>

        <provider>
            <grant-uri-permission />
            <meta-data />
            <path-permission />
        </provider>

        <uses-library />

    </application>

</manifest>
{% endhighlight %}

# What to remember

# Reference

* [Android document](http://developer.android.com/guide/topics/manifest/manifest-intro.html)
