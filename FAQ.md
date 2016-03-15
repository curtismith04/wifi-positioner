**Q: What do I need to run wifi-positioner?**

_A: If want to use/test it and don't want to have a lot of work, use it with .NET Version 4 and Windows 7_

**Q: Does wifi-positioner works in Windows XP?**

_A: Right now, it doesn't because it's based on a library called NativeWifi which has some problems with Windows XP ([see Issue](https://code.google.com/p/wifi-positioner/issues/detail?id=1))_

**Q: I'm getting errors, what should I do?**

_A: Post it as an [issue](https://code.google.com/p/wifi-positioner/issues/list) and try to explain the best you can what you have done to produce this error_

**Q: Does wifi-positioner works on Linux?**

_A: The .NET 4 version of wifi-positioner won't run in wine because the .NET Framework 4 is not running on wine. Check the appdb.winehq.com for this. I'm trying to create a version of wifi-positioner to run on [.NET 3.5](https://code.google.com/p/wifi-positioner/downloads/detail?name=WiFi_Positioner_v10_NET3.5.zip&can=2&q=) or even .NET 3.0. And I maybe try to compile it with mono, in order that you can run it on linux natively_