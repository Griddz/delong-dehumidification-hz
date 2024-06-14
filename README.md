## 德龙除温机改造，通过ESPhome控制接入homeassistant
### 材料：
1. 德龙除湿机型号：DD30P
2. 配件：
- ESP32开发板一个（有5V供电脚）
- 单向电平转换模块 5V与3.3V，淘宝购买连接`https://detail.tmall.com/item.htm?id=41275922276&spm=a1z09.2.0.0.779e2e8dqbkCIT&_u=e3u5cah0a0d`
- 5V小型继电器模块4路2路的各一个，**一定要买小型继电器模块！** 大的放不进去，淘宝购买连接`https://item.taobao.com/item.htm?spm=a1z09.2.0.0.779e2e8dqbkCIT&id=714450413157&_u=e3u5cah110d`
-  
### ESP32接线说明：
#### 按纽：
1. power_button <----------> GPIO16
2. fan_button   <----------> GPIO17
3. pump_button  <----------> GPIO18
4. plus_button  <----------> GPIO19
4. sub_button   <----------> GPIO21
#### 二进制状态线：
1. 83waterfull_is_on <----------> GPIO13
2. 84fan_high_is_on  <----------> GPIO26
3. 85fan_low_is_on   <----------> GPIO27
4. 87compressor_is_on <----------> GPIO14
5. 88pump_water_accumulation <----------> GPIO25
6. 89pump_draining <----------> GPIO23
#### 电平转换器引脚：
1. DIR引脚 <---------> GPIO22
