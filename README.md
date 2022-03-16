# daimon, the simplest but powerful and flexible monitoring tool

'daimon' runs a sub-command specified in crontab, compares its output with the standard file(s) under the TASK directory under var/, records the history, and sends out email alert if user specifed so in /etc/daimon.conf if the output is different.

'dm-report' reports all monitoring task status.

'dm-check' checks the output of all abnormal tasks under current directory. User can choose to confirm the status is abnormal or a new normal.

'dm-linux' prints storage usage, CPU load percentage, internal temperature, drive SMART attributes, file changes, directory permissions, LSI raid and Areca raid. It also supports custom commands.

'dm-ups' prints UPS status, it supports two APC UPS models. Feel free to add new models and send me a pull request.

'dm-ssh' is another parallel ssh based on GNU parallel.

We has been using daimon to monitor UPS status and hundreds of Linux machines for a decade. Recently we also use it to monitor LSI raid card in Windows machine.

## Installation
```
cd /opt
git clone https://github.com/daimh/daimon.git
ln -s /opt/daimon/etc/daimon.conf /etc
```
Then check out file etc/crontab.example, and add /opt/daimon/bin to your PATH

## Usage
```
dm-linux localhost -d 99P
dm-linux localhost -d 1P:/
daimon -t test/localhost -- dm-linux localhost -d 99P
daimon -t test/localhost -- dm-linux localhost -d 1P:/
dm-report -a
dm-check -a
```

## Help
use '-h' with each command

## Contribute

Contributions are always welcome!

## Copyright

Developed by [Manhong Dai](mailto:manhongdai@gmail.com)

Copyright © 2002-2021 University of Michigan 

Copyright © 2022 KLA, Corporation

License [GPLv3+](https://gnu.org/licenses/gpl.html): GNU GPL version 3 or later 

This is free software: you are free to change and redistribute it.

There is NO WARRANTY, to the extent permitted by law.

## Acknowledgment
Ruth Freedman, MPH, former administrator of MNI, UMICH

Fan Meng, Ph.D., Research Associate Professor, Psychiatry, UMICH

Huda Akil, Ph.D., Director of MNI, UMICH

Stanley J. Watson, M.D., Ph.D., Director of MNI, UMICH

Prashanth Thinakaran, KLA

Raghuram Bondalapati, KLA
