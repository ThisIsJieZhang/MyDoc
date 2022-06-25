### 录屏

adb shell screenrecord --time-limit 20 --bit-rate 12000000 /sdcard/novel_start_2.mp4

### 通过adb导内存

```
adb shell am dumpheap com.tencent.mtt /data/local/tmp/a1.hprof
adb pull /data/local/tmp/a1.hprof /Users/zhangjie/Desktop
hprof-conv a1.hprof a1-out.hprof
```

### 通过adb输入字符（注意：&需用\&）

```adb shell input text ‘this is text’```

### 通过mttbrowser的scheme打开浏览器

``` adb shell am start -a android.intent.action.VIEW -d “mttbrowser://url=xxxxx,openType=1,PosID=1,ChannelID=xxx” ```