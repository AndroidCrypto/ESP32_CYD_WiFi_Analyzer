# ESP32 Cheap Yellow Display (CYD) Wi-Fi analyzer

This is the accompanying repository for my article "**Use an ESP32 Cheap Yellow Device as graphical Wi-Fi Analyzer**" available here: 

For short - what is a "Cheap Yellow Display" ? This device was introduced some years ago and allowed for very fast development of projects where an ESP32, a TFT (optional Touch surface), an SD Card Reader and an RGB LED is included. The first version was equipped with a 2.8 inch large TFT display with **ILI9341** driver chip and **XPT2046** resistive Touch driver chip. Newer versions are sold with a **ST7789** display driver chip. Nowadays, the device is available with different display sizes (1.28 up to 7 inches) and driver chips, and for this project I'm using 1.9-inches variants The display has a resolution of **320 x 170** pixels in Landscape orientation. Most of the devices are driven by an ESP32 WROOM microcontroller, but I saw some others with an ESP32-S3 chip.

![Image 1](./images/esp32_cyd_1_9_inches_st7789_christmas_clock_01_600w.png)

## Source of the Christmas images

I'm using the Domino style images provided by **judge2005** in the GitHub repository **https://github.com/judge2005/EleksTubeIPS**. You will find the originals in the path "more_faces | Christmas". The original images are BMP encoded images with a size of 135 x 240 pixels, but this is far to much for our display, as I want to display the current time and date with 6 digits each. The second issue would be: how do I load the images into the sketch (SD-Card, LittleFS). I decided to use the "inline" style by converting the files in C-style header files.

![Image 2](./images/esp32_clock_face_christmas_508w.png)

For both the image size reducing and converting I used an internet service: https://mischianti.org/rgb-image-to-byte-array-converter-for-arduino-tft-displays/

Simply open each of the ten digit BMP files, set the new image size (here 80 x 142 pixels), convert the file and download it as *h file.

The are the default settings I used:

````plaintext
Settings (default):
Code format Hex 0x00
Palette mod 16bit RRRRRGGGGGGBBBBB (2byte/pixel)
Resize: use both parameters to match exact size, e.g. 80 x 142
Multi line yes
Endianness Little Endian
static yes
const yes
Data type uint16_t
PROGMEM yes
````

## Required Library
````plaintext
GFX library for Arduino Version 1.6.3
TFT_eSPI Version: 2.4.3 *1) (https://github.com/Bodmer/TFT_eSPI)

*1) In case you encounter any problems with the TFT_eSPI library you should consider to use my forked TFT_eSPI library that solved some problems, see link below
````
Forked TFT_eSPI library by AndroidCrypto: https://github.com/AndroidCrypto/TFT_eSPI

## Set up the TFT_eSPI library

Please don't forget to copy the file "*Setup809_ESP32_CYD_1721S019_170x320.h*" in the "User_Setups" folder of the TFT_eSPI library and edit the "*User_Setup_Select.h*" to include the set up.

## Development Environment
````plaintext
Arduino IDE Version 2.3.6 (Windows)
arduino-esp32 boards Version 3.2.0 (https://github.com/espressif/arduino-esp32)
Board: ESP32 Dev Module
````

