# GM300 tool in DOSBox in a container

This is the easiest way to program your Motorola Radius in Linux.

Here we have put together the work by [Jacek Ozimek](https://sourceforge.net/p/dosbox/patches/288/), [KK6JYT](https://kk6jyt.com/motorola-radius-gm300-programming/) and others in a ready-to-use container that you can just run!


## Use a RIB to connect your radio to your PC

If you don't already have a RIB, we recommend following the [schematics by VR2ZHU](http://www.hkra.org/homebrew/rib/Rib.html) to reproduce the original Motorola RLN4008B RIB.

Below is my RIB which looks like it came straight from an ugly DIY projects contest.

![](fig/rib.jpg)

Alternatively, you can use off-the-shelf equipment as mentioned below.

Tested RIBs:

- [RLN4008B Programming Interface Box RIB For Motorola](https://www.ebay.com/itm/365265881999)
  - [UL Listed 9V AC Power Adapter](https://www.amazon.com/dp/B06Y1LF8T5)

Tested Programming Cables (need RIB):

- [Programming Cable Motorola Radius Maxtrac GM300 M1225 CDM CDM1250 CM200 CM300](https://www.ebay.com/itm/350585751560)

Tested USB/Serial Adapters:

- [TRENDnet USB to Serial 9-Pin Converter Cable, TU-S9](https://www.amazon.com/dp/B0007T27H8/)

**Note:** Under Linux, USB/Serial adapters with the Prolific chipset work just fine for programming your radio. You do not necessarily need an adapter with an FTDI chipset.

## Make sure your user can access /dev/ttyUSB0

Depending on your Linux distro, you might have to add yourself to the `uucp` or `dialout` groups.

On Debian/Ubuntu, this would be done with:

```
sudo usermod -aG dialout $USER
exec su -l $USER
```

Depending on your distro you may have better results logging out with `exit` and logging back in or simply rebooting with `sudo reboot now`.

If you get yourself in despair and want a quick hack, you may just `chmod 0666 /dev/ttyUSB0`.


## Run the container

Just clone this repository and call `./run.sh`.

On Debian/Ubuntu, you first need to install `git` and `docker`, then add yourself to the `docker` group:

```
sudo update && sudo apt install docker-compose git
sudo usermod -aG docker $USER
exec su -l $USER
```

Then clone the repository, change to the directory, and run the script:

```
git clone https://github.com/thotypous/gm300-dosbox.git
cd gm300-dosbox
./run.sh
```

If you don't see DOSBox boot up, your user may not have access to the `X` server.  
Here is a command that allows local users on the machine access:

```
xhost local:
```

You can then try running `./run.sh` again.


## Follow the steps

![](fig/screen1.png)

1. Press any key.

![](fig/screen2.png)

2. Press F3 to enter the `GET/SAVE Codeplug Data` menu.

![](fig/screen3.png)

3. Press F2 to `READ Radio`.

![](fig/screen4.png)

4. Wait some instants while radio codeplug is read.

   Press F10 to go back to the `MAIN Menu`. Then, press F4 to enter the `CHANGE/VIEW Codeplug Data` menu.

![](fig/screen5.png)

5. Press F5 to go to `MODE Configuration: Frequency, Squelch Type and Codes`.

![](fig/screen6.png)

6. Change the settings as desired. Navigate using Tab and F3/F4.

   When programming ham radio frequencies, you may receive the error `Valid Range is: 146.0 to 174.0`. Override the check by pressing Shift when entering numbers. Enter the decimal point as usual (no Shift when entering `.`) and take care to fill the entire field (pad with zeros, i.e. `)`, to the right if needed). See the figure above for an example.

![](fig/screen7.png)

7. Press F2 if you receive a warning.

![](fig/screen8.png)

8. Press F10 twice to return to the `Main Menu`. Then, press F3 to enter the `GET/SAVE Codeplug Data` menu.

   Finally, press F8 to `PROGRAM Radio` and F2 to confirm.

![](fig/screen9.png)

9. Wait some instants while radio codeplug is programmed and have fun.


## Acknowledgments

Thanks to all the friends from QRM-BR!
