# ESP32 SuperMini C5 + SSD1306 OLED – Smart Web Display

A small MicroPython project for the **ESP32 SuperMini C5** with an **SSD1306 OLED display (128×64)**, controllable via a **smart webpage in your browser**. The display shows various effects – and can easily be extended with your own effects at any time!

---

## 📸 Features

- 🌐 Webserver running directly on the ESP32 – no cloud service needed
- 🎨 Multiple display effects selectable via browser
- ➕ Easily extendable – just add your own effects
- 📡 Connects to your local WiFi (enter SSID & password once)
- 🔌 Everything written in MicroPython

---

## 🗂️ Project Structure

```
📦 esp32-oled-webdisplay/
 ┣ 📄 main.py          → Main file: WiFi, webserver, effects & routing
 ┣ 📄 boot.py          → Boot file: WiFi setup & important initializations
 ┗ 📄 ssd1306.py       → Driver for the SSD1306 OLED display (I2C)
```

---

## 🔧 Hardware

| Component | Details |
|---|---|
| Microcontroller | ESP32 SuperMini C5 |
| Display | SSD1306 OLED 128×64 (I2C) |
| Display connection | SDA → GPIO 21, SCL → GPIO 22 |
| Power supply | USB or 3.3V |

> **Note:** I2C pins may vary depending on your ESP32 variant. Adjust in `main.py` if needed.

---

## ⚡ Quick Start

### 1. Enter your WiFi credentials

Open `main.py` and fill in your WiFi details at the very top:

```python
# ⚠️ CHANGE THIS ⚠️
SSID = "YOUR_WIFI"
PASSWORD = "YOUR_PASSWORD"
```

### 2. Upload files to the ESP32

Using **Thonny** or **mpremote**:

```bash
# With mpremote:
mpremote cp ssd1306.py :ssd1306.py
mpremote cp boot.py :boot.py
mpremote cp main.py :main.py
```

### 3. Restart the ESP32

After uploading, the ESP32 starts automatically. In the serial monitor (115200 baud) you will see the assigned IP address:

```
Connecting to WiFi...
Connected! IP: 192.168.1.42
Webserver running at http://192.168.1.42
```

### 4. Open the webpage

Open the displayed IP address in your browser (on the same WiFi network). You will see the control page with all available effects.

---

## 🎨 Available Effects

| Effect | Description |
|---|---|
| `scrolltext` | Text scrolling from right to left |
| `blink` | Text blinking on the display |
| `bounce` | Text bouncing back and forth |
| `invert` | Invert display colors (white ↔ black) |
| `static` | Clear the display |
| `custom` | Enter custom text via the webpage |

---

## ➕ Adding Your Own Effects

In `main.py` you will find the function `run_effect(name)`. Simply add a new `elif` block:

```python
elif name == "my_effect":
    # Your code here
    oled.fill(0)
    oled.text("My Effect!", 0, 28)
    oled.show()
```

And in the HTML page inside `main.py`, just add a new button:

```html
<button onclick="setEffect('my_effect')">My Effect</button>
```

That's it! After uploading, the new effect is immediately available on the webpage. 🎉

---

## 📄 File Overview

### `boot.py`
- Runs automatically first on startup
- Establishes the WiFi connection
- Initializes the I2C bus and the display
- Sets important global variables

### `main.py`
- Contains the complete webserver (simple HTTP socket server)
- Contains all effect functions
- Contains the HTML webpage (inline as a string)
- **This is where you enter your SSID and password!**

### `ssd1306.py`
- MicroPython driver for the SSD1306 OLED display
- Communicates via I2C
- Provides functions like `text()`, `fill()`, `show()`, `invert()` etc.
- Standard driver – usually does not need to be modified

---

## 🛠️ Requirements

- [MicroPython](https://micropython.org/download/ESP32_GENERIC/) flashed onto the ESP32
- [Thonny IDE](https://thonny.org/) or `mpremote` to upload the files
- ESP32 and control device (PC/phone) on the **same WiFi network**
- [SSD1306 Module](https://de.aliexpress.com/item/1005006141235306.html?spm=a2g0n.productlist.0.0.7676iowziowzI0&browser_id=dc94df19f33449258e8d8bcc6107aacb&aff_trace_key=d9be5f4a88204e37b6174669cdda15f5-1770732239441-03580-UneMJZVf&aff_platform=msite&m_page_id=ufijiggpojcaverd19c6d455bcb14a46a8691878e4&gclid=&pdp_ext_f=%7B%22order%22%3A%2219603%22%2C%22spu_best_type%22%3A%22price%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21EUR%211.75%210.99%21%21%2113.90%217.82%21%40210385bb17713597879603518e651a%2112000035944225408%21sea%21DE%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3Aafc1e24%3Bm03_new_user%3A-29895%3BpisId%3A5000000197696339&algo_pvid=e7621a90-d3f4-4475-8b27-5a958adc1496&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005006141235306%7C_p_origin_prod%3A) for showing the Effekts/Text

---

## 📝 License

MIT License – free to use and extend.

---

## 💡 Ideas for More Effects

- Clock display (with NTP time sync)
- Weather widget (via HTTP request)
- Snake game on the display
- QR code display
- Running light / LED matrix simulation
- Countdown timer

> Built a cool effect? Just add it as a pull request! 🚀