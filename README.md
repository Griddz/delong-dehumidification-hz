## 德龙除湿机DD30P智能化改造，通过ESPhome控制接入homeassistant
![1](https://github.com/Griddz/delong-dehumidification-hz/blob/main/%E6%88%AA%E5%B1%8F2024-06-14%2014.07.28.png)
### 改造思路
- **本人非专业人士，项目仅作交流用。改造涉及强电，重则有生命危险，轻则损坏除湿机，本个概不负责，不承担任何法律责任！**
- 除湿机面板上七个按键，中间有一个显示屏，通过继电器来模拟其中的五个按键分别为电源、风量、+、—、Pump按键，另外两个按键分是温湿度的显示设定和定时设定没有模拟。拆开机器可以看到电路板上的每个按键背面有四个锡焊点，接其中两个点，一个点是与电路板接地相连的，如果不确定你可以用电线或摄子去短接两个点，除湿机有相应反应了，说明这两个点可以作为按键模拟的接线点。
- 电路板上有一个12针的插头，通过测量除湿机各种状态下的各针的电压值，用来反馈除湿机的各种状态。将对应针焊接连线接入电平转换模块转换成3V电平信号，再接入ESP32开发板。
- 注：德龙除湿机比较难拆，将近有20颗螺丝要卸。从后背开始卸，卸掉后背，再拆前盖，前盖与要焊接线的电路板固定在一起的，拔掉12针插头线就能卸下前盖，再从前盖取下电路板。
### 达成的效果
- 可以通过Homeassistant来控制开关、设定目标湿度值、设定风扇高低档、设定是否水泵排水并且有实时的状态反馈。
- 缺陷：
   1. 未能接入除湿机自带的湿度传感器。
   2. pin7反馈水泵排水，pin6反馈水泵临时储水状态。因为水泵不会一直处于排水状态，只有当机器储了一定数量的水后才会启动水泵排水。当你设定水泵排水时，pin7和pin6状态始终是相反的，这样就可以判断已设定为水泵排水。但是如果在pin6是ON时关掉除湿机，在打开除湿机时pin6是ON的状态，尽管这时没有设定用水泵排水。这表明无法完全用pin6和pin7来反馈是否是水泵排水状态！这个问题我无法解决。但是当机器断电重启或软重启时都会默认是水箱排水，这样如果你要设定水泵排水，只要重启一下机器，再按一下水泵排水模拟按键就能确保是水泵排水。强调一点只要pin7是on，则机器设定肯定是水泵排水。

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
- **pin11:5v供电正极** 给ESP32开发板、电平转换模块、继电器模组供电。
- **pin12: 5v供电零线**给ESP32开发板、电平转换模块、继电器模组供电。
### 材料：
1. 德龙除湿机型号：DD30P
2. 配件：
-    ESP32开发板一个（有5V供电脚）
-    单向电平转换模块 5V与3.3V，[淘宝购买连接](https://detail.tmall.com/item.htm?id=41275922276&spm=a1z09.2.0.0.779e2e8dqbkCIT&_u=e3u5cah0a0d)
-    5V小型继电器模块4路2路的各一个，**一定要买小型继电器模块！** 大的放不进去，[淘宝购买连接](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.779e2e8dqbkCIT&id=714450413157&_u=e3u5cah110d)
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
