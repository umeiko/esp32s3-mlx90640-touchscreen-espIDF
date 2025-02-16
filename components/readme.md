### 将`Arduino`侧载为IDF的组件

#### 1.3 安装 Arduino依赖

在 `./components`文件夹中，将[arduino仓库的zip文件](https://github.com/espressif/arduino-esp32/archive/refs/tags/2.0.17.zip)下载到这里，并且重命名文件夹为`arduino`

#### 1.4 配置工程

在`ESP-IDF终端` (如果你是VScode IDE，在底部的工具栏中可以找到) 中输入命令

```bash
idf.py menuconfig
```

在`Arduino Configuration  --->`中配置:

```json
[*] Autostart Arduino setup and loop on boot
```


### 将`TFT-eSPI`侧载为IDF的组件

#### 1.5 克隆`TFT-eSPI`库

在终端中输入命令

```bash
cd components
git clone https://github.com/Bodmer/TFT_eSPI.git
cd TFT_eSPI
cp Kconfig Kconfig.projbuild 
cd ..
idf.py menuconfig
```
在`TFT_eSPI  --->`中配置正确的屏幕参数,以这些为参考:

`TFT_eSPI  ---> `
```C
Select TFT driver (ST7789 - 1)  --->
Define the colour order (RGB)  --->
(240) LCD pixel width in portrait orientation
(280) LCD pixel height in portrait orientation
Color inversion correction (None)  --->
LCD Interface (SPI)  --->
Display SPI config  --->
Control Pin configuration  --->
Fonts  --->
Touch screen configuration  ---> 
Other settings  --->
```

`Display SPI config  --->`
```json
SPI port (HSPI (SPI3))
(-1) TFT MISO pin              
(4) TFT MOSI pin
(3) TFT Clock pin              
[ ] Use SDA line for reading       
(27000000) SPI Frequency (Hz)
(20000000) SPI Read Frequency (Hz)
```

`Control Pin configuration  --->`
```json
(2) TFT Chip Select pin
(1) TFT Data/Command pin
(5) TFT Reset pin
[ ] Enable backlight control
```