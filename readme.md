# Quick Guide: Identifying HDA Device for hda-verb

## Overview
Use `hda-verb` to send low-level commands to the **High Definition Audio (HDA) codec** in Linux. Identify the correct device path in this format:

```sh
/dev/snd/hwC<ID>D<ID>
```

## Steps to Find Your HDA Device

### **1. List Sound Cards**
```sh
cat /proc/asound/cards
```
Example output:
```
 0 [PCH ]: HDA-Intel - HDA Intel PCH
 1 [HDMI ]: HDA-Intel - HDA ATI HDMI
```
- **Card 0** = onboard audio
- **Card 1** = HDMI audio

### **2. List HDA Devices**
```sh
ls /dev/snd/
```
Example output:
```
controlC0  controlC1  hwC0D0  hwC1D0
```
- `hwC0D0` → **Card 0, Device 0**
- `hwC1D0` → **Card 1, Device 0**

### **3. Verify Codec Nodes**
```sh
cat /proc/asound/card<ID>/codec#*
```
Example:
```sh
cat /proc/asound/card0/codec#*
```
Shows codec nodes and **Node IDs (NIDs)** for `hda-verb`.

### **4. Use in hda-verb**
```sh
hda-verb /dev/snd/hwC1D0 0x20 0x400 0x0
```
- `/dev/snd/hwC1D0` = Device path
- `0x20` = **Node ID (NID)**
- `0x400` = **Command (verb)**
- `0x0` = **Parameter**

## Conclusion
Follow these steps to identify and use the correct `/dev/snd/hw(device id)` for `hda-verb`, then edit and run the script.
Its not nessecary to restart. Be amazed as your audio is finaly working for native Linux on the Razer.

