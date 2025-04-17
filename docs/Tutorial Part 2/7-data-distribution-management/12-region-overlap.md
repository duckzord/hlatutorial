---
sidebar_position: 12
---

# Region Overlap for the Checkerboard Case

Figure 7-15 shows an example of the overlap of the regions for the attributes of a car and a subscribing MapViewer that subscribes to the four top left squares.

![14-checkerboard-overlap.png](img%2F14-checkerboard-overlap.png)

The checkerboard view shows the logical overlap. Since the checkerboard approach transforms this to a one-dimensional dimension the actual HLA regions are shown in the bottom. When implementing the subscribing federate you can either subscribe using several point regions, or create larger regions.