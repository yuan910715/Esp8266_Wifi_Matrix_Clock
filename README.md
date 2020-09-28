# Esp8266_Wifi_Matrix_Clock
A Esp8266 wifi matrix clock 

看不到图自行翻墙或查看Pics目录里的图  

# Video  
https://youtu.be/mZeVnjwp35k  
https://space.bilibili.com/402654671  

固件上传方法:   
how to upload firmware:  

如果你的开发板写入过其他程序(尤其是使用了EEPROM的),务必使用第二种Arduino IDE上传方法,webUpdate.ino会清除之前的EEPROM值.  
If your ESP8266 board has been written other programs (especially those using EEPROM), be sure to use the second Arduino IDE to upload, webUpdate.ino will clean old EEPROM value.  

#  ~~1.Flash tools~~

~~使用FlashESP8266.exe直接选择COM口,上传.bin固件(若无COM口 检查microUSB先是否正常以及是否有CP2102/CH340驱动程序)~~   
~~Open flashesp8266.exe , select COM port and upload. Bin firmware (if there is no COM port, check whether microusb cable is ok and CP2102 / ch340 driver)~~    
这个工具有很多人打不开，推荐使用第二种Arduino IDE方法烧录    
Many people cannot run this tool. It is recommended to use Arduino IDE to burn the firmware    

#  2.Arduino IDE
1.自行设置安装ESP8266开发板  
进入首选项（Preferences），找到附加开发板管理器地址（Additional Board Manager URLs），并在其后添加如下信息：  
1.Install ESP8266 board  
enter-（Preferences），find（Additional Board Manager URLs），add text：  
http://arduino.esp8266.com/stable/package_esp8266com_index.json   
![pic2.png](https://i.loli.net/2020/05/08/tlLTqHzFaPwCYUu.png)

2.点击工具 - 开发板 - 开发板管理器  
搜索ESP8266并安装  
2.open tools - board - board manager    
search ESP8266 and install  
![pic1.png](https://i.loli.net/2020/05/08/mNBRfaV4S8sb37I.png)  

选择开发板为Nodemcu 1.0  
select board : Nodemcu 1.0  

3.打开webUpdate.ino 修改wifi名和密码 烧录进Nodemcu后 打开网页上传.bin文件   
3.open webUpdate.ino modify wifi ssid and password,  after upload to board, open webpage and upload .bin file.     



![bom.jpg](https://github.com/yuan910715/Esp8266_Wifi_Matrix_Clock/blob/master/Pics/bom.jpg?raw=true)

![1.jpg](https://github.com/yuan910715/Esp8266_Wifi_Matrix_Clock/blob/master/Pics/1.jpg?raw=true)

![blue.jpg](https://github.com/yuan910715/Esp8266_Wifi_Matrix_Clock/blob/master/Pics/blue.jpg?raw=true)

![green.jpg](https://github.com/yuan910715/Esp8266_Wifi_Matrix_Clock/blob/master/Pics/green.jpg?raw=true)

![red.jpg](https://github.com/yuan910715/Esp8266_Wifi_Matrix_Clock/blob/master/Pics/red.jpg?raw=true)

使用DS18B20模块(use DS18B20 module)  
![wire.png](https://github.com/yuan910715/Esp8266_Wifi_Matrix_Clock/blob/master/Pics/wire.png?raw=true)

如果你没有DS18B20模块 只有DS18B20 可以自己接一个4k7上拉电阻(If you only have DS18B20(not module), you can add a 4k7 pull-up resistant)  
![wire1.png](https://github.com/yuan910715/Esp8266_Wifi_Matrix_Clock/blob/master/Pics/wire1.png?raw=true)
