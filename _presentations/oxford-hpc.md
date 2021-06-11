---
title: HPC and how to use it
layout: default
---

# High-performance computing and how to use it

This document introduces the high-performance computing resources available to
researchers in Oxford (or people working on collaborative projects),
particularly in the School of Geography and the Environment.

There's a risk that this will go out of date - please see [SoGE intranet
pages](https://intranet.ouce.ox.ac.uk/it/cs/index.html) for potentially more
recent information.

1. Why would I run code on a computer that's not my laptop/desktop?
1. What resources are available? How do I use them?


## Why?

Reasons to consider using a server, a cluster or HPC:
- laptop fan is getting tired
- long-running process that stops you shutting down/unplugging
- too much data to handle, running out of disk space
- not enough memory
- way more model-runs/iterations/replicates than would be feasible to run before
  the end of the project

Essentially - wanting to run more or bigger or longer computations than are
possible on a single, normal-sized machine.


## What?

All of these things - clusters, HPC, the cloud - are essentially more or bigger
computers, running somewhere else.

### School of Geography and the Environment (SoGE) Linux cluster

The SoGE Linux cluster has (this bit may be out of date, gives a lower bound):
- plenty of terabytes of storage
- Over 30 nodes with >12 cores each
- some reasonably high-memory nodes (>100GB RAM)
- some GPU nodes

Contact itsupport to request an account. You might want to be added to a
project group to access a shared directory.

#### VPN - Virtual Private Network

You need to be connected to the VPN before you can log in to the server
from outside of the department.

VPN help - https://help.it.ox.ac.uk/network/vpn/index

#### SSH - Secure Shell

The usual way to connect to and run programs on high-performance compute
clusters is on the command line. This applies for the SoGE and ARC clusters.

On Linux or Mac, open a Terminal:

    $ echo "Hello"
    > Hello

    $ pwd
    > /home/tom/some_directory

    $ ls
    > some_file.txt data.csv image.png ...

Tutorial - http://www.linuxcommand.org/

On Windows, the same commands would work in the
[Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/)
or [Git Bash](https://git-scm.com/download/win) or would be a little different
in Powershell or cmd.exe. Consider installing WSL and/or Git Bash - they let you
learn the Linux command line on your local computer and mean you don't need to
learn and remember two different ways of working.

On Linux or Mac (or in WSL or Bash), you should be able to use the ssh command
to connect to a remote computer - remember to use your Oxford username:

    ssh abcd1234@linux.ouce.ox.ac.uk
    > prompt for password
    > once you're logged in, try running "pwd" and "ls" to see where you are

On Windows, without installing a different command line, you can use the
program [putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
to connect - click through the forms to set up a new SSH connection.

One quirk when connecting to the OUCE server is that it randomly assigns you a
node on the cluster to log in to (linux1 or linux2 .... linux32) and sometimes
that node is overloaded so login fails. Try again when that happens, or pick a
specific node:

    ssh abcd1234@linux3.ouce.ox.ac.uk


#### Moving files

__`scp`__ - copy files to the cluster

Copy a single file to your home directory (`~` for short) on the cluster:

    scp data.csv abcd1234@linux.ouce.ox.ac.uk:~/

Copy a folder to the cluster, spelling out the full path:

    scp -r ./data abcd1234@linux.ouce.ox.ac.uk:/ouce/staff/home/abcd1234/project/

Copy from the cluster to your local computer:

    scp -r abcd1234@linux.ouce.ox.ac.uk:/ouce/staff/home/abcd1234/project/results ./


__`rsync`__ - sync a directory with the cluster

Similar to `scp`, but can keep directories in sync and avoid sending files that
already exist:

    rsync -azP ./data abcd1234@linux.ouce.ox.ac.uk:/ouce/staff/home/abcd1234/project/

Tutorial - https://www.digitalocean.com/community/tutorials/how-to-use-rsync-to-sync-local-and-remote-directories-on-a-vps


__`WinSCP`__ - File transfer for Windows https://winscp.net/eng/index.php

Graphical program for file transfer - set up connection, browse through
folders. [Filezilla](https://filezilla-project.org/) is a good cross-platform
alternative.


#### Long jobs

`screen` - leave a job running and log out

- log in to a node
- remember which node number you're on (e.g. linux24)
- type `screen` to start a screen session
- run command
- type `CTRL+A, D` to quit screen
- log out
- log back in to the specific node number (e.g. linux24.ouce.ox.ac.uk)
- type `screen -r`
- see how your process is doing


#### Many jobs

`parallel` - run in parallel https://www.gnu.org/software/parallel/

Count the lines in all the CSV files anywhere in the current directory:

    find . -name '*.csv' | parallel wc -l

Use an argument list from a file (each line gets passed to the command
separately, replacing `{}`):

    cat list.txt | parallel echo {}

Use an argument list from a CSV (each row gets passed to the command
separately, and each column value is available as a numbered argument):

    parallel -a args.csv --colsep ',' python run.py --alpha {2} --beta {1}

One important option for `parallel` is `-j` - to limit the number of jobs that
run in parallel. E.g.

    seq 1 8 | parallel -j4 'sleep 1 && echo {}'


#### Checking the cluster

Handy commands to give a slightly clunky overview of what's running and the
resources available

```bash
# check how many copies of my_program are running on each node
for i in {1..32}; do printf "linux$i "; ssh linux$i.ouce.ox.ac.uk ps -e | grep my_program | wc -l; done

# check number of cpus on each node
for i in {1..32}; do printf "linux$i "; ssh linux$i.ouce.ox.ac.uk nproc --all; done

# check memory usage on each node
for i in {1..32}; do printf "\nlinux$i\n"; ssh linux$i.ouce.ox.ac.uk free -g; done
```


### Oxford Advanced Research Computing (ARC) clusters

The University of Oxford has a couple of clusters managed centrally by the ARC
service.

Introduction, help, how-to:

- https://help.it.ox.ac.uk/arc/index

ARCUS-HTC is optimised for single-core jobs and running serial applications
many times - like a parameter sweep, sensitivity analysis or big scenario
analysis. In terms of resources, it has:

- 1728 (108*16) 2.0GHz Xeon SandyBridge/Ivybridge cores
- 64GiB (80 nodes), 128GiB (4 nodes) RAM
- 20TB scratch disk
- GPU resources

ARCUS-B is optimised for large parallel jobs spanning multiple nodes - like a
climate model run or other gridded, massively parallel computation. In terms of
resources, it has:

- 5792 (362*16) Intel E5-2640v3 (Haswell) cores
- 64GiB (246 nodes), 128GiB (92 nodes), 256GiB (9 nodes) of RAM
- Low latency interconnect
- Minimum job size 16 cores (1 node)

Contact ARC support to set up an account and request credits if necessary.


#### Scheduler

The ARC cluster runs jobs using a scheduler. Instead of running things directly
or through `screen`, you write a short configuration script to tell the cluster
what you want to run, and submit it to the job scheduler. Your jobs sit in a
queue until there's space to run them.

- https://help.it.ox.ac.uk/arc/job-scheduling

Here's a simple example, plenty more details in the link above.

Save the following in a script `test_job.sh`:

```bash
#!/bin/bash

# set the number of nodes
#SBATCH --nodes=1

# set max wallclock time
#SBATCH --time=00:00:10

# set name of job
#SBATCH --job-name=test123

# mail alert at start, end and abortion of execution
#SBATCH --mail-type=ALL

# send mail to this address
#SBATCH --mail-user=user.name@ouce.ox.ac.uk

# run the application
echo "Hello"
```

Then submit the job:

    sbatch test_job.sh


### External facilites

For more storage or compute, access to specialist data or computational support,
or to support broader collaborations, there are national facilities, and further
international links through these.

- [DAFNI (Data and Analytics Facility for National Infrastructure)](https://www.dafni.ac.uk/)
  for infrastructure systems data and modelling, mainly EPSRC-remit research
- [JASMIN](http://www.jasmin.ac.uk/) for environmental data and modelling,
  mainly NERC-remit research
- [Tier-2 HPC facilities](https://epsrc.ukri.org/research/facilities/hpc/tier2/)
  for access to various newer architectures (multicore/GPU/ARM...)
- [ARCHER (Advanced Research Computing High End Resource)](http://www.archer.ac.uk/)
  national supercomputer, "Tier-1", for massive parallel workloads
