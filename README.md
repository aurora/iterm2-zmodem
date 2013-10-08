# Z-Modem integration for iTerm2

## Preface

The purpose of this script is to add Z-Modem file transfer support to (in theory) any ssh session
from within iTerm2.

This script is inspired by and would probably not exist without the scripts "iterm2-recv-zmodem.sh" 
and "iterm2-send-zmodem.sh" (c) by Matt Mastracci, https://github.com/mmastrac/iterm2-zmodem. 

The motivation to not forking but rewriting the scripts was mainly to put the functionality into 
a single shell script to make it possible to share common code used by both sending and receiving 
funtionality and to make it more easy to extend the functionality in future.


## Installation

### Prework

For sending and receiving files the Z-Modem tools are required on both machines involved in the 
transfer. I recommend installing the lrzsz package which should be available in most Linux 
distributions or which can be downloaded and build from source from: 

http://ohse.de/uwe/software/lrzsz.html

A recent version of iTerm2 is required for Mac OS X to make things work, downloadable from:

http://www.iterm2.com/

Optionally the script supports Growl notifications. For this to work the Growl application and 
the additional tool "growlnotify" is needed.

### Installation and configuration

The script iterm2-zmodem should by copied to /usr/local/bin. 

It's required to setup the following "Triggers" in iTerm2:

    Regular expression: \*\*B0100
    Action:             Run Coprocess
    Parameters:         /usr/local/bin/iterm2-zmodem sz

    Regular expression: \*\*B00000000000000
    Action:             Run Coprocess
    Parameters:         /usr/local/bin/iterm2-zmodem rz

The script "iterm2-zmodem" tries to determine the names (lrz, rz, lsz, sz) and locations 
of the binaries of growlnotify and the Z-Modem tools. The pathes searched are: 
    
    /usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin
    
If the Z-Modem tools are installed in some unusual place, the path can be specified when 
configuring the triggers using the LRZSZ_PATH envirnment variable, the "Parameters" setting
of the trigger has to be modified in this case to become (eg):

    Parameters:         LRZSZ_PATH=/opt/lrzsz/bin /usr/local/bin/iterm2-zmodem rz

## Usage

The file transfer is initiated on the remote machine by executing rz respectively lrz 
(for receiving a file on the remote machine) or by executing sz respectively lsz (for sending
a file to the remote machine). See the command usage information of the Z-Modem tools for 
additional details.

Note, that sending files will overwrite the destination file on the local machine, if it
already exists.


## Disclaimer

Use with caution. This software may contain serious bugs. I can not be made responsible 
for any damage the software may cause to your system or files.

## License

### iterm2-zmodem

iterm2-zmodem

Copyright (C) 2013 by Harald Lapp harald@octris.org

This program is free software: you can redistribute it and/or modify it under the terms of the 
GNU General Public License as published by the Free Software Foundation, either version 3 of the 
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without 
even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU 
General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. 
If not, see http://www.gnu.org/licenses/.

### 3rd party code

The AppleScript portion included in the script is inspired by 
http://stackoverflow.com/questions/4309087/cancel-button-on-osascript-in-a-bash-script
licensed under cc-wiki with attribution required 
