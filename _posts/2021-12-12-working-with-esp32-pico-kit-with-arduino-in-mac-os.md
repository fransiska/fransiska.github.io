---
layout: post
title: Working with ESP32 Pico Kit with Arduino in Mac OS
---

On Macbook Pro 2016 (Mac OS Catalina), Board is `ESP32 Pico Kit`

1. Download [Arduino IDE](https://www.arduino.cc/en/software), I used 1.8.16
2. Install [CP210x VCP Mac OSX Driver](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)
    - It will ask you to allow the driver in `Security & Privacy`
3. Even before restarting I had the `/dev/cu.SLAB_USBtoUART` folder. I ended up restarting though.
4. Open Arduino IDE
5. `Arduino` -> `Preferences` -> `Additional Board Manager URLs`, set it to `https://dl.espressif.com/dl/package_esp32_index.json`
6. `Tools` -> `Board` -> `Boards Manager`, search for `ESP32` and click Install (I installed version 1.0.6)
7. `Tools` -> `Board` -> `ESP32 Arduino` -> `ESP32 Pico Kit`, also select the appropriate `Upload Speed` (115200) and `Port` (`/dev/cu.SLAB_USBtoUART`)

    <img src="esp32.png" width="70%" />

8. Test a hello world program

    ```
    void setup() {
      Serial.begin(115200);
    }
    
    void loop() {
      Serial.println("Hello World");
      delay(2000);
    }
    ```

9. Click on the top second from left icon (right arrow) to upload to ESP32. The black screen below will show how many percent has been written.
10. (This took me awhile to figure out) To see the "Hello World", click on the top right magnifier icon, or `Tools` -> `Serial Monitor`, select the Baud Rate to 115200.

### Using multiple files

<img src="arduino_ide.png" width="70%" />

Arduino Sketch is a folder, by default saved in `~/Documents/Arduino/sketch_<date>`. (I'm not really sure how it knows which is the main file, maybe by the `setup()` and `loop()` name)

We can create a function in another file in the same folder, with extension name `.ino`. Then write the function definition at the top of where we have the `setup()` and `loop()` file. It will automatically compile the file in the same folder and find the function definition.

Editing the files on Emacs will not automatically update the opened files in the IDE, but if we close the window and open it with `File` -> `Sketchbook`, it will automatically open all files inside the sketch folder.


- [[ref](https://www.hackster.io/shahizat005/getting-started-with-esp32-on-a-mac-4b3997)]

### Next thing to learn

- [Creating web server](https://randomnerdtutorials.com/esp32-web-server-arduino-ide/)
