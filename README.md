# PHY-Functions

Fisrt we need a mechansim to detect erroron thr level of transport block.

**CRC**
For this purpose CRC(Cyclic Redundancy Check) is calculated and added to the transport block. On the reciever side, CRC can be used to detect error in the transport block level and request retransmissions if transport block is fully corrupt.
