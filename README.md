# Daimon

**Simple, Unix-native system monitoring based on known-good state.**

Daimon monitors systems by running ordinary Unix commands and detecting changes in their output.

Instead of requiring an administrator to define every possible failure condition, Daimon records a **known-good state** and reports when that state changes. A change can then be investigated and either treated as an abnormal condition or accepted as the **new normal**.

Daimon has been used to monitor IT infrastructure at the Michigan Neuroscience Institute (MNI), University of Michigan, for more than two decades.

## How it works

Daimon deliberately keeps the monitoring model simple:

```text
              cron
                |
                v
          +-----------+
          |   daimon  |
          +-----------+
                |
                v
       run an ordinary command
                |
                v
        compare with baseline
             /       \
          same       changed
           |            |
         ignore      record change
                         |
                         v
                  notify / review
```

A monitoring task is simply a command whose output represents some aspect of system state.

For example:

```bash
daimon -t localhost -- dm-linux localhost -d 99P
```

Daimon saves the command's output as the baseline. When the command produces different output later, Daimon records the difference and can notify the administrator.

This makes it useful for things that are difficult to monitor with simple thresholds, such as:

- disk and filesystem state
- drive SMART attributes
- RAID configuration and status
- file and directory changes
- permissions
- system configuration
- hardware information
- custom diagnostic commands
- practically anything that can be expressed as a Unix command

### New normal

Not every change is an error.

A disk may be replaced. A filesystem may grow. A system administrator may intentionally change a configuration.

Daimon therefore treats a change as something that deserves attention, rather than automatically declaring it a failure. After reviewing the change, the administrator can accept it as the **new normal**.

This simple distinction helps reduce the need to maintain large collections of hard-coded monitoring rules.

## Commands

### `daimon`

Runs a monitoring command, compares its output with the stored baseline, records changes, and optionally sends notifications.

```bash
daimon -t test/localhost -- dm-linux localhost -d 99P
```

### `dm-check`

Reviews monitoring results.

```bash
# Print a summary report for all tasks
dm-check -ar

# Check abnormal tasks
dm-check -a
```

### `dm-linux`

A collection of Linux system diagnostics, including:

- storage usage
- CPU load
- internal temperature
- drive SMART attributes
- file changes
- directory permissions
- LSI RAID
- Areca RAID
- custom commands

Examples:

```bash
dm-linux localhost -d 99P
dm-linux localhost -d 1P:/
```

### `dm-ssh`

A parallel SSH utility based on GNU Parallel.

It runs the same command on multiple hosts and combines the output, making it easier to inspect a group of systems at once.

### `dm-scp`

Copies files or directories between the local system and multiple hosts in parallel.

## Installation

Clone the repository:

```bash
cd /opt
git clone https://github.com/daimh/daimon.git
```

Make the configuration available under `/etc`:

```bash
ln -s /opt/daimon/etc/daimon.conf /etc/daimon.conf
```

Add the Daimon `bin` directory to your `PATH`:

```bash
export PATH=/opt/daimon/bin:$PATH
```

See [`etc/crontab.example`](etc/crontab.example) for examples of scheduling monitoring tasks.

## Quick start

Run a diagnostic command directly:

```bash
dm-linux localhost -d 99P
```

Run the same command under Daimon:

```bash
daimon -t test/localhost -- dm-linux localhost -d 99P
```

Run the task again later. If its output has changed, Daimon records the difference.

Review monitoring results:

```bash
dm-check -ar
```

Check individual commands with:

```bash
command -h
```

For example:

```bash
daimon -h
dm-check -h
dm-linux -h
dm-ssh -h
dm-scp -h
```

## Why Daimon?

Modern monitoring systems are often built around agents, databases, metrics, dashboards, and predefined thresholds.

Daimon takes a different approach:

> **If a system was healthy yesterday, show me what changed today.**

It uses the tools Unix already provides—commands, files, `diff`, cron, SSH, and email—to turn ordinary command output into persistent system monitoring.

There is no monitoring server to maintain and no special agent protocol to deploy.

If you can write a command that describes something you care about, you can monitor it with Daimon.

## Production history

Daimon was originally developed at the University of Michigan and has been used for more than 20 years to monitor production IT infrastructure at MNI.

Its long-term use is an important part of the project's design philosophy:

**keep monitoring simple enough that it can remain useful for decades.**

## Contributing

Contributions are welcome.

If you have an improvement, bug fix, or new diagnostic that would be useful to other Unix/Linux administrators, please open an issue or pull request.

## Acknowledgments

- Fan Meng, Ph.D., Research Associate Professor, Psychiatry, University of Michigan
- Ruth Freedman, MPH, former Administrator, MNI, University of Michigan
- Julie Gales, Administrative Director, MNI, University of Michigan
- Andy Lin, MNI, University of Michigan
- Huda Akil, Ph.D., Director, MNI, University of Michigan
- Stanley J. Watson, M.D., Ph.D., Director, MNI, University of Michigan
- Prashanth Thinakaran

## Author

**Manhong Dai**

## License

MIT License

Copyright © 2002–2026 University of Michigan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
