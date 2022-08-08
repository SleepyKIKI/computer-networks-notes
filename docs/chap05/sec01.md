#Network layer design issue

##5.1.1 Store-and-forward packet switching

##5.1.2 Services provided to the transport layer

- 3 goals:
  - Independent of the router technology
  - shield transport layer from the number, type, and topology of the router system
  - use a uniform numbering plan
- 2 camps:
  - connection-oriented
    - example: X.25, Frame Relay, ATM
    - Internet目前也正在向connection-oriented方向发展，使用的技术：MPLS, VLANs
  - connectionless
    - example: ARPANET
##5.1.3 Implementation of connectionless Service
- datagram network
  - datagrams
- 每个路由器内部都有一个表：当一个带有目的地址的packet到达时，该表指示应该送去哪个邻接的路由器
- routing algorithm
  - 管理路由表，做出路由选择的算法
- example protocol: IP
##5.1.4 Implementation of connection-oriented Service
- VC network (Virtual Circuit network)
- 在进行分组交换前，建立Virtual Circuit
- label switching
- example protocol: MPLS
##5.1.5 Comparison of virtual-Circuit and datagram network
- some important issue:
  - setup time vs address parsing time
  - destination addresses is longer than Circuit index
  - VC is better in guaranteeing quality of service and avoiding congestion
  - VC is more vulnerable
