# Building a Mechanical Keyboard from Scratch

## 1. Ergopad for Hand Mapping

Use Ergopad to create a hand map on your iPad: [Ergopad](https://pashutk.com/ergopad/)

## 2. Ergogen for Key Placement on PCB

[Ergogen](https://ergogen.cache.works/) takes the key positions from Ergopad and places them on a PCB.

1. The tool allows you to define key spacing, margin, key size (MX/Chock), and reset button configuration.
2. Define columns and rows (in our case, 5 columns with 3 rows). The thumb is also treated as a column, which we rotate.
3. You can adjust how much each column is staggered and rotated.
4. Fine-tune the parameters:
    - `stag`: defines stagger height.
    - `spaly`: defines the positive or negative angles.
    - You can create matrix subparts, e.g., one matrix for the 5 finger columns and one for the thumb column.
5. Draw key outlines to ensure no overlap.
6. Draw the base as a polygon:
    1. Start from the pinky top and create a margin.
    2. You can add a fillet (curve instead of sharp corner).
    3. Widen the base for the case and define the bottom wall.
7. This tool exports:
    1. Raw PCB: `.pcb` format.
    2. 3D model for the case.
8. The "combo" includes the PCB + holes + key combinations.

## 3. Keycap Considerations

Be mindful that key sizes depend on keycap size, which may be larger than the key itself. With high-quality keycaps, it’s recommended to use the keycap size.

## 4. Case Design Considerations

After designing the wall, focus on details such as adding cutout points for USB connectors or connections between the keyboard halves. You can edit the STL or other 3D printing formats post-production.

**Caution**: The mirror function treats the design as one PCB and one case. It’s better to repeat the procedure for the other hand for precision, as hand sizes may differ.

## 5. PCB in KiCad

Open the exported PCB in KiCad:

1. Logical lines show which pins need to connect to the microcontroller.
2. There are two layers: front and bottom. Each hole connects the front and bottom layers.
3. Since traces cannot overlap, use both front and bottom layers.

## 6. Routing in KiCad

KiCad has a tool for routing traces, ensuring that each pin connects correctly to the microcontroller.

- Ground fills: Areas without signal traces are filled with ground to dissipate heat and shield radiofrequency components.
- You can define ground areas on both the front and back layers.

## 7. DRC (Design Rule Check) in KiCad

KiCad's DRC tool checks for electrical rule compliance. Focus on errors, not warnings.- Errors include: insufficient space, unconnected pins, etc. Fix these issues.- Some pins may have nearby ground connections that need to be linked.

## 8. Adding Components

After fixing DRC errors, add missing components (e.g., switch keys).

## 9. Two-Layer Limitations

If two layers aren’t enough to prevent trace overlap, you can add vias (PCB holes) to move lines from the top to the bottom layer.

## 10. KiCad Gerber Export

KiCad exports a Gerber file, which is sent to the PCB manufacturer.

- Gerber includes: front and bottom layers, paste for solder, conductive pads, and a silk layer for text or drawings.
- Layers to export:
  - Silk
  - Copper (CU)
  - Paste
  - Mask
  - FAB (board)
  - edge.cuts
- Generate a drill file for holes and submit everything to the manufacturer for review.
