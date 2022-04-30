# PHY-Functions

Fisrt we need a mechansim to detect erroron thr level of transport block.

**CRC**<br />
For this purpose CRC(Cyclic Redundancy Check) is calculated and added to the transport block. On the reciever side, CRC can be used to detect error in the transport block level and request retransmissions if transport block is fully corrupt.

A 24 bit CRC is used for payloads larger than 3824 btis and if payload is smaller than the 16 bit CRC is used.

**LDPC Coding**<br />
We have seen error detetection mechanism in transport block level , let see procedure for error correction. When it comes to channel coding , which is used for error correction ,NR uses LDPC Coding. 

LDPC uses a parameter called BASE GRAPH , that governs the coding process. In our support to LDPC base graps, one for small transport block and one for large transport block.

LDPC uses two parameter :-<br />
1. Transport Block Size(TBS)<br />
2. Code Rate

When a TBS and Code rate is above the threshold then Base-Graph1 iS used otherwise BaseGraph-2 is used.

If transport block is larger than it will be segmented into small block known as code block before performing LDPC Coding to it.

Channel Coding is the process of adding additional bits that makes the information resilient to the channel attenuation.

Although it result in the reduntation of data rate ,  it is essential to combat the attenuation.

So some of the error can be corrected without retransmission using channel coding process. In this case , we need to apply LDPC coding to each code-block to improves its resiliency and to correct some of the small error.

**Rate Matching**<br />
Not all the output bit of LDPC coding step can be transmitted in a given transmitted time. So after the LDPC coding , rate matching takes the coded bits and extract the exact set of bits that can be transmitted in a given transmission time of interval. It is perform separately for each code block.

**Scrambling**<br />
The Device (UE) may hearing signals from multiple gNB simultaneously. So can the UE differentiate the incominh=g signals into separate gNB's at the very low layers of the protocol-stack.

Because in high layer , we have different lways of addressing the devices. But a PHY-layer , the device needs a mechanism so that it can listen to one gNB and ignore the information from interfering gNB.

The Scrambling Block of code is multiplied by scrambling sequence.

Now the device that knows the scrambling sequence can see the information corresponding to the correct gNB as a signal.So in this way UE can lsiten to the intended gNB and treat all the other gNB as interference signals(as ignored).

**Modulation**<br />
After scrambling is done , now its time for modulation.So in downlink data modulation, we transform block of scrambled bits from 1's and 0's to a corresponding complex modulation symbols.

Now one symbol can represent 'n' bits depending on what is the modulation type that's used.

Supported Modulation schemes:-<br />
QPSK, 16QAM, 64QAM and 256QAM in both downlink and uplink.

**Layer Mapping**<br />
It is important to recall that NR supports special multiplexing , it means it can be transmit more than one layer of data simultaneouly using benefits of multiple antenna technologies.Since many of the NR Radio includes multiple antennas. It is often  possible multiple layers are supported. 

In this step, the complex value modulation symbols that needs to be transmitted are mapped into one or more layer.


**Antenna Mapping and Pre-coding**<br />
After mapping to different layers, the next step is to map the corresponding virtual antenna ports.

In order to different data layer to be decoded as if they are different layers on the reciever they need to be pre-coded.
Pre-coding are based on the channel conditions , the pre-coding process maps the different number of layers into the corresponding number of virtual ports.

This uses precoding matrix .It i sselected based on 'what is the current channel conditions'.

**Resource and Physical Antenna Mapping**<br />
From the previos step of antenna mapping , we have the symbols for each virtual antenna ports. The Resource Block mapping takes the modulation symbols to be transmitted on each antenna ports anf maps to the set of resource bllock assigned by the MAC's scheduler for current transmission.

Resorce block are shared together with control and reference signals. The other resource block fro actual data transmission.

Number of physical antenna is larger than number of virtual antenna ports, which is used in pre-coding stage. So, linear mapping is applied to map from virtual antenna port to physical antenna.

For mapping, we take the data that is mapped different virtual antenna port and put them into the right time and frequency resource block, which is correspond to the decisionmade by scheduler. And we also placed the control signals here and then we put it to the actual physical antenna port.

**OFDM, DAC, RF**<br />
Till now, symbols are mapped into the OFDMwaveform together with corresponding cyclic prefixes. Now they are converted to analog waveform using Digital to Analog Converter(DAC). And then converted to RF frequencies and fed to the Antenna for transmission.
 
If Analog-Beam Forming is used , it is carried out in the time domain just before transmission.
