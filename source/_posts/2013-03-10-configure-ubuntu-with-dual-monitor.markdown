---
layout: post
title: "Configure Ubuntu with Dual Monitor"
date: 2013-03-10 09:11
comments: true
categories: linux 
---

## Goals:

Setting ubuntu monitor like this:

    LCD with HDMI --> Laptop Monitor

## Solutions:

Create a xrandr script, named as `dual_monitor`:

    #!/bin/sh
    if [ "$1" != "off" ]; then
      # External Screen as HDMI, Laptop below
      echo "Dual Screen on"
      xrandr --output VGA1 --off
      xrandr --output HDMI1 --primary --mode 1920x1080
      xrandr --output LVDS1 --off
      xrandr --output LVDS1 --mode 1600x900 --right-of HDMI1
    else
      # External Screen off, Laptop primary
      echo "Dual Screen off"
      xrandr --output HDMI1 --off
      xrandr --output LVDS1 --primary --mode 1600x900
    fi
    
To use it conveniently, add the directory into $PATH.

Start dual monitor mode with:
    
    dual_monitor

Stop dual monitor mode with:
   
    dual_monitor off

## Reference
+ [AskUbuntu:"Setting primary monitor on dual display"](http://ubuntuforums.org/showthread.php?t=1801549 "Setting primary monitor on dual display")
