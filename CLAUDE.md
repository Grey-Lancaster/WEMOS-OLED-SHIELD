# CLAUDE.md

WEMOS-OLED-SHIELD: a PlatformIO project for the Wemos (LOLIN) D1 mini with the 64x48 OLED shield. The point of the repo is the `platformio.ini`, which pulls the special SSD1306 library fork the shield needs, plus Adafruit's demo sketch to prove it works. Public repo.

## Layout
- `platformio.ini` - env `d1_mini` (ESP8266, Arduino). Libraries: `adafruit/Adafruit GFX Library@^1.11.9` and the `stblassitude/Adafruit_SSD1306_Wemos_OLED` fork from GitHub (the stock Adafruit SSD1306 library does not support this 64x48 panel).
- `src/OLED_SHIELD.ino` - Adafruit's SSD1306 example adapted for the shield (about 380 lines of drawing demos). Display is created with `Adafruit_SSD1306 display(OLED_RESET)`, reset on GPIO0, I2C address `0x3C`, SCL on GPIO5 and SDA on GPIO4 per the sketch comments. It has a compile-time check that the library's configured display height is right.
- `README.md` (two lines), `LICENSE` (GNU GPL v3).

## Build / flash
- `pio run -t upload`, then `pio device monitor`. I found no tests and no CI.

## Gotchas
- Do not replace the library fork with the stock `Adafruit SSD1306`; the display size is configured inside the fork's header (the sketch errors out at compile time if the height is wrong).
- The sketch carries Adafruit's license/attribution header; keep it when editing.

## Deploy
- Push to `main`. There are no tags, releases or workflows.
