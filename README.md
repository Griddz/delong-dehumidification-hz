#ESP32接线说明：
##按纽：
    .power_button <----------> GPIO16
    .fan_button   <----------> GPIO17
    .pump_button  <----------> GPIO18
    .plus_button  <----------> GPIO19
    .sub_button   <----------> GPIO21
二进制状态线：
    1.83waterfull_is_on <----------> GPIO13
    2.84fan_high_is_on  <----------> GPIO26
    3.85fan_low_is_on   <----------> GPIO27
    4.87compressor_is_on <----------> GPIO14
    5.88pump_water_accumulation <----------> GPIO25
    6.89pump_draining <----------> GPIO23
