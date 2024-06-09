[tab]: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

## RushDev Version 0.10.10
Usage: rushdev [OPTIONS]

## FTDI Device Commands
Dictates the type of ftdi-cmd command to be run.
Multiple instances of --ftdi-cmd can be called in sequence.

--ftdi-cmd=VALUE      
[tab]monitor\
[tab]load\
[tab]verify\
[tab]ramp\

### FTDI Device Monitor Options
Additional information to be passed within an --ftdi-cmd command when selecting monitor type
-t                  Integer     Amount of time in milliseconds      ex: 12000 = 12 seconds
-p                  Integer
-d                  DNA         Device Identifier to pass.          ex: 400200000129b2a60c7002c5
--unit-count=X      Integer     Number of units to be acted upon
-v                  String                                          ex: user
-x                  Integer

#### Monitor Example:
--ftdi-cmd="monitor -t 5500 -p 350 -d 400200000129b2a60c7002c5 --unit-count=1 -v user"


### FTDI Device Load Options
Additional information to be passed within an --ftdi-cmd command when selecting load type
-f                  File        Bitstream .bit file piece. Can pass multiple instances to load in sequence.
-a

#### Load Example:
--ftdi-cmd="load -f bitstreams/ECU50/GRAM20_ECU50_Top_A2.bit -d 400200000129b2a60c7002c5"
--ftdi-cmd="load -f bitstreams/ECU50/GRAM20_ECU50_Top_A2.bit -f bitstreams/ECU50/Z1.bit -f bitstreams/ECU50/Z2.bit -f bitstreams/ECU50/Z3.bit -f bitstreams/ECU50/Z4.bit  -a"

### FTDI Device Verify Options
Additional information to be passed within an --ftdi-cmd command when selecting verify type
--max-clock=X       Maximum clock value, an integer
--action=VALUE      Action to take after verify is complete
    quit

#### Verify Example:
--ftdi-cmd="verify --max-clock=35 --action=quit"

### FTDI Device Ramp Options
-t                  Integer     Amount of time in milliseconds      ex: 12000 = 12 seconds

#### Ramp Example:
--ftdi-cmd="ramp -t 10"

### FTDI Device Initialization
Dictates which form of communication to initialize with the device
--ftdi-init=VALUE
    uart

## Logging
Which way logs will be displayed
--log-level=VALUE     
    warn
    trace

## UI Display
Which display will be selected
--no-ui         