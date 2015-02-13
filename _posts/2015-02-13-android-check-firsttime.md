---
layout: blog
title: Android Develop Apps memo
category: blog
tags: [android]
summary: Android apps things
image: http://www.leadinge.co.jp/common/img/androids.gif
---

# How to check if the activity is runned when install only?

{% highlight xml %}
    //Check first time run
    final String PREFS_NAME = "MyPrefsFile";
    SharedPreferences settings = getSharedPreferences(PREFS_NAME, 0);
    if (settings.getBoolean("my_first_time_new", true)) {
        //the app is being launched for first time, do something
        Log.d("Comments", "First time");
                 // first time task
        // record the fact that the app has been started at least once
        settings.edit().putBoolean("my_first_time_new", false).commit();
    } else {
      Log.d("Comments", "NOT First time");
    }
{% endhighlight %}

# Refences:

* [Stack1 - Using SharedPreferences](http://stackoverflow.com/questions/4636141/determine-if-android-app-is-the-first-time-used)
* [Stack2 - Get installation time](http://stackoverflow.com/questions/2831333/how-to-get-app-install-time-from-android)
