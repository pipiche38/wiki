# Reinstall Plugin and keep Database and Configuration

## Overview

Purpose is to do a re-install of the plugin without loosing any data

You have __critical__ files under the Domoticz-Zigbee folder. In case of crash, you might want to have backup to restore. Here after are the files to backup

    Conf/PluginConf-*.json
    Data/*
    Reports/*

Of course you must backup the Domoticz Database `domoticz.db` (check to Domoticz) __at the same time__ in order to have consistency between the two.

## Since stable8: data also stored in Domoticz

Since the __stable8__ version, the plugin __also__ stores all of its information directly into the Domoticz database (`domoticz.db`), in addition to the `Data/DeviceList-xx.txt` files.

This greatly simplifies re-installations: as all the relevant plugin information is already kept inside the Domoticz database, restoring that database is, in practice, enough to recover the plugin state, without having to manually copy back the `Data/` folder.

However, in order to be able to troubleshoot potential issues, the plugin is still able to load the data the legacy way, from the `Data/DeviceList-xx.txt` files. This fallback is used __if and only if__ the timestamp of those files is more recent than the timestamp of the data written into Domoticz. Otherwise, the data stored in the Domoticz database is used.

> __Note__: it is still recommended to back up all the items listed above (and especially the `Data/` folder) as an extra safety net.

## Assumption

* Domoticz plugins are located in ```/home/pi/domoticz/plugins ```
* ZigBeeForDomoticZ plugin has been installed by default under ```/home/pi/domoticz/plugins/Domoticz-Zigbee```

In case this is different, please use your own location


## Procedure

1. Stop domoticz

1. Copy the ZigBeeForDomoticZ plugin folder to your home directory

   ```
   cp -r /home/pi/domoticz/plugins/Domoticz-Zigbee /home/pi
   ```

1. Install the fresh version of the plugin

see Instalaltion page

1. Copy the ZigBeeForDomoticZ plugin database to the new installation

   ```
   cp /home/pi/Domoticz-Zigbee/Data/* /home/pi/domoticz/plugins/Domoticz-Zigbee/Data
   ```

1. Copy the Plugin configurations file

   ```
   cp /home/pi/Domoticz-Zigbee/Conf/PluginConf* /home/pi/domoticz/plugins/Domoticz-Zigbee/Conf
   ```

1. Copy the Plugin reports (if you want to keep the old reports)

   ```
   cp /home/pi/Domoticz-Zigbee/Reports/* /home/pi/domoticz/plugins/Domoticz-Zigbee/Reports
   ```

   At that stage you have a copy of the Old plugin in /home/pi/Domoticz-Zigbee and a new version ready to be launched in ```/home/pi/domoticz/plugins/Domoticz-Zigbee```

1. You can now restart DomoticZ
