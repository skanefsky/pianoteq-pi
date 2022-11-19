# pianoteq-sff

> Script to install and run [Pianoteq](https://pianoteq.com/) in a headless configuration (i.e. no keyboard/monitor/mouse) on small-form-factor (SFF) computers running Raspberry Pi OS or Ubuntu MATE (other distributions may work but have not been tested).

> Based on youfou's pianoteq-pi with updates to support the current release of Raspberry Pi OS (as of November 2022) and new support for Ubuntu MATE.

## How to use

1a. Install your preferred Linux distribution:
   - [Raspberry Pi OS (64 bit) with desktop](https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-64-bit) for Raspberry Pi.
   - [Ubuntu MATE (64-bit)](https://ubuntu-mate.org/download/) for Raspberry Pi or other SFF computer such as [MeLE Quieter3C](https://ww.amazon.com/gp/product/B0B765VF84)
   - 
3. Download Pianoteq from [the official website](https://pianoteq.com/) onto your SFF (either demo or licensed copy will work).
4. Run the following command in the same folder of the 7z/zip package:
```shell
wget -qO setup.py https://git.io/JqVD6 && sudo python3 setup.py
```
Simple as that.

After installed in this way, Pianoteq will run headlessly (No GUI, to get better performance) on every system boot.
If you want to adjust something on it, just double click the desktop icon to open GUI.

## What this script actually does?

1. Installs dependencies:
   - `p7zip-full` - to extract the Pianoteq 7z/zip package
   - `cpufrequtils` - to improve CPU performance while running Pianoteq
   - lowlatency linux kernel for better performance (optional, Ubuntu only)
2. Extracts the Pianoteq 7z/zip package in your preferred location.
3. Creates a service to set the CPU to performance mode at boot time.
7. Creates a system service to run Pianoteq headlessly at boot time.
4. Creates a `start.sh` script under the Pianoteq folder which:
  - stops the headless Pianoteq service
  - runs Pianoteq in GUI mode to make changes or use interactively
  - restarts the headless Pianoteq service when you quit the GUI.
6. Creates a desktop entry for Pianoteq, so you can open the GUI easily by clicking the icon
8. Set a default resolution so that you can run Pianoteq while not connecting to a display
9. Overclocks the CPU to 2000 MHz at the 6th voltage level to get better performance as well (Raspberry Pi OS only)
10. Disables smsc95xx.turbo_mode as Pianoteq officially advised (Raspberry Pi OS only)
11. Installs x11vnc server and openssh-server for remote access when running headless (optional, Ubuntu only)
13. Modifies the "account limits" as Pianoteq officially advised
14. Checks if you have already installed Pianoteq and can re-install or uninstall it if you want
