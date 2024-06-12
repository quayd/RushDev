# RushDev

FPGA Utility

### Disclaimer

This tool is a work in progress and intends to make it safer and easier to troubleshoot your devices however it can be used to do things you shouldn't! It is up to you to know how your devices work and what operations are not safe for them.

## Latest Release
You can find the latest release [here](https://github.com/quayd/RushDev/releases/latest)

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
 

## OS Compatibility

| Operating System  | Functionality |
|-------------------|:-------------:|
| Ubuntu 16.04      | Y             |
| Ubuntu 18.04      | Y             |
| Ubuntu 20.04      | Y             |
| Ubuntu 22.04      | Y             |
| Windows 10        | N             |
| Windows 11        | N             |

* Ubuntu subversions in between main .04 releases are untested
* HiveOS and MMPOS run off of Ubuntu 18.04, 20.04 or 22.04 depending on version. In theory they should work but are not yet confirmed.
* Windows version coming shortly.

## Device Compatability

Currently, thorough testing has only occurred with the Osprey ECU50. Some testing has taken place for C1100, BCU 1525, FK33, TH53 and CVP-13.

Additional FPGA's may function but testing is required. The following compatability list is a rough instance based on current community testing.

List of Devices and Primary Function Compatability

| Unit XCVU33P                  | Bitstream Loading | Voltage Control | 
|-------------------------------|:-----------------:|:---------------:|
| Squirrel Forest Kitten FK33   |         Y*        |        Y*       |
| TUL TH53                      |         Y         |        Y*       |
| TUL TH53M                     |         Y*        |        Y*       |
| Osprey E333                   |         Y         |        N        |
| Osprey E333C                  |         Y*        |        N        |

| Unit XCVU35P                  | Bitstream Loading | Voltage Control | 
|-------------------------------|:-----------------:|:---------------:|
| AMD Alveo U50C                |         Y         |        Y*       |
| AMD Varium C1100              |         Y         |        Y*       |
| TUL TH55                      |         Y*        |        Y*       | 
| Squirrel Jungle Cat JC35      |         Y*        |        Y*       | 
| Osprey ECU50                  |         Y         |        Y*       | 
| Osprey E335                   |         Y         |        N        | 
| Osprey E335C                  |         Y*        |        N        | 

| Unit XCVU9P                   | Bitstream Loading | Voltage Control | 
|-------------------------------|:-----------------:|:---------------:|
| AMD VCU1525                   |         Y*        |        N        | 
| AMD Alveo U200                |         Y*        |        N        | 
| AMD XBB1525                   |         N         |        N        | 
| TUL BTU9P                     |         Y*        |        N        | 
| TUL BTU9P-Pro                 |         Y*        |        N        | 
| Squirrel BCU1525              |         Y         |        N        |
| Bittware XUP VV8              |         N         |        N        | 
| Osprey ECU200                 |         Y*        |        N        | 
| Osprey E309                   |         Y         |        N        | 

| Unit XCVU13P                  | Bitstream Loading | Voltage Control | 
|-------------------------------|:-----------------:|:---------------:|
| Bittware CVP13                |         Y*        |        N        |
| Bittware XUP VV8              |         N         |        N        | 
| Squirrel Jungle Cat JC13      |         Y*        |        N        | 
| Osprey E313                   |         N         |        N        | 

Voltage Control *: Currently uses TeamRedMiner to Bootstrap Settings

Bitstream Loading *: Currently only loads portion of bitstream or loads inconsistently

#### Osprey E300 Series Unit Disclaimers:
- No Osprey Units will possess Voltage Control as each unit has it built in
- Bitstream Loading and Support are typically dependant on the Osprey Team implementing. However, in theory code could be directly run through SSH or similar connections.

#### XCVU13P Disclaimers:
- The CVP-13 only partially works due to different UARTS for JTAG and FPGA Communications (to be fixed shortly).
- Additional XCVU13P chip units are predominantly untested.

#### XUP VV8 Disclaimers:
- No current or planned support but listed because they are hardware viable and may be some degree of compatible but untested.
- The XUP VV8 has numerous variants depending on Chip Type (XCVU9P, XCVU13P) and Chip Grades (2, 3, S)

## Usage

Refer to [USAGE.md](USAGE.md) for a full list of options and commands.
  
Scripts in the zip file demonstrate common operations and there is terminal utility built-in that can be accessed with the command line option --key-input or running the term.sh script. Some of the features in the terminal are undocumented at the moment. 

The terminal allows you to do operations that in certain states may be dangerous for your device. Please, be very aware of what you are doing. Using 'M" a lot to quickly get a monitored assessment of your clock speed and temperature can aid in understanding the state of your device.

### Terminal Operations:
- pressing 'e' will take you to the Custom Command edit box where you can enter any command that you could have supplied in the scripts with `--ftdi-cmd`. Type `help` to see a list of command and ex. `help load` to see the help for a specific command.
- pressing 'm' will open an edit box that lets you monitor FPGA communication and is just a short-cut allowing you to skip typing `monitor -t`. You can directly just type how many ms you want to monitor for and any other options you wish, that can be found in the above Custom Command help section or taken from script examples.
- pressing 'l' will open an edit box that lets you load bitstreams. Again it is a short-cut for `load -f` so you can directly type a filename and any other options you wish, that can be found in the above Custom Command help section or taken from the script examples. ex `top.bit -f K1.bit -f K2.bit`
  
Lots more work to go but it might be useful for some of you as a start. 

### FK33 / TH53 / TH53M and potentially TH55 Notes:
These units won't detect DNA until a valid bitstream is detected, so any `-d <device>` options will require the serial number instead to get the expected results.

### CVP-13 Specific Notes
For the CVP there are two FTDI devices. If you run RushDev once with no command line options or the `term.sh` script it will show you whether your CVP is detected, which FTDI device JTAG was found on, and it will show another FTDI device on another serial number. Take note of this other device serial number. This second FTDI device is the one the bitstream communicates to, not the JTAG one. The JTAG FTDI is used for detecting the device if no bitstream is loaded, getting the basic temperature and DNA, and loading the bitstream. The other FTDI device is used for ramping up/down and actual mining. 

With the second FTDI serial number, now change the script `load-full.sh` to use the specified serial number with the `-d <your_cvp_serial>` option instead of `-a`
example: `sudo ./rushdev --log-level=warn --no-ui --ftdi-cmd="monitor -t 5500 -p 350 --unit-count=1 -v user" --ftdi-cmd="verify --max-clock=35 --action=quit" --ftdi-cmd="load -f GRAM20_ECU50_Top_A2.bit -f Z1.bit -f Z2.bit -f Z3.bit -f Z4.bit -d <your_cvp_second_serial_number" --ftdi-cmd="monitor -t 5500 -p 350 --unit-count=1 -v user"`

### Voltage Control
There is a script `set-volt6.sh` which will run rushdev to set the voltage on all devices or you can modify the script and change `-a` to `-d <dna/serial number>` one or more times to set the voltage for specific devices. Voltage control requires the utility `changeVoltage` and the `bits` folder from other miner releases to be put in a sub-folder `util`. Inquire on Discord channel for assistance.

# Feedback
It will be helpful to receive logs from devices not listed above running the various RushDev scripts with the option `--log-level=trace`.
Some features are not yet working fully. No need to report text user interfaces issues at the moment, as most are known.
Primarily, helpful issues would be reports of errors, devices not responding properly, or other unexpected results. Please submit these as a new Issue [here](https://github.com/quayd/RushDev/issues)

