
## 🛜Routing 

## Maze Routing – Lee’s Algorithm (1961)
<img width="1752" height="752" alt="Screenshot 2025-10-31 144723" src="https://github.com/user-attachments/assets/d6430f8e-48ab-4980-850b-9dc7ff58acbd" />

1. Grid-Based Routing Area

The entire routing region is represented as a blue square grid.

Every small square represents a routing tile through which wires can move.

Movement is allowed in four directions: up, down, left, right (Manhattan routing).

2. Fixed Obstacles (DECAP Blocks)

Blocks named DECAP1, DECAP2, DECAP3, and functional blocks Block a and Block b act as obstacles.

These areas cannot be passed through by the routing algorithm.

Routing must go around them.

3. Source and Target Pins

Blue squares labeled 1 and 2 represent:

Source pin (starting point)

Target pin (ending point)

The algorithm must find a valid path between these two pins avoiding obstacles.

✅ 4. How Lee’s Algorithm Works (Simple Explanation)

Lee’s algorithm consists of two main phases:

(a) Wave Propagation

Start from the source pin.

Expand outwards, cell by cell, marking reachable grid points with an increasing “wave number.”

Propagation continues until the target pin is reached.

(b) Traceback

Once the wave reaches the target, the algorithm backtracks along the decreasing wave numbers.

This gives the shortest possible path between source and target.

✅ Guarantees shortest path
✅ Guarantees a route if one exists
❌ Can be slow for large grids

✅ 5. Significance in VLSI Routing

Used as a gold standard for routing correctness.

Still influences modern algorithms like A* search and global/detail routing engines.

Ensures wires avoid forbidden zones like macros, decaps, and blockages.

<img width="1603" height="774" alt="Screenshot 2025-10-31 145041" src="https://github.com/user-attachments/assets/d460d505-864a-4a06-ab14-212b59a06508" />

The blue grid represents the routing area where each cell can be visited by the router.

The grey blocks (DECAP1, DECAP2, DECAP3, Block a, Block b) act as obstacles that the router must avoid.

The blue square labeled T2 is the target pin to which the source must connect.

The numbers (1,2,3…) written on the grid represent wavefront expansion levels:

1 = first expansion step

2 = second expansion step

3 = third step

These numbers show how the routing algorithm spreads outward from the source until it reaches the target.

Lee’s algorithm uses this method to guarantee a shortest path around obstacles.

What This Step Represents

✅ Wave propagation phase
✅ Grid cells are labeled with increasing integers as the wave expands
✅ Obstacles block propagation
✅ Routing continues until the wave reaches T2

<img width="1805" height="766" alt="Screenshot 2025-10-31 151348" src="https://github.com/user-attachments/assets/7a4eec84-399f-48b9-9209-e60c05801c56" />


## Routing (Step 5): Detailed Explanation
<img width="1713" height="747" alt="Screenshot 2025-10-31 151425" src="https://github.com/user-attachments/assets/7698c273-2d74-4475-8b6d-b650375eb17a" />

1. Multi-Layer Routing

- Different colors represent wires routed on different metal layers.

- Routing uses preferred directions (horizontal/vertical) to reduce congestion and shorts.

- Vias are inserted wherever a net changes metal layer.

2. Signal Routing

- Each input pin (Din1, Din2, Din3, Din4) is routed to the corresponding FF1 block.

- The combinational logic (gates 1 and 2) and buffers are connected in between.

- Output paths from FF2 reach Dout1, Dout2, Dout3, and Dout4.

3. Clock Routing

- Two clock inputs (CLK1, CLK2) feed multiple flip-flops.

- Buffers (Buf) are placed along clock paths to balance delay and reduce skew.

- A dedicated ClkOut line is also routed through the design.

4. Avoiding Blockages

- Large obstacle blocks (DECAP1, DECAP2, DECAP3, Block a, Block b) force the router to:

Detour around obstacles

- Use vertical/horizontal tracks efficiently

- Maintain DRC-clean spacing

5. Buffer Insertion

- Red boxes labeled Buf represent buffers added:

- To reduce long wire delay

- To strengthen signal drive

- For timing closure (setup/hold fixes)

6. Logical Net Mapping (Right Side Diagram)

- The small diagram on the right shows the logical connection graph.

- Each FF1 → logic → FF2 → Dout mapping corresponds exactly to the routed paths on the left.

- Ensures physical routing matches the intended RTL/netlist design.



### ✅ 6) DRC Clean – Explanation
<img width="1501" height="750" alt="Screenshot 2025-10-31 152521" src="https://github.com/user-attachments/assets/bb337115-fdf6-415f-b9b8-b2cd78924278" />


- This stage ensures that the entire routed layout follows all Design Rule Checks (DRC) defined by the foundry. After routing, the layout must be verified for spacing, width, enclosure, and via rules so the chip can be manufactured reliably.

1. Layout Completely Routed

- All data paths from Din1–Din4 → FF1 → logic → FF2 → Dout1–Dout4 are connected.

- Clock paths (CLK1, CLK2) and ClkOut are properly routed with buffers.

- Multiple metal layers are used without causing congestion.

2. Checking New Design Rules

- The yellow arrows highlight two key DRC checks:

(A) Via Spacing Rule

- Vias must have minimum spacing from each other to avoid:

- Metal bridging

- Shorts between layers

- Etching defects during fabrication

- The diagram on the right shows:

- Two vias with proper spacing

- No overlap between via enclosures

- Distance ≥ minimum technology-defined spacing

✅ (B) No Signal Short

DRC ensures:

- No two different nets overlap or touch

- No short circuits between timing, power, or signal nets

- Each net stays inside its routing track

- The highlighted FF1 → FF2 region shows that clocks and data signals pass close but do not short.

3. DRC Clean Layout

- Once all spacing, width, via, and short checks pass:

- The design is marked DRC clean

- Safe for next stages (LVS, STA, GDS export)



### 🖤 TritonRoute
<img width="1395" height="626" alt="Screenshot 2025-10-31 152822" src="https://github.com/user-attachments/assets/4edb53e7-b208-4e5f-87af-154dfc8a3365" />

- Performs the detailed routing stage, converting route guides into actual metal/via routes on the layout.

- Follows the preprocessed route guides generated during global/fast routing, ensuring wires stay inside their assigned routing regions.

- Assumes inter-guide connectivity, meaning each net’s guides are arranged so routing can continue smoothly from one guide segment to another.

- Uses a MILP-based panel routing approach, where:

- Intra-layer routing is done in parallel for efficiency, and

- Inter-layer routing is executed sequentially, coordinating via usage and layer transitions.




<img width="1320" height="723" alt="Screenshot 2025-10-31 154103" src="https://github.com/user-attachments/assets/5e074ffd-58db-4181-8525-ed238fa301d4" />

Intra-layer parallel & Inter-layer sequential panel routing

TritonRoute divides each metal layer into several routing panels.

Intra-layer routing is performed in parallel, meaning all panels on the same layer (e.g., M2) are routed simultaneously.

Inter-layer routing is done sequentially, routing one metal layer after another (M2 → M3 → M4 …).

On higher layers, even-indexed panels and odd-indexed panels are routed in alternating steps to avoid conflicts.

Each panel uses previously routed panels/layers as constraints to ensure DRC-clean routing.

Overall flow:

(a) Parallel routing of panels on M2

(b) Parallel routing of even-indexed panels on M3

(c) Parallel routing of odd-indexed panels on M3





<img width="1294" height="756" alt="Screenshot 2025-10-31 154514" src="https://github.com/user-attachments/assets/6fe2b1fa-8d43-4bfe-a87e-15c51154b031" />

Handling Connectivity – TritonRoute

Access Point (AP):
An on-grid point on the metal layer of the route guide.
It is used to connect to lower-layer segments, upper-layer segments, pins, or IO ports.

Access Point Cluster (APC):
A union/group of all Access Points that originate from the same lower-layer segment, upper-layer guide, pin, or IO port.

### Routing Topology Algorithm

<img width="1147" height="556" alt="Screenshot 2025-10-31 155101" src="https://github.com/user-attachments/assets/01128a79-7b76-428f-96c3-4b36737e0c0e" />

The algorithm optimizes routing topology using Access Point Clusters (APCs).

A nested loop is used to compute pairwise distances between all APCs.

For every APCᵢ (from i = 1 to n−1), the algorithm computes distances only with APCⱼ where j > i (to avoid duplicates).

The pairwise cost costᵢⱼ is computed as the distance between APCᵢ and APCⱼ → cost[i,j] = dist(APCᵢ, APCⱼ).

After all pairwise costs are computed, an MST (Minimum Spanning Tree) is constructed using APCs and the cost matrix.

The MST ensures minimum wiring cost and optimal routing connectivity.

The edges eᵢⱼ selected by the MST form the final routing topology and are returned as output.





