# Routing algorithm

- decide which output line(Software part)
- distinction between "routing" and "forwarding"
- desired properties:
  - correctness
  - simplicity
  - robustness
  - stability:a stable algorithm should quickly reaches equilibrium and stays there
  - fairness and efficiency(tradeoff)
    - what is we seek to optimize:
      - mean packet delay
      - total network throughput
      - overall hops
- nonadaptive algorithm (static routing) and adaptive algorithm (dynamic routing)
- discussion in this section is mainly based on topology
## 5.2.1 The optimiality principle
如果从源点S到终点T有一条最短路径，该路径途径点A和B，则该段子路径是A到B的最短路径。

构造`sink tree`

## 5.2.2 Shortest Path algorithm

- Dijkstra Algorithm

## 5.2.3 Flooding
