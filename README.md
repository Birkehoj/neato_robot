## Neato Drivers

This repository contains the Neato ROS drivers, catkinized, and ready for ROS Hydro and newer.

## Usage
You can check this out into your catkin workspace as follows:

    cd <ws>/src
    git clone https://github.com/jlohse/neato_robot.git
    cd <ws>
    catkin_make
    source <ws>/devel/setup.bash

## Changes in jlohse's fork

 * The driver has been changed from the original version in order to support a wider range of neato models and firmware versions.
 * This node works with Indigo. The required third parameter to rospy.Publisher() has been supplied.
 * A minor issue in xv11::setMotors() has been fixed. Due to incorrect indentation in that function neato used to slowly crawl forward.

## Changes in wphan's fork

 * modified some files(neato.py and neato_driver.py) to fix errors I was having
 * ultimately ran on with meta-ros layer running on a Gumstix Overo COM on a Tobi expansion board
        connected to a Neato XV Signature

### Yocto bitbake Recipes 
Place the bitbake recipes in your Yocto build environment:
```
user@HOSTNAME:~/Documents/yocto/poky/meta-gumstix-extras/recipes-ros/neato-robot$ ls
neato-2dnav.bb  neato-driver.bb  neato-node.bb  neato-robot.bb  neato-robot.inc
```


##### neato-robot.inc (change ```SRCREV``` to match latest commit)
```
SRC_URI = "https://github.com/wphan/${ROS_SPN}/archive/${SRCREV}.tar.gz;downloadfilename=${ROS_SP}.tar.gz"

SRCREV = "67906ca9ca5990e5c1cca15f0e185c5c2c019742" 

SRC_URI[md5sum] = "a93213a144980edc19c24d590ef077ce"
SRC_URI[sha256sum] = "2abfa06a4c21db7241042d025ecf6654c07c45de45322907e536e1d11c3f383b"
S = "${WORKDIR}/${ROS_SPN}-${SRCREV}/${ROS_BPN}"

inherit catkin

ROS_SPN = "neato_robot"

```

##### neato-robot.bb
```
DESCRIPTION = "Metapackage for drivers for the Neato XV-11 robot."
SECTION = "devel"
LICENSE = "BSD"
LIC_FILES_CHKSUM = "file://package.xml;beginline=9;endline=9;md5=d566ef916e9dedc494f5f793a6690ba5"

DEPENDS = "neato-driver neato-node neato-2dnav"

require neato-robot.inc
```

##### neato-2dnav.bb
```
DESCRIPTION = "This package contains configuration and launch files for using the navigation stack with the Neato XV-11 robot."
SECTION = "devel"
LICENSE = "BSD"
LIC_FILES_CHKSUM = "file://package.xml;beginline=9;endline=9;md5=d566ef916e9dedc494f5f793a6690ba5"

require neato-robot.inc

RDEPENDS_${PN} = "neato-node"

```

##### neato-driver.bb
```
DESCRIPTION = "This is a generic drivers for the Neato XV-11 Robotic Vacuum."
SECTION = "devel"
LICENSE = "BSD"
LIC_FILES_CHKSUM = "file://package.xml;beginline=9;endline=9;md5=d566ef916e9dedc494f5f793a6690ba5"

RDEPENDS_${PN} = "python-pyserial"

require neato-robot.inc
```

##### neato-node.bb
```
DESCRIPTION = "A node wrapper for the neato_driver package."
SECTION = "devel"
LICENSE = "BSD"
LIC_FILES_CHKSUM = "file://package.xml;beginline=9;endline=9;md5=d566ef916e9dedc494f5f793a6690ba5"

RDEPENDS_${PN} = "neato-driver sensor-msgs geometry-msgs nav-msgs tf"

require neato-robot.inc
```

