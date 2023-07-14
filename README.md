# -Memo-ESP32-S3-n16r8_Screen_Test
记录使用EPS32-S3-DevKitC-1与ILI9341作为显示驱动，XPT2046作为触控驱动的tft显示屏使用方法。亦可参考[此处](https://blog.csdn.net/zgj_online/article/details/104992395)

# 驱动库
bodmer/TFT_eSPI@^2.5.30  
impulseadventure/GUIslice@^0.17.0

# 步骤
**配置TFT_eSPI驱动**  
1. 修改`.pio\libdeps\esp32-s3-devkitc-1\TFT_eSPI\User_Setup.h`配置，一些引脚不如预期那样可用，可参考`.pio\libdeps\esp32-s3-devkitc-1\TFT_eSPI\User_Setup_Select.h`文件内头文件定义，如`<User_Setups/Setup70b_ESP32_S3_ILI9341.h>`
2. 测试，推荐测试文件`.pio\libdeps\esp32-s3-devkitc-1\TFT_eSPI\examples\320 x 240\Keypad_240x320\Keypad_240x320.ino`，可直接复制到`src`中，不必再声明文件尾定义的函数
  
**配置GUIslice驱动**  
1. 取消`.pio\libdeps\esp32-s3-devkitc-1\GUIslice\src\GUIslice_config.h`内相应配置文件注释，`"../configs/esp-tftespi-default-xpt2046_int.h"`是配合带XPT2046触控的TFT_eSPI驱动的配置文件，不带`_int`的为单独触控驱动。
2. 测试文件`.pio\libdeps\esp32-s3-devkitc-1\GUIslice\examples\arduino\diag_ard_touch_calib\diag_ard_touch_calib.ino`
3. 根据测试结果修改配置文件`.pio\libdeps\esp32-s3-devkitc-1\GUIslice\configs\esp-tftespi-default-xpt2046_int.h`内的  
    `#define ADATOUCH_X_MIN    198`  
    `#define ADATOUCH_X_MAX    3871`  
    `#define ADATOUCH_Y_MIN    3871`  
    `#define ADATOUCH_Y_MAX    338`  
    
# 备注
1. 使用GUIslice Builder，Text需要设置External Storage Size，否则gslc_ElemSetTxtStr函数不起作用

# 屏幕接线
| 屏幕引脚 | ESP32引脚 |
| --- | --- |
|T_IRQ|7|
|T_DO|13|
|T_DIN|11|
|T_CS|16|
|T_CLK|12|
|SDO\<MISO\>|13|
|LED|3V3|
|SCK|12|
|SDI\<MOSI\>|11|
|DC|7|
|RESET|6|
|CS|10|
|GND|GND|
|VCC|3V3|

# 测试
screen_test.zip内的头文件与主文件直接放入src文件夹
<iframe width="854" height="480" src="https://github.com/minquejoe/-Memo-ESP32-S3-n16r8_Screen_Test/blob/main/screen_test.mp4" frameborder="0" allowfullscreen></iframe>
