## 德龙除湿机改造，通过ESPhome控制接入homeassistant
![1](https://github.com/Griddz/delong-dehumidification-hz/blob/main/%E6%88%AA%E5%B1%8F2024-06-14%2014.07.28.png)
### 德龙除湿机照片
![3](https://github.com/Griddz/delong-dehumidification-hz/blob/68925bcedc6171949328a0cf1243ec6983e5d9fe/image/IMG_1312%20%E5%A4%A7.png)
### 电压测量记录：
![2](https://github.com/Griddz/delong-dehumidification-hz/blob/ccd5cdc13bc65598f94d9fe02108713f1a27075d/image/12pin%E6%8F%92%E5%A4%B4%E7%94%B5%E5%8E%8B%E6%B5%8B%E9%87%8F%E8%AE%B0%E5%BD%95.png)
根据电压测量记录得出各针高电平时的状态：
- **pin1:水满状态**
- **pin6:水泵正在储水状态**
- **pin7:水泵排水状态**
- **pin8:风扇高档状态**
- **pin9:风扇低档状态**
- **pin10:化霜状态**
- 
### 材料：
1. 德龙除湿机型号：DD30P
2. 配件：
- ESP32开发板一个（有5V供电脚）
- 单向电平转换模块 5V与3.3V，[淘宝购买连接](https://detail.tmall.com/item.htm?id=41275922276&spm=a1z09.2.0.0.779e2e8dqbkCIT&_u=e3u5cah0a0d)
- 5V小型继电器模块4路2路的各一个，**一定要买小型继电器模块！** 大的放不进去，[淘宝购买连接](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.779e2e8dqbkCIT&id=714450413157&_u=e3u5cah110d)
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
#### 图片
![22](https://github.com/Griddz/delong-dehumidification-hz/blob/ccd5cdc13bc65598f94d9fe02108713f1a27075d/image/22-total.jpg)
![23](https://github.com/Griddz/delong-dehumidification-hz/blob/ccd5cdc13bc65598f94d9fe02108713f1a27075d/image/23-12pin.jpg)
![25](https://github.com/Griddz/delong-dehumidification-hz/blob/ccd5cdc13bc65598f94d9fe02108713f1a27075d/image/25-pcb.jpg)
![26](https://github.com/Griddz/delong-dehumidification-hz/blob/ccd5cdc13bc65598f94d9fe02108713f1a27075d/image/26-solderline.jpg)
