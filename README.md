# pianoteq-sff

> Script to install and run Modartt's [Pianoteq](https://pianoteq.com/) in a headless configuration (i.e. no keyboard/monitor/mouse) on small-form-factor (SFF) computers running Raspberry Pi OS or Ubuntu MATE (other distributions may work but have not been tested).

> Based on youfou's pianoteq-pi with updates to support the current release of Raspberry Pi OS (as of November 2022) and new support for Ubuntu MATE.

## How to use

1. Install your preferred Linux distribution:
   - [Raspberry Pi OS (64 bit) with desktop](https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-64-bit) for Raspberry Pi.
   - [Ubuntu MATE (64-bit)](https://ubuntu-mate.org/download/) for Raspberry Pi or other SFF computer such as [MeLE Quieter3C](https://www.amazon.com/gp/product/B0B765VF84)
2. Download Pianoteq from [the official website](https://pianoteq.com/) onto your SFF (either demo or licensed copy will work).
3. Download the [setup script](https://raw.githubusercontent.com/skanefsky/pianoteq-sff/main/setup.py) from this project into the same directory
4. Run the setup script:
```shell
sudo python3 setup.py
```

After installed in this way, Pianoteq will run headlessly (No GUI, to get better performance) on every system boot.
If you want to adjust something on it, just double click the desktop icon to open GUI.

## What this script actually does?

- Installs Pianoteq:
  - Installs `p7zip-full` to extract the Pianoteq 7z/zip package
  - Extracts the Pianoteq 7z/zip package in your preferred location.
  - Creates a system service to run Pianoteq in the background (no GUI) at boot time.
  - Adds permissions in /etc/sudoers.d for the user to start/stop the Pianoteq service
  - Creates a desktop icon and a start.sh script for Pianoteq, so you can open the GUI easily by clicking the icon.

- Installs/Configures Performance Optimizations
  - Installs `cpufrequtils` to allow CPU performance to be configured.
  - Creates a service to set the CPU to performance mode at boot time.
  - Disables smsc95xx.turbo_mode as Pianoteq officially advised (Raspberry Pi OS only)
  - Modifies `/etc/security/limits.conf` as Modartt officially advises
  - Overclocks the CPU to 2000 MHz for get better performance (optional, Raspberry Pi OS only)
  - Installs `linux-image-lowlatency` kernel to improve performance (optional, Ubuntu only).

- Installs/Configures Remote Access:
  - Installs `x11vnc` for GUI remote access using any VNC client (optional, Ubuntu only)
  - Set remote access password for `x11vnc` (Ubuntu only)
  - Installs `openssh-server` for remote command-line access (optional, Ubuntu only)
  - Set default resolution for VNC access when no monitor is connected
  - Creates a .xprofile file to fix performance issues when accessing x11vnc server remotely over VNC (Ubuntu only)

- Checks if you have already installed Pianoteq and can re-install or uninstall it if you want
