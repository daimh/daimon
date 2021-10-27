# daimon, the simplest monitoring tool

bin/daimon runs whatever command after --, and then compares its output with standard file(s) under var directory. If the output is different and the difference is new, daimon will send out email alerts.

## Installation
```
cd /opt
git clone https://github.com/daimh/daimon.git
ln -s /opt/daimon/etc/daimon.conf /etc
```
Then check out file etc/crontab.example, and add /opt/daimon/bin to your PATH

## Administration
```
dm-report
cd /opt/daimon/var
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
