
# floorplanning 

## Definition: Floorplanning is the process of allocating space, determining the shape and size of the chip, and defining the precise locations of the major functional blocks (macros, I/O pads, etc.) before the standard cells (logic gates) are placed.

### there are different areas in the floorplaning

- Die Area: The total physical area of the silicon chip.
- Core Area: The inner region where all the logic (standard cells and macros) is actually placed. Its size is determined by the required Core Utilization (usually 70%-85%), which is the ratio of standard cell area to the available core area.

### I/O Pad / Pin Placement:
- I/O (Input/Output) pads are placed around the periphery (edge) of the die. They are the        communication bridge between the chip's internal logic and the outside world.

### Macro Placement:

- Macros are large, pre-designed blocks like SRAM (memory), PLLs, or custom IP (Intellectual Property).

- Macros take up huge amounts of space and their placement is strategic: they should be placed close to the logic they communicate with to minimize wire length (using a guide called flylines), and they must be positioned to avoid congestion.


### Standard Cell Row Creation:

- The core area is divided into horizontal rows where the standard cells (basic logic gates) will be placed and powered.

### Power Planning (PDN):

- This is highly critical! You must create the Power Distribution Network (PDN)—a grid of thick metal straps (VDD and GND)—to deliver stable power to every part of the chip. A weak PDN leads to IR Drop (voltage sag), which causes timing failures.

### Adding Physical-Only Cells:

- Tap Cells (like the TAPCELL_X1 that caused your error) are special cells inserted into the standard cell rows to maintain substrate integrity and prevent latch-up.

- Endcaps are placed at the ends of rows.

- Blockages are defined to reserve areas for future logic or to keep standard cells away from macro pins to avoid congestion.

### Inshort A good floorplan minimizes wire length, balances power, and prevents congestion, making the subsequent steps of placement and routing much easier and faster to complete.










