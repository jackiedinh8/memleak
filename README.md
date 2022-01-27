# memleak

A tool to trace and display outstanding allocations to detect
memory leaks in user-mode processes and the kernel.

```
USAGE: memleak [-h] [-p PID] [-t] [-a] [-o OLDER] [-c COMMAND]
                [--combined-only] [--wa-missing-free] [-s SAMPLE_RATE]
                [-T TOP] [-z MIN_SIZE] [-Z MAX_SIZE] [-O OBJ]
                [interval] [count]

EXAMPLES:

./memleak -p $(pidof allocs)
        Trace allocations and display a summary of "leaked" (outstanding)
        allocations every 5 seconds
./memleak -p $(pidof allocs) -t
        Trace allocations and display each individual allocator function call
./memleak -ap $(pidof allocs) 10
        Trace allocations and display allocated addresses, sizes, and stacks
        every 10 seconds for outstanding allocations
./memleak -c "./allocs"
        Run the specified command and trace its allocations
./memleak
        Trace allocations in kernel mode and display a summary of outstanding
        allocations every 5 seconds
./memleak -o 60000
        Trace allocations in kernel mode and display a summary of outstanding
        allocations that are at least one minute (60 seconds) old
./memleak -s 5
        Trace roughly every 5th allocation, to reduce overhead

  -a, --show-allocs          Show allocation addresses and sizes as well as
                             call stacks
  -c, --command=COMMAND      Execute and trace the specified command
  -C, --combined-only        Show combined allocation statistics only
  -o, --older=MILLISECONDS   Prune allocations younger than this age in
                             milliseconds
  -O, --obj=OBJ              Attach to allocator functions in the specified
                             object
  -p, --pid=PID              Process PID
  -P, --percpu               trace percpu allocations
  -s, --sample-rate=RATE     Sample every N-th allocation to decrease the
                             overhead
  -t, --trace                Print trace message for each alloc/free call
  -T, --top                  Display only this many top allocating stacks (by
                             size)
  -W, --wa-missing-free      Workaround to alleviate misjudgments when free is
                             missing
  -z, --min-size             Capture only allocations larger than this size
  -Z, --max-size             Capture only allocations smaller than this size
  -?, --help                 Give this help list
      --usage                Give a short usage message
  -V, --version              Print program version
```

# Install
```
git clone https://github.com/jackiedinh8/memleak
cd memleak
git submodule update --init
make
```
