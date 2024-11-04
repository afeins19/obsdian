# How to Connect the M5 Stack to the Arduino IDE 

### Installing Libraries 
1. Open the Arduino IDE 
2. go to preferences and paste this URL at the very last section labeled **additional board manager URLS** (This contains libaraires and exmaple code to interface with the M5CoreS3 through arduino): https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/arduino/package_m5stack_index.json
3. The link above makes the libraries available to the the Arduino IDE Library Manager. Navigate to the Library Manager and start searching "M5" - the "M5CoreS3" Library should then appear. You then click install to download it and make it available to the Arduino IDE 

### Connecting to your M5CoreS3 
1. connect the core s3 to your computer via the USB 
2. In the top menu bar, navigate to `tools -> board` and then select the M5CoreS3 
3. Now we must select the port through which your computer communicates with the M5. Go to `tools -> port` and then select the device that corresponds to the M5 


