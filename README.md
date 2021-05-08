Information:
----
With this script you are able to execute a command/scipt/program periodically with different amount of cores. It automatically
gets the amount of free cores and reruns your program based on this.

Setup
----
You have several ways to use this script. Either set the variable `${command}` in the script or set the environment variable 
`COMMAND` to the actual command you want to periodically execute with different amount of free cores each time. Not that 
the command in the envionment variable has a higher priority and overwrites the command passed as a flag. Please 
export `export LC_NUMERIC="en_US.UTF-8"` to make sure the decimal points are points. Also note that `export LANG="en.US"`
is set to make the parsing platform independent. 

Needed programs:
- `sysstats`
- `grep`
- `mpstat`
- `bc`

Usage in a script
---
You can use the bash variable `${free_cores}` in your command to specify the number of cores/threads you program
should use.

```bash
# return the command every 10 seconds
./run.sh -s 10 -c "echo foo"

# rerun you bitcoin miner every 3600 and check for free cores, while leaving 10 cores free. 
# I know thats stupid, dont do it.
./run.sh -e 10 -s 3600 -c "./bitcoin_miner.sh"

# rerun every 10 seconds and display the free cores
./run.sh -s 10 -c 'echo "currently you have ${free_cores} cores free."'
```