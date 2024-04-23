# RushDev v0.8.0
https://github.com/quayd/RushDev/releases/tag/v0.8.0

FPGA Utility

## ** Big disclaimer ** 
This tool is a work in progress and intends to make it safer and easier to troubleshoot your devices however it can be used to do things you shouldn't! It is up to you to know how your devices work and what operations are not safe for them.

## Description

This is a utility supporting the upcoming RushMiner.

RushDev can be used to load bitstreams and perform troubleshooting and scripting for supported FPGA's and bitstreams. 

Supported operations currently:
- Detect and identify devices
- Report device temperature and DNA
- Load Zetheron bitstreams
- Monitor UART ports for bytes over user specified time and frequency of polling
- Monitor UART ports for Zetheron bitstream packets over user specified time and frequency of polling
- Display Zetheron status packet information (temperature, voltage, clock frequency, etc.)
- Ramp up/down clock frequency
- Chain sequences of 'operations'
- Verify state of device and perform action. Current actions are simply forms of stopping further chained operations. Primary use case is to prevent loading a bitstream on a device that is already at clock setting that would be dangerous to initiate loading.
 

## Compatibility
Windows version and a version compatible with older Linux GLibC's coming shortly.

Currently, thorough testing has only occurred  with the Osprey ECU50. Some testing has taken place for C1100, BCU 1525, FK33 and CVP-13. The CVP-13 only partially works due to different UARTS for JTAG and FPGA Communications (to be fixed shortly). 

RushDev most likely works with other FPGA's but requires further testing and documenting, which should come shortly.

List of devices having existing code support but untested in majority of cases:
- AMD Alveo U50C
- AMD Alveo U200
- AMD Varium C1100
- AMD VCU1525
- Bitware CVP13
- Osprey ECU50
- Osprey ECU200
- Osprey E313
- Osprey E333C
- Osprey E335C
- Squirrel BCU1525
- Squirrel Foreest Kitten FK33
- Squirrel Jungle Cat JC13
- Squirrel Jungle Cat JC35
- TUL BTU9P
- TUL BTU9P-Pro
- TUL TH53
- TUL TH53M
- TUL TH55


## Usage

RushDev has 3 modes:

1. NoUI - no user interaction, useful for quick commands or scripting.
2. KeyInput - for the most part is a no-UI mode, allowing scripting, but also acts as a terminal for sending multiple operations and requesting help on features press `?`.
3. TUI - ** disabled momentarily ** provides a text user interface with scrolling, multi-page views, and status bars.
  
Scripts in the zip file demonstrate common operations and there is terminal utility built-in that can be accessed with the command line option --key-input or running the term.sh script. Some of the features in the terminal are undocumented at the moment. 

The terminal allows you to do operations that in certain states may be dangerous for your device. Please, be very aware of what you are doing. Using 'M" a lot to quickly get a monitored assessment of your clock speed and temperature can aid in understanding the state of your device.

### The main operations in the terminal are:
- pressing 'e' will take you to the Custom Command edit box where you can enter any command that you could have supplied in the scripts with --ftdi-cmd. Type 'help' to see a list of command and ex. 'help load' to see the help for a specific command.
- pressing 'm' will open an edit box that lets you monitor FPGA communication and is just a short-cut allowing you to skip typing `monitor -t`. You can directly just type how many ms you want to monitor for and any other options you wish, that can be found in the above Custom Command help section or taken from script examples.
- pressing 'l' will open an edit box that lets you load bitstreams. Again it is a short-cut for 'load -f' so you can directly type a filename and any other options you wish, that can be found in the above Custom Command help section or taken from the script examples. ex 'top.bit -f K1.bit -f K2.bit'
  
Lots more work to go but it might be useful for some of you as a start. 

# Welcome Feedback
It will be helpful to receive logs from devices not listed above running the various RushDev scripts with the option `--log-level=trace`.
Some features are not yet working fully. No need to report text user interfaces issues at the moment, as most are known.
Primarily, helpful issues would be reports of errors, devices not responding properly, or other unexpected results. 

