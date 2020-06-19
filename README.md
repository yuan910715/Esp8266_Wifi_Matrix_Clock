# Esp8266_Wifi_Matrix_Clock
A Esp8266 wifi matrix clock 

看不到图自行翻墙或查看Pics目录里的图  

固件上传方法:   
how to upload firmware:  
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

如果你没有DS18B20模块 可以自己接一个4k7上拉电阻(If you only have DS18B20(not module), you can add a 4k7 pull-up resistant)  
![wire1.png](https://github.com/yuan910715/Esp8266_Wifi_Matrix_Clock/blob/master/Pics/wire.png?raw=true)
