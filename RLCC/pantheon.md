### run on every boot
```
sudo sysctl -w net.ipv4.ip_forward=1
cd /home/airman/Github/pantheon/third_party/pcc-experimental/src
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/airman/Github/pantheon/third_party/pcc-experimental/src/core/ 
```

### how to change pcc-rl model
PCC-Uspace.md check

### Recent Test
```
src/experiments/test.py local --schemes "ccrl" --data-dir 0203rb-LTE -t 60 --run-times 20 --uplink-trace /home/airman/Github/mahimahi/traces/Verizon-LTE-short.up --downlink-trace /home/airman/Github/mahimahi/traces/Verizon-LTE-short.down --extra-mm-link-args " --uplink-queue=droptail --uplink-queue-args=packets=500" --prepend-mm-cmds "mm-delay 32"
```

### LTE Link
```
src/experiments/test.py local --schemes "cubic pcc vivace bbr copa pcc_experimental" --data-dir 0205icmlLTE -t 30 --run-times 5 --uplink-trace /home/airman/Github/mahimahi/traces/Verizon-LTE-short.up --downlink-trace /home/airman/Github/mahimahi/traces/Verizon-LTE-short.down --extra-mm-link-args " --uplink-queue=droptail --uplink-queue-args=packets=500" --prepend-mm-cmds "mm-delay 32"
```

### general Link
```
src/experiments/test.py local --schemes "cubic pcc vivace bbr copa pcc_experimental" --data-dir 0205icml -t 30 --run-times 5 --extra-mm-link-args "--uplink-queue=droptail --uplink-queue-args=packets=500" --prepend-mm-cmds "mm-delay 32"

src/experiments/test.py local --schemes "pcc_experimental" --data-dir ccrltest2 -t 30 --run-times 5 --extra-mm-link-args "--uplink-queue=droptail --uplink-queue-args=packets=500" --prepend-mm-cmds "mm-delay 32"
```

#### ICML19 paper env
```

```

### Optinal arguments:
```
optional arguments:
  -h, --help            show this help message and exit
  -f FLOWS, --flows FLOWS
                        number of flows (default 1)
  -t RUNTIME, --runtime RUNTIME
                        total runtime in seconds (default 30)
  --interval INTERVAL   interval in seconds between two flows (default 0)
  --all                 test all schemes specified in src/config.yml
  --schemes "SCHEME1 SCHEME2..."
                        test a space-separated list of schemes
  --run-times TIMES     run times of each scheme (default 1)
  --start-run-id ID     run ID to start with
  --random-order        test schemes in random order
  --data-dir DIR        directory to save all test logs, graphs, metadata, and
                        report (default pantheon/src/experiments/data)
  --pkill-cleanup       clean up using pkill (send SIGKILL when necessary) if
                        there were errors during tests
  --uplink-trace TRACE  uplink trace (from sender to receiver) to pass to mm-
                        link (default pantheon/test/12mbps.trace)
  --downlink-trace TRACE
                        downlink trace (from receiver to sender) to pass to
                        mm-link (default pantheon/test/12mbps.trace)
  --prepend-mm-cmds "CMD1 CMD2..."
                        mahimahi shells to run outside of mm-link
  --append-mm-cmds "CMD1 CMD2..."
                        mahimahi shells to run inside of mm-link
  --extra-mm-link-args "ARG1 ARG2..."
                        extra arguments to pass to mm-link when running
                        locally. Note that uplink (downlink) always represents
                        the link from sender to receiver (from receiver to
                        sender)
```
