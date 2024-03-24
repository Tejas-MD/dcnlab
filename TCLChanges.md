# Program 3: 

``` tcl
$ns duplex-link-op $n4 $n3 orient right-up
$ns make-lan "$n0 $n1 $n2 $n3" 100Mb 300ms LL Queue/DropTail Mac/802_3
$ns make-lan "$n4 $n5 $n6 $n7" 100Mb 300ms LL Queue/DropTail Mac/802_3

set err [new ErrorModel]
$ns lossmodel $err $n3 $n4
$err set rate_ 0.1
```


# Program 4:

``` tcl
$ns make-lan "$n0 $n1 $n2 $n3 $n4 $n5" 100Mb 100ms LL Queue/DropTail Mac/802_3

set file1 [open file1.tr w]
$tcp0 attach $file1
set file2 [open file2.tr w]
$tcp2 attach $file2

$tcp0 trace cwnd_ 
$tcp2 trace cwnd_

```

# Program 5:

``` tcl
Agent/Ping instproc recv {from rtt} {
$self instvar node_
puts "node [$node_ id] received ping answer from \ $from with round-trip-time $rtt ms."
}

set PingAgent1 [new Agent/Ping]
$ns attach-agent $n0 $PingAgent1
set PingAgent2 [new Agent/Ping]
$ns attach-agent $n1 $PingAgent2
set PingAgent3 [new Agent/Ping]
$ns attach-agent $n2 $PingAgent3
set PingAgent4 [new Agent/Ping]
$ns attach-agent $n3 $PingAgent4
set PingAgent5 [new Agent/Ping]
$ns attach-agent $n4 $PingAgent5
set PingAgent6 [new Agent/Ping]
$ns attach-agent $n5 $PingAgent6

$ns connect $PingAgent1 $PingAgent2
$ns connect $PingAgent2 $PingAgent3
$ns connect $PingAgent3 $PingAgent4
$ns connect $PingAgent4 $PingAgent5
$ns connect $PingAgent5 $PingAgent6
$ns connect $PingAgent6 $PingAgent1



$ns at 0.1 "$PingAgent1 send"
$ns at 0.1 "$PingAgent2 send"
$ns at 0.1 "$PingAgent3 send"
$ns at 0.1 "$PingAgent4 send"
$ns at 0.1 "$PingAgent5 send"
$ns at 0.1 "$PingAgent6 send"


$ns at 0.1 "$PingAgent1 send"
$ns at 0.1 "$PingAgent2 send"
$ns at 0.1 "$PingAgent3 send"
$ns at 0.1 "$PingAgent4 send"
$ns at 0.1 "$PingAgent5 send"
$ns at 0.1 "$PingAgent6 send"
```