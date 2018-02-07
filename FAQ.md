# Frequently Asked Questions

## How do I connect to my IxE when my laptop is on *eduroam* or *RedRover* and my Pi is connected to DeviceFarm in Bloomberg or Tata?

If your laptop is on *eduroam* or *RedRover* and you would like to remotely connect to your IxE using `ssh` and see a webpage served from port `8000` follow these directions.

(Note: Replace **[00]** with your interaction engine number on your SD card.)

### If your laptop is on eduroam or RedRover and your IxE is on DeviceFarm in **TATA**
For SSH use:
```
ssh pi@interactive-device-design-1.tech.cornell.edu -p 122[00]  
```

Connect to the Website
```
interactive-device-design-1.tech.cornell.edu:280[00]
```

### If your laptop is on eduroam or RedRover and your IxE is on DeviceFarm in **BLOOMBERG**
For SSH use:

```
ssh pi@interactive-device-design-2.tech.cornell.edu -p 122[00]  
```

Connect to the Website

```
interactive-device-design-2.tech.cornell.edu:280[00]
```