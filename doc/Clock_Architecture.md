# Clock architecture
Using the ATMega328, it is possible to accurately generate the 1PPS signal, by exclusively relying on hardware and timers.
The 50kHz signal is transfered from `timer2` to `timer1` though a connection of `OSC2A` (PortB_3) to `T1` (PortD_5).

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
    PLL -->|Δf, PLL_LOCK| uC

    subgraph ATMega328
    uC_CLK -->|10MHz| T2
    uC[ µC code ] -->|Set tick| T1
    T2[ /200<br>Timer2 ] -->|50 kHz| T1[ /50k<br>Timer1 ]
    end

    T1 --> PPS> 1PPS Out ]
```

## Timer1 characteristics
Timer1 is set to:
  - Set OC1A High when it reaches `44999`.
  - Set OC1A Low and reset timer1 when it reaches `49999`.

## Sync modes
### Rough sync
Until the undocumented part content is reverse-engineed, a rough estimation of the 1PPS epoch is necessary.
Easiest way to do this is to rely on the 59th second, which is known to be unmodulated.

To do this, we measure the time to last interrupt. The first interrupt for which $`Δt > 500ms`$ is a good marker to set the epoch (don't forget to add the 50ms delay). 

### Fine sync
Once we're roughly synced, we can measure and store consecutive epochs (± a few samples), then adjust the epoch timer to mean value. More details to come.

### Propagation delay compensation
Compute the distance from your point of installation to `47.171585, 2.204646`. 

No need to get an up-to-the-meter precise location: the coordinates is the middle point between the two transmitting masts (1 being the active one, and the other being a reflector), which introduces a +/- 230 meters uncertainty (767ns), which is negligible, when compared to the epoch average uncertainty (~30µs/d according to Bulletin H[^1]).

[^1]: [Liste des bulletins H disponibles](https://syrte.obspm.fr/tfc/temps/outgoing_data/laboTAF/bulH/liste_bulh.php), LNE-SYRTE
