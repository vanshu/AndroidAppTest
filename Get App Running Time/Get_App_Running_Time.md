## Get App Running Time

#### 1.先查找要检测启动时间的APP的进程，通过以下命令进行进程查找
* On Windows:adb logcat | findstr START
* On MacOS/Linux: adb logcat | grep START

```{r, engine='bash', count_lines}
01-09 03:59:00.291   996  3260 I ActivityManager: START u0 {act=android.intent.action.MAIN cat=[android.intent.category.LAUNCHER]
flg=0x4000000 cmp=com.google.android.youtube/com.google.android.apps.youtube.app.WatchWhileActivity
bnds=[579,1229][747,1397] (has extras)} from uid 10090 on display 0
```

#### 2.adb shell am start -W -n package/activity
* 获取youtube首次启动时间 ,ThisTime 就是启动的时间，检测分为冷启动和冷启动，热启动，冷启动表示APP没有后台运行的启动，热启动表示APP在后台有运行
* adb shell am start -W -n com.google.android.youtube/com.google.android.apps.youtube.app.WatchWhileActivity


```{r, engine='bash', count_lines}
Starting: Intent { cmp=com.google.android.youtube/com.google.android.apps.youtube.app.WatchWhileActivity }
Status: ok
Activity: com.google.android.youtube/com.google.android.apps.youtube.app.WatchWhileActivity
ThisTime: 1749
TotalTime: 1749
WaitTime: 1762
Complete
```

#### 3.输入home键回退到Launcher:adb shell input keyevent 3 

#### 4.停止app
* adb shell am force-stop package(这里只需要传入package,操作系统会杀死进程)
* adb shell am force-stop com.google.android.youtube
