# Cycle 2 --4 - Simulation of -bus-topology-Network -NS2
# Bus Topology Simulation in NS2

## AIM

To create and monitor a Bus Topology and effective data transmission using NS2 Software.

## APPARATUS REQUIRED

*   PC System with Linux OS
*   NS2 software

## ALGORITHM
 
* STEP 1: Start the program. 
* STEP 2: Declare the global variables ns for creating a new simulator. 
* STEP 3: Open the network animator file in the write mode. 
* STEP 4: Open the trace file in the write mode. 
* STEP 5: Transfer the packets in network. 
* STEP 6: Create the capable no of nodes. 
* STEP 7: Create the duplex-link between the nodes including the delay time, bandwidth 
and dropping queue mechanism. 
* STEP 8: Set a tcp connection for source node. 
* STEP 9: Set the destination node using tcp sink. 
* STEP 10: Set the window size and the packet size for the tcp. 
* STEP 11: Set up the ftp over the tcp connection. 
* STEP 12: Create the traffic generator CBR for the source and destination files. 
* STEP 13: Define the plot window and finish procedure. 
* STEP 14: In the definition of the finish procedure declare the global variables. 
* STEP 15: Close the trace file and namefile and execute the network animation 
file.
* STEP 16: At the particular time call the finish procedure. 
* STEP 17: Stop the program.
Program:
# Create simulator
set ns [new Simulator]

# NAM trace
set nf [open out.nam w]
$ns namtrace-all $nf

# Finish procedure
proc finish {} {
    global ns nf
    $ns flush-trace
    close $nf
    exec nam out.nam &
    exit 0
}

# Create nodes
set n0 [$ns node]
set n1 [$ns node]
set n2 [$ns node]
set n3 [$ns node]
set n4 [$ns node]

# Create LAN
set lan0 [$ns newLan "$n0 $n1 $n2 $n3 $n4" 0.5Mb 40ms \
          LL Queue/DropTail MAC/Csma/Cd Channel]

# TCP Agent
set tcp0 [new Agent/TCP]
$ns attach-agent $n1 $tcp0

# TCP Sink
set sink0 [new Agent/TCPSink]
$ns attach-agent $n3 $sink0

# Connect TCP -> Sink
$ns connect $tcp0 $sink0

# CBR Application
set cbr0 [new Application/Traffic/CBR]
$cbr0 set packetSize_ 500
$cbr0 set interval_ 0.01
$cbr0 attach-agent $tcp0

# Schedule
$ns at 0.5 "$cbr0 start"
$ns at 4.5 "$cbr0 stop"
$ns at 5.0 "finish"

$ns run

![WhatsApp Image 2025-10-23 at 20 52 44_1a5dc9a8](https://github.com/user-attachments/assets/f77f4b31-4e85-4ffd-8b59-3b761178c8e7)

## Result:
 Hence to create and monitor a Bus Topology and effective data transmission using NS2 Software is verified.

