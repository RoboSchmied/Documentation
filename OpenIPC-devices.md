![OpenIPC logo][logo]

## OpenIPC settings

**This page is personal notes by @RoboSchmied for public reading only and may not be edited by others**

### Device table for customization

* [gk7205v210-sc223a-okaidi](#gk7205v210-sc223a-okaidi)


-------


### gk7205v210-sc223a-okaidi 


```
cli -s .system.staticDir /var/www/majestic
cli -s .nightMode.enabled true
cli -s .nightMode.irCutPin1 9
cli -s .nightMode.irCutPin2 8
cli -s .nightMode.backlightPin 14
cli -s .nightMode.minThreshold 6000
cli -s .nightMode.maxThreshold 14000
cli -s .nightMode.colorToGray false
cli -s .nightMode.drcOverride 300
cli -s .nightMode.dncDelay 1
cli -s .video0.codec h264
cli -s .hls.enabled false
```


[logo]: https://openipc.org/assets/openipc-logo-black.svg
[chat]: https://openipc.org/images/telegram_button.svg
[site]: https://openipc.org/images/openipc_button.svg
[site_basic]: https://openipc.org
[telegram_en]: https://t.me/OpenIPC
