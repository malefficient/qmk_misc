# jc-qmk-config-notes

## Quick ref:

The 'qmk' 'binary' (by default, $HOME/.local/bin/qmk) must be in your $PATH to interact with the qmk Makefile directly. This file is actually a python3 script, and the simplest way to instantiate it is to install it via pip

python3 -m pip install qmk
export PATH=$PATH:~/.local/bin
export QMK_HOME='~/qmk_firmware' # Optional, set the location for `qmk_firmware`
qmk setup  # This will clone `qmk/qmk_firmware` and optionally set up your build environment

## qmk 'config'
You can save default values (keyboard, keymap, etc) to a qmk configuration file (by default $HOME/.config/qmk/qmk.ini)

# qmk config compile.keyboard=sofle/rev1 compile.keymap=default #compiler specific arguments
qmk config user.keyboard=clueboard/66/rev4 user.keymap=default  #'global' defaults


## qmk compiling (manually) https://beta.docs.qmk.fm/cli/cli_commands
Force of habit (/developer) will cause you to call 'make XYZ' 
make sofle:default:flash
avrdude -p atmega32u4 -c avr109 -P /dev/ttyACM0 -U flash:w:.build/sofle_rev1_jc-009.hex


## qmk compiling (more friedlyly)
In lieu of manually running make sofle:default:flash (which must be done from $QMK_HOME), the 'qmk' wrapper can do this with some contextual awareness
I.e., if you are in ~/QMK_HOME/keyboards/hadron/ver2 and run 
qmk compile

The qmk wrapper will realize your CWD, and automatically fill in your desired/sane results

## qmk compiling <configurator_output.json>
This will convert the json to appropriate keymap.c

## qmk compile and flash <configurator_output.json>
qmk flash [-bl <bootloader>] [-c] [-e <var>=<value>] <configuratorExport.json>

## Errors 

### Cannot open /dev/ttyACM0 
Either perform flash as root, or add your current user to group 'uucp'


## Debug console(!)
If firmware is compiled with CONSOLE_ENABLED=yes, then there is a magic(?) qmk console embedded. (This might/probably requires the custom udev rules)
## keymap.c 
