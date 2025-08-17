# Flicker 🔦
### An RF Geolocation Obfuscation Tool
*(Originally made for OpenWRT Linux / WiFi Pineapples)*
---
**Ever feel like you're being watched?  
In the digital world, you most likely are.**  

Your wireless devices are constantly broadcasting signals.  
To a determined adversary, these signals are like a trail of breadcrumbs leading directly to your physical location, work, school, home, or even friends.  

***Flicker*** is a lightweight, but still a powerful tool designed to turn that trail into a storm of misinformation and obfuscation when broadcasting packets, making it alot harder to track the device it's being ran on.  
It was actually specfifically written to be run on the WiFi Pineapple MKVII, made by Hak5. To make it even harder to detect where it's traffic comes from. And it works perfectly on the Pineapple. Which i have tested myself.

---

## What is Flicker?

***Flicker*** is my own work. I wrote in a day (10.th August 2025).  
- It's a 100% POSIX-compliant shell script that makes your wireless device(s) a ghost in the machine.  
- It runs on OpenWrt-based systems *(like the Hak5 WiFi Pineapples)* and continuously randomizes your device's radio frequency *(RF)* signature.  
- By rapidly and randomly changing the selected interfaces **transmit power** as well as other low-level settings **MAC timing parameters**, ***Flicker*** introduces two random layers of chaos that *"corrupts/obfuscates"* the data used by normal geolocation trackers.  
- It doesn't just hide your signal; it actively pollutes the surveillance environment, making you a hard target to pin down.  

*Think of it like this: if a standard Wi-Fi signal is a steady lighthouse beacon, ***Flicker*** turns your signal into a thousand flickering candles in a hurricane.*

---

## The Problem: The Invisible Fingerprint

Every packet your device sends can be measured by a listener.  
By analyzing the signal strength *(RSSI)* from multiple points, an adversary can triangulate your position with surprising accuracy.  
This technique, known as *"RF-fingerprinting"*, requires absolutely no interaction from youm it's totallt passive, and can be done with commodity hardware.  
It's a silent, 100% legal, passive method of surveillance. Which anyone can perform.  

***Flicker*** is the countermeasure. It's designed to be a simple, but still very effective wrench in the gears of these tracking systems!

---

## Features

* **Dynamic TX Power Modulation**: The core of ***Flicker***. It randomizes your device's transmit power at totally unpredictable intervals.  
* **Advanced Timing Obfuscation**: An optional advanced mode *(`-A`)* randomizes the *`Coverage Class`*, altering low-level timing parameters to defeat more sophisticated fingerprinting, by applying extra layers of obfuscation.  
* **Highly Configurable**: Control all parameters via command-line arguments or a simple configuration file located at *`/etc/flicker/config.txt`*.  
* **POSIX Compliant**: Built for `ash` and other minimalist shells. No `bash` required.  
* **Lightweight & Low-Overhead**: Designed to run efficiently on embedded devices like the Hak5 WiFi Pineapple MK7 without impacting it's overall performance at all.  
* **Safe & Ephemeral**: Changes are made to the live system state and do not persist after a reboot. The script also includes a cleanup routine to restore your original settings on exit.  ***XXX***: *I will consider adding a option for reboot persistence in the future.

---

## Getting Started

***Flicke***r is designed for simplicity.

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/adde88/flicker.git](https://github.com/adde88/flicker.git)
    cd flicker
    ```

2.  **Copy to your Device:**
    Use `scp` to copy the ***`flicker`*** script and the *`config.txt`* file to your OpenWrt device (e.g., into `/root/`).
    ```bash
    scp flicker config.txt root@172.16.42.1:/root/
    ```

3.  **Make it Executable:**
    Log in to your device and make the script executable.
    ```bash
    chmod +x /root/flicker
    ```

4.  **First Run & Configuration:**
    The first time you run ***Flicker***, it will automatically copy *`config.txt`* to *`/etc/flicker/config.txt`*.
    ```bash
    /root/flicker wlan0
    ```
    *(Use `Ctrl+C` to stop it for now)*. You can now edit the defaults in *`/etc/flicker/config.txt`* to your liking.

---

## Usage

Flicker is controlled via command-line arguments, which will always take priority over the settings in *`config.txt`.*

**Basic Usage *(uses settings from the config file)*:**
```bash
./flicker
```

**Specify an Interface:**
```bash
./flicker wlan1
```

**Enable Advanced Mode and set a lower sleep time:**
```bash
./flicker -A -s 5 wlan0
```

### Command-Line Options

| Flag | Long Flag | Description |
| :--- | :--- | :--- |
| `[interface]` | | Target interface (e.g., `wlan0`). Overrides config file. |
| `-h` | `--help` | Show the help menu. |
| `-A` | `--advanced` | Enable Advanced Obfuscation mode (randomizes Coverage Class). |
| `-p <dBm>` | `--min-power <dBm>` | Minimum TX power to use. |
| `-s <sec>` | `--base-sleep <sec>` | Base sleep duration in seconds. |
| `-v <%>` | `--variation <%>` | Sleep time variation percentage. |
| `-c <num>` | `--coverage <num>` | Maximum Coverage Class for Advanced mode. |

---

## We Need You!

This is a community-driven project. The best way to make ***Flicker*** better is to use it and report back.

* **Found a bug?** Sweet! Open an issue.
* **Have an idea for a new feature?** Start a discussion! :)
* **Want to contribute?** Fork the repo and submit a pull request. ;)

Your feedbacks is extremely valuable and appreciated in the ongoing effort to build better and better tools for privacy and security.

---

## License

***Flicker*** is licensed under the **Creative Commons Attribution Non-Commercial ShareAlike 4.0 International License**.

You are free to share and adapt this work for non-commercial purposes, as long as you give appropriate credit to its author and distribute your contributions under the same license.

---

### Support This Project
If you find this project helpful, please consider supporting its continued development:
- **Bitcoin**: `bc1qnamkw2g3n9w4v5lejn8rlw000g2mqpdca9vk04`

*Your support helps keep this project maintained and improved. Thank you!*
