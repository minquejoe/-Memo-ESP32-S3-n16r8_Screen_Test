# -Memo-ESP32-S3-n16r8_Screen_Test
记录使用EPS32-S3-DevKitC-1与ILI9341作为显示驱动，XPT2046作为触控驱动的tft显示屏使用方法。

# 驱动库
bodmer/TFT_eSPI@^2.5.30 <br>
impulseadventure/GUIslice@^0.17.0

# 步骤
**配置TFT_eSPI驱动**
1. 修改`.pio\libdeps\esp32-s3-devkitc-1\TFT_eSPI\User_Setup.h`配置，一些引脚不如预期那样可用，可参考`.pio\libdeps\esp32-s3-devkitc-1\TFT_eSPI\User_Setup_Select.h`文件内头文件定义，如`<User_Setups/Setup70b_ESP32_S3_ILI9341.h>`
2. 测试，推荐测试文件`.pio\libdeps\esp32-s3-devkitc-1\TFT_eSPI\examples\320 x 240\Keypad_240x320\Keypad_240x320.ino`，可直接复制到src中，不必再声明文件尾定义的函数
