# Wastewater Network Designer

A lightweight, browser-based sketchpad for sizing small wastewater networks. Build networks by dropping fixtures and nodes on the canvas, connect them with pipes, and size diameters using a k·√ΣDU flow calculation.

## Node palette
- **Source (fixtures):** Place individual fixtures that emit design units (DU). Default catalog entries include WC (2.5 l/s, DN110), Lavabo (0.5 l/s, DN40), Bidè (0.5 l/s, DN40), Doccia (0.8 l/s, DN50), Vasca (0.8 l/s, DN50), Lavastoviglie (0.8 l/s, DN50), Lavatrice (0.8 l/s, DN50), and Lavello (0.8 l/s, DN50). Fixtures can be renamed and swapped from the inspector.
- **Destination:** Terminal node for collecting flows. An optional design flow can be entered in the inspector.
- **Two-way split:** Merge up to two incoming pipes into one outgoing pipe.
- **Three-way split:** Merge up to three incoming pipes into one outgoing pipe.

## Connection rules
- Pipes run **from outputs to inputs only**. Sources expose an output on the right; destinations expose an input on the left; split nodes expose multiple inputs on the left and a single output on the right.
- Begin a connection by clicking an output port, then click the desired input port. Split nodes enforce their maximum input count (two or three). Duplicate self-connections are blocked.
- To remove items, select the pipe/node and use **Delete** in the inspector, the **Delete selected** shortcut, or **Clear all** to reset the canvas.

## Flow and diameter logic
- Enter a **k-factor** in the header (default 1.0) and press **Recompute flows** to apply the calculation.
- Source nodes adopt the flow and base diameter of their selected fixture. All other nodes compute outgoing flow as **k·√ΣDU**, where ΣDU is the sum of incoming flows.
- WC influence propagates downstream: any pipe carrying WC load is flagged and forced to **DN110**. Non-WC pipes take the larger of the source fixture diameter or a DN picked from flow: Q<0.5 ➝ DN40; 0.5–<0.8 ➝ DN50; 0.8–<1 ➝ DN63; 1–<1.5 ➝ DN75; 1.5–<2 ➝ DN80; 2–<2.25 ➝ DN90; ≥2.25 ➝ DN110.
- Edge labels show `flow l/s · DN` and stroke thickness scales with diameter. WC-carried edges use a cyan arrowhead.

## Working with the canvas
1. Pick a node type from the **Palette**, then click the canvas to place it. Drag nodes to reposition them.
2. Click an output port (right side) then an input port (left side) to draw a pipe. Click a pipe or node to inspect it.
3. In the **Inspector**, rename nodes, change fixture types, set destination design flows, and delete items. Pipe details display flow, diameter, and WC status.
4. Use the k-factor control and **Recompute flows** to update sizing after edits.

## Demo scene
The page opens with a sample network: two sources feeding a two-way split, which then connects to a destination. Use it as a starting point or clear and rebuild.

## Quick start
1. Clone or download this repository.
2. Open `index.html` in any modern browser (double-click the file or serve the folder with a simple HTTP server).
3. Adjust the k-factor if needed, place/modify nodes and pipes, then recompute flows to size the network.
