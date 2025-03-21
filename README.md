# Daimon, the simplest but powerful and flexible monitoring tool

Tired of running commands every day, hour, or minute to check your system's health? Or are you struggling to debug a random system failure, which is always the hardest task? Daimon is here to help. We’ve been using it to monitor the IT infrastructure at the Michigan Neuroscience Institute, University of Michigan, for decades.

Daimon runs a sub-command specified in crontab, compares its output with standard files located in the TASK directory under `var/`, records the differences, logs them with a timestamp, identifies known critical alerts, and sends email notifications if specified by the user in `/etc/daimon.conf`.

- **dm-check**: Prints a summary report or checks for abnormal tasks. Users can confirm whether the status is abnormal or a new normal.
- **dm-linux**: Displays storage usage, CPU load, internal temperature, drive SMART attributes, file changes, directory permissions, LSI RAID, and Areca RAID stats. It also supports custom commands.
- **dm-scp**: Copies a local file or directory to mutiple nodes in parallel, or vice versa.
- **dm-ssh**: A unique parallel SSH tool based on GNU Parallel. It combines the output of all SSH commands to save your eyes, fingers, and time.

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
dm-check -ar	#print summary report for all
dm-check -a		#check abnormal task
```

## Help
use '-h' with each command

## Contribute

Contributions are always welcome!

## Acknowledgment

Fan Meng, Ph.D., Research Associate Professor, Psychiatry, UMICH

Ruth Freedman, MPH, former administrator of MNI, UMICH

Julie Gales, Administrative Director, MNI, UMICH

Andy Lin, MNI, UMICH

Huda Akil, Ph.D., Director of MNI, UMICH

Stanley J. Watson, M.D., Ph.D., Director of MNI, UMICH

Prashanth Thinakaran

## Developer

[Manhong Dai](mailto:manhongdai@gmail.com)

## License

MIT License

Copyright © 2002-2023 University of Michigan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
