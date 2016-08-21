**HOW TO DISABLE GOOGLE ADS IN ANDROID APPS**
                                        
Follow the steps to get an Ad-Free android app without paying extra for it. You can be the one who find ads irritating or someone who cares about the battery drain due to Ads(http://www.clic.cs.columbia.edu/~nieh/teaching/e6998/papers/eprof_eurosys2012.pdf).

Steps to reproduce:  
1. Get Apk file from mobile to laptop.  
2. Use Apktool to decompile the app(http://forum.xda-developers.com/showthread.php?t=2213985).  
3. In decompiled app, go to folder /res/values. Open files strings.xml and public.xml.   
4. Corrupt the strings with google ad ids(eg. display_activity_ad_unit_id). Changing any one number in the id would work. This way google admob will not be able to authenticate and communicate with the app.Every app developer has to put a unique id in strings.xml or public.xml file for communicating with google admob. Changing this id disables the ad.  
5. Recompile the app, sign it and reinstall it in mobile.  
6. App works as usual with no ads.   

Example(GeeksForGeeks Android App version 7.8.20):   
1. adb shell pm list packages -> adb shell pm path free.programming.programming -> adb pull /data/app/free.programming.programming-1.apk   
2. apktool if free.programming.programming-1.apk -> apktool d free.programming.programming-1.apk   
3. Open strings.xml file in free.programming.programming-1/res/values/ folder.   
4. Corrupt these 3 ids a) category_fragment_ad_unit_id, b) display_activity_ad_unit_id, c) disqus_activity_ad_unit_id For eg. change the last number to random number in 1-9 for each of the ids.   
5. apktool b free.programming.programming-1 -> java -jar signapk.jar certificate.pem key.pk8 D:\project3\SignApk\free.programming.programming-1.apk D:\project3\SignApk\signedapks\free.programming.programming-1.apk -> adb install free.programming.programming-1.apk   
6. App works as usual with no ads.   
7. Other examples : Merriam Dictionary, Dictionary.com  

Limitations :   
1. Many of the famous apps show ads from multiple ad sources. So, even if this method disables ads from Google, the app might still show you ads from a different source e.g. InMobi.     
2. Some app developers write the unique admob IDs' in java files which become incomprehensible smali files on decompiling.    
