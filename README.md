# Microchip FPGA Tools Installation Guide

Instructions for installing the Microchip FPGA tools on a Ubuntu 20.04 desktop.

These installation steps should take less than one six-pack and 5 bags of crisps to complete. If you finish the six-pack before seeing Libero asking if you want it to check for updates, try some other day. You either missed a step or cannot hold your drink. If you complete the installation before finishing your first bottle then you definitively do not drink fast enough.

## Install Libero 2022.3
- Download installer from the Microchip website. [Link](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/fpga/libero-software-later-versions) at time of writing this.
- Install Libero

```
unzip Libero_SoC_v2022.3_lin.zip
cd Libero_SoC_v2022.3_lin/
./launch_installer.sh
```


  - Do not use the default location suggested by the Libero installer

    - Instead of /usr/local/Microchip/Libero_SoC_v2022.3 install into ~/Microchip/Libero_SoC_v2022.3

- Run the post installation script which will install missing packages:

```
sudo /home/<USER-NAME>/Microchip/Libero_SoC_v2022.3/Logs/req_to_install.sh
```
No need to run the FlashPro hardware installation scripts. This will be taken care of as part of the SoftConsole installation.

## Install SoftConsole 2022.2

- Download intaller from Microchip website. [Link](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/soc-fpga/softconsole) at time of writing.

```
sudo chmod +x Microchip-SoftConsole-v2022.2-RISC-V-747-linux-x64-installer.run

./Microchip-SoftConsole-v2022.2-RISC-V-747-linux-x64-installer.run
```
Accept the license, Click Forward, Finish.

Perform the post installation steps as described in the html file opened when you click Finish.


Please pay special attention to the "Enabling non-root user to access FlashPro" section of the post-installation instructions. This will actually allow you to program the board using Libero.

## Install the Libero licensing daemon

Download the 64 bit Licensing Daemons from the Microchip website. It is somewhere on this page, I promise: https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/fpga/licensing#

Tired of playing "Where's Wally": This [link](http://ww1.microchip.com/downloads/aemdocuments/documents/fpga/media-content/FPGA/daemons/Linux_Licensing_Daemon_11.16.1_64-bit.tar.gz) might work. Yes, your browser might complain about the http instead of https but it is the same link if you win at Where's Wally.

Copy the downloaded file to the Microchip directory within your home directory and untar it.
```
cd ~/Microchip
tar -xvf Linux_Licensing_Daemon_11.16.1_64-bit.tar.gz
```
Install the Linux Standard Base:
```
sudo apt-get update
sudo apt-get -y install lsb
```

## Request a Libero Silver license

- Another round of Where's Wally on that page: www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/fpga/licensing
  - hint: search for "free license"

- Welcome to MicrochipDirect! Register or login.
- There's a good chance you will need to go back to click on "free license" on the Microchip page. Mileage varies on this one.
- Back into MicrochipDirect? Click "Request Free License" and choose "Libero Silver 1Yr Floating License for Windows/Linux Server" from the list.
- Enter you MAC address and click register
  - A MAC address looks something like 12:34:56::78:ab:cd when you use the "ip address" command to find out its value on your Linux machine. However, you need to enter it as 123456abcd in this dialog box. Would be too easy to just copy the output from the ip address command. Why miss an opportunity to introduce a typo?

You will get an email with a license.dat file. Copy it into the ~/Microchip/license directory. Edit the License.dat file to replace the <put.hostname.here> string with... localhost.

## Download tool setup script

```
git clone https://github.com/vauban353/Microchip-FPGA-Tools-Setup.git
```
Source the script:
```
. ./setup-microchip-tools.sh
```
Do not forget the leading dot. It matters. You will need to run this every time you restart your machine.

You can then start Libero to open an existing Libero project.
```
libero
```

However you will more than likely want to use Libero to run a TCL script that will build a design for you.
```
libero SCRIPT:BUILD_A_DESIGN.tcl
```
