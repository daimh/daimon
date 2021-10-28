# daimon, the simplest but powerful and flexible monitoring tool

bin/daimon runs whatever command after --, and then compares its output with standard file(s) under var directory. If the output is different and the difference is new, daimon will send out email alerts.

bin/dm-linux monitors storage usage, CPU load percentage, internal temperature, drive SMART attributes, file changes, directory permissions, LSI raid and Areca raid. It also supports custom commands to be flexible.

bin/dm-ups supports two APC UPS models. Feel free to add new models and send me a pull request.

We has been using daimon to monitor UPS status, Linux, and even LSI raid card in Windows with ssh for a decade.

## Installation
```
cd /opt
git clone https://github.com/daimh/daimon.git
ln -s /opt/daimon/etc/daimon.conf /etc
```
Then check out file etc/crontab.example, and add /opt/daimon/bin to your PATH

## Usage
```
dm-linux localhost -d /:99
dm-linux localhost -d /:1
daimon -t test/localhost -- dm-linux localhost -d /:99
daimon -t test/localhost -- dm-linux localhost -d /:1
dm-report
cd /opt/daimon/var/test/localhost
dm-check
```

## Help
use '-h' with each  command under bin/

## Contribute

Contributions are always welcome!

## Copyright

Developed by [Manhong Dai](mailto:daimh@umich.edu)

Copyright © 2021 University of Michigan. License [GPLv3+](https://gnu.org/licenses/gpl.html): GNU GPL version 3 or later 

This is free software: you are free to change and redistribute it.

There is NO WARRANTY, to the extent permitted by law.

## Acknowledgment

Ruth Freedman, MPH, former administrator of MNI, UMICH

Fan Meng, Ph.D., Research Associate Professor, Psychiatry, UMICH

Huda Akil, Ph.D., Director of MNI, UMICH

Stanley J. Watson, M.D., Ph.D., Director of MNI, UMICH
