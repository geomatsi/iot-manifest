# pcDuino upstream
Manifest for pcDuino IoT Yocto distro based on upstream kernel and u-boot

## Fetch yocto layers

$ mkdir -p /home/builder/project/source  
$ mkdir -p /home/builder/project/build  
$ cd /home/builder/project/source  
$ repo init -u git@github.com:geomatsi/iot-manifest.git -b pcduino-upstream  

## Prepare yocto build environment

$ cd poky  
$ source oe-init-build-env /home/builder/project/build  

## Add the following layers to bblayers.conf:

```
...

BBLAYERS ?= " \
 /home/builder/project/source/poky/meta \
 /home/builder/project/source/poky/meta-poky \
 /home/builder/project/source/meta-openembedded/meta-oe \
 /home/builder/project/source/meta-openembedded/meta-python \
 /home/builder/project/source/meta-openembedded/meta-networking \
 /home/builder/project/source/meta-nodejs \
 /home/builder/project/source/meta-sunxi \
 /home/builder/project/source/meta-iot-simple \
 "
...

```

## Edit build settings

1. Replace default machine definition in local.conf:

```
MACHINE = "pcduino"
```

2. Add preferred nodejs provider to local.conf:

```
PREFERRED_PROVIDER_node = "nodejs"
PREFERRED_PROVIDER_node-native = "nodejs-native"
```

## Building the image

$ bitbake iot-image-base  
or  
$ bitbake iot-image-web  

# pcDuino sunxi
Manifest for pcDuino IoT Yocto distro based on legacy linux-sunxi kernel and u-boot

## Fetch yocto layers

$ mkdir -p /home/builder/project/source  
$ mkdir -p /home/builder/project/build  
$ cd /home/builder/project/source  
$ repo init -u git@github.com:geomatsi/iot-manifest.git -b pcduino-sunxi  

## Prepare yocto build environment

$ cd poky  
$ source oe-init-build-env /home/builder/project/build  

## Add the following layers to bblayers.conf:

```
...

BBLAYERS ?= " \
 /home/builder/project/source/poky/meta \
 /home/builder/project/source/poky/meta-yocto \
 /home/builder/project/source/meta-openembedded/meta-oe \
 /home/builder/project/source/meta-openembedded/meta-python \
 /home/builder/project/source/meta-openembedded/meta-networking \
 /home/builder/project/source/meta-sunxi \
 /home/builder/project/source/meta-iot-simple \
 "
...

```

## Edit build settings

1. Replace default machine definition in local.conf:

```
MACHINE = "pcduino-lite-wifi"
```

## Building the image

$ bitbake iot-image-base  

# BeagleBone
Manifest for BeagleBone IoT Yocto distro

## Fetch yocto layers

$ mkdir -p /home/builder/project/source  
$ mkdir -p /home/builder/project/build  
$ cd /home/builder/project/source  
$ repo init -u git@github.com:geomatsi/iot-manifest.git -b beaglebone  

## Prepare yocto build environment

$ cd poky  
$ source oe-init-build-env /home/builder/project/build  

## Add meta-sunxi layer to the build environment

```
--- a/conf/bblayers.conf
+++ b/conf/bblayers.conf
@@ -9,6 +9,7 @@ BBLAYERS ?= " \
    /home/builder/project/source/poky/meta \
    /home/builder/project/source/poky/meta-yocto \
-   /home/builder/project/source/poky/meta-yocto-bsp \
+   /home/builder/project/source/meta-openembedded/meta-oe \
+   /home/builder/project/source/meta-beagle \
+   /home/builder/project/source/meta-iot-simple \
"
BBLAYERS_NON_REMOVABLE ?= " \
    /home/builder/project/source/poky/meta \
```

## Edit build settings

1. Replace default machine definition in local.conf:

```
MACHINE = "beaglebone"
```

## Building the image

$ bitbake core-image-base  
