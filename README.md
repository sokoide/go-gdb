# go-gdb
Fixed runtime-gdb.py script for goroutine debugging.
Originally written at http://blog.securitymouse.com/2014/10/golang-debugging-turning-pennies-into-gs.html.

## Note
Check branch and use the same version of the script as your target go version.
It may not work in 32bit process or other OS than OSX/Windows.

## How to use
1 run your debuggee written in go under gdb, or run gdb and attach to it
1 source path-to-runtime-gdb.py
1 info goroutine
1 goroutine $goroutine-id bt

## Samples
```
(gdb) info go
  1 waiting  fname=runtime.gopark faddr=0x13415 &g=0xc208000120 waitreason="sleep"
  2 waiting  fname=runtime.gopark faddr=0x13415 &g=0xc208000480 waitreason="force gc (idle)"
  3 waiting  fname=runtime.gopark faddr=0x13415 &g=0xc2080005a0 waitreason="GC sweep wait"
  4 waiting  fname=runtime.gopark faddr=0x13415 &g=0xc2080006c0 waitreason="finalizer wait"
  5 syscall  fname=runtime.switchtoM faddr=0x366c0 &g=0xc208000a20
(gdb) goroutine 1 bt
#0  runtime.gopark (unlockf=0x2eba0 <runtime.parkunlock_c>, lock=0x1576e0 <runtime.timers>, reason="sleep")
    at /Users/sokoide/repo/go/src/runtime/proc.go:131
#1  0x0000000000013488 in runtime.goparkunlock (lock=0x1576e0 <runtime.timers>, reason="sleep") at /Users/sokoide/repo/go/src/runtime/proc.go:136
#2  0x0000000000017de5 in runtime.timeSleep (ns=2000000000) at /Users/sokoide/repo/go/src/runtime/time.go:58
#3  0x00000000000020f8 in main.f2 (a=40, b=2, ~r2=1) at /Users/sokoide/workspace/go/foo/foo.go:24
#4  0x0000000000002551 in main.main () at /Users/sokoide/workspace/go/foo/main.go:22
```

## More Info
http://www.sokoide.com/wp/2015/03/02/debugging-go-program-with-gdb-1/
http://www.sokoide.com/wp/2015/03/03/debugging-go-program-with-gdb-2/

