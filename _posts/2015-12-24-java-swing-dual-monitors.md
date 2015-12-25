---
layout: post
title: Java Swing For Dual Monitors
cover: roma-building.jpg
date:   2015-12-24 22:00:00
categories: posts
---
##Java Swing For Dual Monitors
As nomal way to get screen size, we invoke method:

```java
java.awt.Toolkit.getDefaultToolkit().getScreenSize();
```
This is only works for single monitor settings.
When using multiple monitors, we need to know which monitor we are working on, to get the correct screen size.
```java
    public static Dimension getCurrentWindowDimension(Component c) {
        GraphicsEnvironment ge = GraphicsEnvironment.getLocalGraphicsEnvironment();
        GraphicsDevice[] screens = ge.getScreenDevices();
        Dimension screenSize = new Dimension();
        int n = screens.length;
        for (int i = 0; i < n; i++) {
        if(screens[i].getIDstring().contentEquals(c.getGraphicsConfiguration().getDevice().getIDstring()){
        screenSize.setSize(screens[i].getDisplayMode().getWidth(),screens[i].getDisplayMode().getHeight());
        }
        }
        return screenSize;
        }
```
