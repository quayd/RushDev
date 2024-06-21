## RushDev Version 0.10.0
Usage: rushdev [OPTIONS]

You can use the --help or --ftdi-cmd="help PRIMARY_COMMAND" for a full lsit of application details. However, here is a document containing infomration about more essential comamnds and examples.

## FTDI Device Commands
Dictates the type of ftdi-cmd command to be run.
Multiple instances of --ftdi-cmd can be called in sequence.

--ftdi-cmd=VALUE      
    monitor\
    load\
    verify\
    ramp

| FTDI CMD Commands | Command Type      | Field Type | Description                               | Example                   |
|-------------------|:-----------------:|:----------:|-------------------------------------------|---------------------------|
| -a                | load              |            |                                           |                           |
| --action=VALUE    | load              | String     |                                           | quit,                     |
| -d                | monitor           | DNA        | Device Identifier to pass                 | 400200000328000000011111  |
| -f                | load              | File       | Bitstream file. Can pass multiple instances to load in sequence.      | top.bit  |
| -p                | monitor           | Integer    |                                           | 350                       |
| --max-clock=X     | verify            | Integer    | Maximum clock value                       | 350                       |
| -t                | monitor, ramp     | Integer    | Amount of time in milliseconds            | 12000 = 12 seconds        |
| --unit-count=X    | monitor           | Integer    | Number of units to be acted upon          | 1                         |
| -v                | monitor           | String     |                                           | user                      |
| -x                | monitor           | Integer    |                                           | user                      |

--ftdi-cmd="monitor -t 5500 -p 350 -d 400200000328000000011111 --unit-count=1 -v user"

#### Load Example:
--ftdi-cmd="load -f bitstreams/ECU50/GRAM_ECU50_Top_A2.bit -d 400200000328000000011111"

--ftdi-cmd="load -f bitstreams/ECU50/GRAM_ECU50_Top_A2.bit -f bitstreams/ECU50/Z1.bit -f bitstreams/ECU50/Z2.bit -f bitstreams/ECU50/Z3.bit -f bitstreams/ECU50/Z4.bit  -a"

Load a set of BCU's and a set of C1100 in one script:
--ftdi-cmd="load -f bcu_top.bit -f bcu_partial1.bit -d serial_BCU1 -d serial_BCU2" --ftdi-cmd="load -f C1100_top.bit -f C1100_partial1.bit -d serial_C1100-1 -d serial_C1100-2"

#### Verify Example:
--ftdi-cmd="verify --max-clock=35 --action=quit"

#### Ramp Example:
--ftdi-cmd="ramp -t 10"

### FTDI Device Initialization
Dictates which form of communication to initialize with the device

--ftdi-init=VALUE\
    uart

## Logging
Which way logs will be displayed

--log-level=VALUE   
    warn\
    trace

## UI Display
Which display will be selected

--no-ui - no user interaction, useful for quick commands or scripting.\
--key-input - for the most part is a no-UI mode, allowing scripting, but also acts as a terminal for sending multiple operations and requesting help on features press `?`.\
--tui - ** disabled momentarily ** provides a text user interface with scrolling, multi-page views, and status bars.      
