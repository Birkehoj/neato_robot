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

 * modified some files to work in a Yocto built Linux image
 * tested with meta-ros layer running on a Gumstix Overo COM on a Tobi expansion board
        connected to a Neato XV Signature
