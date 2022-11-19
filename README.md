# pianoteq-sff

> Script to install and run [Pianoteq](https://pianoteq.com/) in a headless configuration (i.e. no keyboard/monitor/mouse) on small-form-factor (SFF) computers running Raspberry Pi OS or Ubuntu MATE (other distributions may work but have not been tested).

> Based on youfou's pianoteq-pi with updates to support the current release of Raspberry Pi OS (as of November 2022) and new support for Ubuntu MATE.

## How to use

1a. Install your preferred Linux distribution:
   - [Raspberry Pi OS (64 bit)](https://downloads.raspberrypi.org/raspios_arm64/images/)) for Raspberry Pi.
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
2. Extracts the Pianoteq 7z/zip package to `/home/pi/`
3. Creates a `start.sh` script under the Pianoteq folder, and it:
   - sets CPUs to "Performance" mode while running Pianoteq
   - runs Pianoteq as a GUI program or headlessly for better performance 
   - sets CPUs to "On Demand" mode when quit Pianoteq
4. Creates a desktop entry for Pianoteq, so you can open it easily by clicking the icon
5. Creates a system service to run Pianoteq headlessly every time the system startups
6. Set a default resolution so that you can run Pianoteq while not connecting to a display
7. Overclocks the CPU to 2000 MHz at the 6th voltage level to get better performance as well
8. Disables smsc95xx.turbo_mode as Pianoteq officially advised
9. Modifies the "account limits" as Pianoteq officially advised
10. Checks if you have already installed Pianoteq and can re-install or uninstall it if you want

## FAQ

1. `Q` Why use the Beta version of Raspberry Pi OS (64 bit) instead of the stable 32 bit version, or Ubuntu Mate (64 bit)?
    - `A` 64 bit allows for better performance, and Raspberry Pi OS comes with VNC Server, which saves a lot of work.
2. `Q` Is Pianoteq playable on it?
    - `A` Sure it is. I get a Performance Index of 32 on it. The internal sample rate set to 24000 Hz, and max polyphony is set to 128. No crackles or dropouts. Playing is quite enjoyable.
3. `Q` Can I try this on other machines / OS version?
    - `A` Not recommended. I haven't tested it on other machines or OS versions.
