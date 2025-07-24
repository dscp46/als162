# Clock architecture
Using the ATMega328, it is possible to accurately generate the 1PPS signal, by exclusively relying on hardware and timers.

The firmware is left the task to adjust the 1PPS event timing and time signal management.

```mermaid
flowchart LR
    CLK@{ shape: hex, label: "VCOCXO"} -->|20MHz| D2[ /2<br>74HC393 ]
    D2 --> 10M> 10MHz Out ]
    D2 -->|10MHz| uC_CLK
    
    CLK --> D125[ /125<br>74HC390 ]
    D125 -->|160 kHz| MIX@{ shape: cross-circ }
    ALS162@{ shape: hex, label: "ALS162"} -->|162kHz| MIX
    MIX -->|2kHz| PLL(PLL)
    D125 -->|160 kHz| D80[ /80<br>74HC390+3 ]
    D80 -->|2kHz| PLL
    PLL -->|Δφ| CLK
    PLL -->|Δf| uC

    subgraph ATMega328
    uC_CLK -->|10MHz| T2
    uC[ µC code ] -->|Set tick| T1
    T2[ /200<br>Timer2 ] -->|50 kHz| T1[ Timer1 ]
    end

    T1 --> PPS> 1PPS Out ]
```
