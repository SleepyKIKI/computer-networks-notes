- Basic function :
  - provide "error-free", "ordered packets" services to network layer 

 

- Very Relaxed Assumptions:
  - [1] the physical layer, data link layer, and network layer are **independent processes** that communicate by passing messages back and forth
  - [2] machine A wants to send a long stream of data to machine B, using a **reliable**, **connection-oriented** service (**One direction only**)
  - [3] A is assumed to have an **infinite supply of data** ready to send and never has to wait for data to be produced.
  - [4] machines do not crash. These protocols **only deal with communication errors**



- Protocol 1 (a Utopian Simplex Protocol)

  - assumptions:

    - error free (no damaging and losing frame )
    - without considering flow-control 
    - one direction only (physical )
    - one direction only (logical : since one end is sending end, the other is receiving end )
    - both(transmitting and receiving) network layers are always ready 
    - always have an **infinite supply of data** ready to send
    - processing time can be ignored (on both sending and receiving end )
    - infinite buffer space 

  - structure :

    <img src="draft_fig\protocol_1.png" alt="protocol 1" style="zoom: 33%;" />

- protocol 2 (Stop-and-wait protocol for an error-free channel )

  - assumptions:

    - error free (no damaging and losing frame )
    - ~~without considering flow-control~~ (considering that frame sending may be faster than the receiver able to process) 
    - ~~one direction only (physical )~~ half duplex (physical )
    - one direction only (logical : since one end is sending end, the other is receiving end )
    - ~~both(transmitting and receiving) network layers are always ready~~
    - always have an **infinite supply of data** ready to send
    - processing time can be ignored (on both sending and receiving end )
    - ~~infinite buffer space~~ 

  - structure :

    <img src="draft_fig\protocol_2.png" alt="protocol 2" style="zoom:33%;" />

- protocol 3 (Stop-and-wait protocol for an noisy channel, there list the code of "ARQ" or called "PAR")

  - assumptions:

    - ~~error free (no damaging and losing frame )~~ ==error or damaging  may happen in transit== (so frame can be damaged or lost )
    - ~~without considering flow-control~~ (considering that frame sending may be faster than the receiver able to process) 
    - ~~one direction only (physical )~~ half duplex (physical )
    - one direction only (logical : since one end is sending end, the other is receiving end )
    - ~~both(transmitting and receiving) network layers are always ready~~
    - always have an **infinite supply of data** ready to send
    - processing time can be ignored (on both sending and receiving end )
    - ~~infinite buffer space~~

  - improvement :

    - sequence number 

      <img src="draft_fig\protocol_3_seq.png" alt="protocol 3 sequence  number change " style="zoom:33%;" />

  - structure : almost same as protocol 2

- protocol 4 (one-bit sliding window  )

  - assumptions:

    - ~~error free (no damaging and losing frame )~~ ==error or damaging  may happen in transit== (so frame can be damaged or lost )
    - ~~without considering flow-control~~ (considering that frame sending may be faster than the receiver able to process) 
    - ~~one direction only (physical )~~ ~~half duplex (physical )~~ full duplex (physical )
    - ~~one direction only (logical : since one end is sending end, the other is receiving end )~~ bidirectional
    - ~~both(transmitting and receiving) network layers are always ready~~
    - always have an **infinite supply of data** ready to send
    - processing time can be ignored (on both sending and receiving end )
    - ~~infinite buffer space~~

  - improvement :
    - two separate physical links --> interleaving --> piggybacking 

  - structure :

    <img src="draft_fig\protocol_4.png" alt="protocol 4" style="zoom:33%;" />

- protocol 5 (go-back-n)

  - assumptions:

    - ~~error free (no damaging and losing frame )~~ ==error or damaging  may happen in transit== (so frame can be damaged or lost )
    - ~~without considering flow-control~~ (considering that frame sending may be faster than the receiver able to process) 
    - ~~one direction only (physical )~~ ~~half duplex (physical )~~ full duplex (physical )
    - ~~one direction only (logical : since one end is sending end, the other is receiving end )~~ bidirectional
    - ~~both(transmitting and receiving) network layers are always ready~~
    - ~~always have an **infinite supply of data** ready to send~~
    - ~~processing time can be ignored (on both sending and receiving end )~~ Transmission and processing time can't be ignored  
    - ~~infinite buffer space~~ 
    - there is always reverse traffic (because in this code there isn't a timer for ack, so when there is no reverse traffic, the ack can't send back to the sender )

  - improvement :

    - pipelining

  - 对于protocol 5 的一些问题：

    - 书中237页的代码：其中的 while 循环判断条件，和下面的操作初看可能觉得有些问题。

      <img src="draft_fig\protocol_5_Q1_code.png" alt="protocol 5 问题" style="zoom: 67%;" />

      但实际上是没有问题的，参看下面的一种ack回复丢失的情况，这一段操作实际上对这种错误具有很强的弹性。

      <img src="draft_fig\protocol_5_Q1.png" alt="protocol 5 问题" style="zoom: 67%;" />

      这种方式实际上实际上叫：**cumulative acknowledgement**

      在第n帧的确认帧到达时，前面的n-1,n-2,n-3等等即被自动确认。

      这种方式可以为发送方提供更多的缓冲区。

      `This type of acknowledgement is called a cumulative acknowledgement. This property is especially important when some of the previous acknowledgement-bearing frames were lost or garbled. Whenever any acknowledgement comes in, the data link layer checks to see if any buffers can now be released. If buffers can be released (i.e., there is some room available in the window), a previously blocked network layer can now be allowed to cause more network layer ready events.`

  - Protocol 5 的时间流程：

     <img src="draft_fig\protocol_5_timeslot.png" alt="protocol 5 时间流程" style="zoom: 67%;" />

- protocol 6 (Protocol using selective repeat )

  - assumptions:
    - ~~error free (no damaging and losing frame )~~ ==error or damaging  may happen in transit== (so frame can be damaged or lost )
    - ~~without considering flow-control~~ (considering that frame sending may be faster than the receiver able to process) 
    - ~~one direction only (physical )~~ ~~half duplex (physical )~~ full duplex (physical )
    - ~~one direction only (logical : since one end is sending end, the other is receiving end )~~ bidirectional
    - ~~both(transmitting and receiving) network layers are always ready~~
    - ~~always have an **infinite supply of data** ready to send~~
    - ~~processing time can be ignored (on both sending and receiving end )~~ Transmission and processing time can't be ignored  
    - ~~infinite buffer space~~ 
    - ~~there is always reverse traffic (because in this code there isn't a timer for ack, so when there is no reverse traffic, the ack can't send back to the sender )~~ 

  - improvement :
    - a better window sequence number size 
    - NAK frame (to notice the frame_expected not acknowledged, improve the efficiency )
    - start_ack_timer() (improve the efficiency regardless of the reverse traffic )