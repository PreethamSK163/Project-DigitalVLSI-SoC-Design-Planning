
# Global & Detailed Routing
> PicoRV32a — OpenLANE Physical Design Flow

![Tool](https://img.shields.io/badge/Tool-FastRoute-blue)
![Tool](https://img.shields.io/badge/Tool-TritonRoute-blue)
![PDK](https://img.shields.io/badge/PDK-Sky130-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

<h2>🔍 Overview</h2>

- Performed global routing using **FastRoute** — approximate signal paths planned across the G-cell grid to guide detailed routing.
- Completed detailed routing using **TritonRoute** — exact metal shapes and vias placed with full DRC compliance. Iterative optimisation passes reduced violations to zero.

<h2>⚙️ Tasks Covered</h2>

| Task | Description |
|:---|:---|
| Global Routing | FastRoute — approximate path planning across G-cell grid |
| Detailed Routing | TritonRoute — exact metal shapes, vias, DRC compliance |
| DRC Verification | Iterative passes until zero DRC violations achieved |

<h2>📊 Key Observations</h2>

| Metric | Details |
|:---|:---|
| Global Router | FastRoute |
| Detailed Router | TritonRoute |
| Routing Strategy | Honours pre-processed route guides from global routing |
| DRC Violations | 0 — DRC clean after iterative optimisation |
| Output | picorv32a.routed.def |

<h2>📝 Stage Details</h2>

**Global Routing** &nbsp;|&nbsp; `FastRoute` `G-cell Grid` `Route Guides`

FastRoute executed — die divided into G-cell grid. Approximate routing paths planned for all signal nets, respecting metal layer capacity and congestion constraints. Route guides generated as input to detailed router — each guide specifies preferred metal layer and approximate path for every net.

**Detailed Routing** &nbsp;|&nbsp; `TritonRoute` `Metal Shapes` `Via Placement`

TritonRoute executed — exact metal wire shapes and via placements determined for every net following route guides from FastRoute. Inter-guide connectivity ensured at all layer transitions. DRC rules enforced throughout — spacing, width, and via enclosure rules applied. Iterative optimisation passes performed until zero DRC violations achieved. Routed DEF generated at `results/routing/picorv32a.routed.def`.

<h2>🖼️ Implementation Results</h2>

### Global & Detailed Routing
![Routing 1](1_Basics_of_global_and_detail_routing_and_configure_TritonRoute_1.png)
![Routing 2](1_Basics_of_global_and_detail_routing_and_configure_TritonRoute_2.png)
![Routing 3](1_Basics_of_global_and_detail_routing_and_configure_TritonRoute_3.png)
![Routing 4](1_Basics_of_global_and_detail_routing_and_configure_TritonRoute_4.png)

<h2>🔗 Navigation</h2>

[Back to Repository Overview](../README.md) &nbsp;|&nbsp; [Previous : 07 : PDN](../07%20:%20PDN) &nbsp;|&nbsp; [Next : 09 : GDSII](../09%20:%20GDSII)
