## Compile [exf1ctrl](https://github.com/jsolsen/exf1ctrl) on Linux

Control your Casio EX-F1 (High Speed Camera) by command line tool or script using a small open source embedded linux machine like [CubieBoard](http://cubieboard.org) or [Odroid](http://www.hardkernel.com).

tested on: [Cubian](http://www.cubian.org), [Linaro](http://www.linaro.org), [Ubuntu](http://www.ubuntu.com), [Debian](http://www.debian.org/) and [OpenWrt](http://www.openwrt.org/)

### get compiler and tools 
```
sudo apt-get update
sudo apt-get install build-essential git
```

### get source

```
git clone https://github.com/jsolsen/exf1ctrl.git exf1ctrl-read-only
```

```console
Klone nach 'exf1ctrl-read-only'...
remote: Counting objects: 563, done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 563 (delta 0), reused 0 (delta 0), pack-reused 549
Empfange Objekte: 100% (563/563), 7.87 MiB | 206.00 KiB/s, Fertig.
Löse Unterschiede auf: 100% (264/264), Fertig.
Prüfe Konnektivität... Fertig.
```

### first try

```
cd exf1ctrl-read-only/prj/NetBeans/exf1Ctrl/
make
```

```console
In file included from ../../../src/libexf1.h:11:0,
                 from ../../../src/exf1api.h:11,
                 from ../../../src/exf1ctrl.h:11,
                 from ../../../src/exf1ctrl.cpp:11:
../../../src/exf1usb.h:49:21: fatal error: usb.h: Datei oder Verzeichnis nicht gefunden
     #include
```

### install missing libusb-dev

```
sudo apt-get install libusb-dev
make 
```

```console
g++    -c -g -I/usr/local/include/opencv/ -MMD -MP -MF build/Debug/GNU-Linux-x86/_ext/1386528437/exf1ctrl.o.d -o build/Debug/GNU-Linux-x86/_ext/1386528437/exf1ctrl.o ../../../src/exf1ctrl.cpp
In file included from ../../../src/exf1ctrl.h:11:0,
                 from ../../../src/exf1ctrl.cpp:11:
../../../src/exf1api.h:13:16: fatal error: cv.h: Datei oder Verzeichnis nicht gefunden
 #include <cv.h>
                ^
compilation terminated.
```

### install missing lib
```
sudo apt-get install libopencv-dev
```

#### In this case cv is expected in /usr/local/include, but located in /usr/include, so link it: 
```
sudo ln -s /usr/include/opencv /usr/local/include/opencv
make
```
```console
g++    -c -g -I/usr/local/include/opencv/ -MMD -MP -MF build/Debug/GNU-Linux-x86/_ext/1386528437/exf1api.o.d -o build/Debug/GNU-Linux-x86/_ext/1386528437/exf1api.o ../../../src/exf1api.cpp
make[2]: *** Keine Regel vorhanden, um das Target »/usr/lib/arm-linux-gnueabi/libusb.a«, 
  benötigt von »dist/Debug/GNU-Linux-x86/exf1ctrl«, zu erstellen.  Schluss.
make[2]: Leaving directory `/home/cubie/TRUNK/exf1ctrl-read-only/prj/NetBeans/exf1Ctrl'
make[1]: *** [.build-conf] Fehler 2
```

### link /usr/lib/arm-linux-gnueabihf/  to /usr/lib/arm-linux-gnueabi/
```
sudo ln -s /usr/lib/arm-linux-gnueabihf /usr/lib/arm-linux-gnueabi
make
```

### compiling done 

```
cd dist/Debug/GNU-Linux-x86/
./exf1ctrl 
```

```console
> Initializing camera... 
 Error: setting config 1. 
usbStart failed!
```

### start as superuser

```
sudo ./exf1ctrl 
```

### it works

```console
 ********************************************************************
 *                                                                  *
 *  ExF1Ctrl ver. 0.2                                               *
 *  -----------------                                               *
 *  This program is able to interface to the Casio EX-F1 over USB.  *
 *  Firmware rev. 2.00 is required and the camera must be put in    *
 *  remote control mode before being connected to the host.         *
 *  --                                                              *
 *  Jens Skovgaard Olsen                                            *
 *  info@feinschmeckerfoosball.com                                  *
 *                                                                  *
 ********************************************************************
 
 Hint: a [x] sets aperture (x = 1-10).
          1: F2.7 (default).
          2: F3.0.
          3: F3.3.
          4: F3.8.
          5: F4.2.
          6: F4.7.
          7: F5.3.
          8: F6.0.
          9: F6.7.
         10: F7.5.
 
 Hint: c [x [y]] sets mode / movie mode (x = 1-9).
          1: Single shot (default).
          2: Continuous shutter.
          3: Prerecord still image.
          4: Movie (STD).
          5: Prerecord movie (STD).
          6: Movie (HD).
          7: Prerecord movie (HD).
          8: Movie (HS).
          9: Prerecord movie (HS).
       In high speed mode y determines the framerate:
          1: 300FPS.
          2: 600FPS.
          3: 1200FPS.
          4: 30-300FPS.

 Hint: e [x] sets exposure (x = 1-4).
          1: M.
          2: Auto (default).
          3: A.
          4: S.

 Hint: f [x] sets focus (x = 1-4).
          1: Auto (default).
          2: Macro.
          3: Infinity.
          4: Manual.

 Hint: h activates half press.

 Hint: i [x] sets iso (x = 1-6).
          1: Auto (default).
          2: 100.
          3: 200.
          4: 400.
          5: 800.
          6: 1600.

 Hint: l [x] sets flash mode (x = 1-4).
          1: Auto (default).
          2: Off.
          3: On.
          4: External.

 Hint: p [x] sets shutter speed (x = 1-64). Exposure must be set to manual.
          1: 60.
          2: 50.
          ...
          64: 1/40000.

 Hint: q quits this program.

 Hint: m [x [y]] records a x second long movie called y.

 Hint: s [x [y [z]]] activates shutter and stores a picture called x
       and a thumbnail called y. If the continous shutter is enabled
       (modes 2 and 3), z determines the shutter duration.

 Hint: v [x [y]] focus y steps. x=in focuses in and x=out focuses out.
       Continous focus is used if y is not defined.

 Hint: z [x [y]] zooms y steps. x=in zooms in and x=out zooms out.
       Continous zoom is used if y is not defined.


> Initializing camera... 
> > Configuring focus... 
> > Configuring flash mode... 
> > Configuring shutter mode / movie mode... 
> > Configuring ISO... 
> > Configuring exposure... 
> > Configuring shutter speed... 
> > Taking picture... 
> Transferring 1186056 bytes... 
> CIMG001.jpg saved to disk. 
> Transferring 7776 bytes... 
> CIMG001_thumb.jpg saved to disk. 
> Exit done
> Bye! 
```
