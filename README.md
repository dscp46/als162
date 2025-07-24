# ALS162 time signal receiver

This project will refresh F5RCT's time signal receiver[^1], frequency standard, using the 162kHz French legal time signal[^3], [^4].
Comments from Hervé QUILLEVERE[^2] have also been taken in account, during the development of this project.

Henning Maier has written an interesting paper for GRcon23[^5]. In the associated presentation, the author [quickly covers the unspecified part of the signal](https://www.youtube.com/watch?v=tjkMXNVhhnU&t=126). On top of his remarks, it appears this part contains an equal amount of positive and negative phase symbols, such that the long-term average phase stays near zero. Further work needed, once the baseline receiver is built.

## System design documents
  - [ALS162 Time Signal](doc/als162_waveform.md)
  - [Clock architecture](doc/Clock_Architecture.md)
  - [Serial Protocol Specification](doc/proto.md)
  - [Alarm conditions](doc/Alarms.md)

## TODO/Feature list
### Rev 1
  - [ ] Power supply revamp, using low noise buck converters (10.5~30V input?)
  - [ ] Fuse/Polyfuse PSU protection
  - [ ] ESD / Lightning protection
  - [ ] 10 MHz Output
  - [ ] PPS Output
  - [ ] Serial Output (PPS on DCD, alarm on /DSR), NMEA on RS232 line?
  - [ ] Built-in Bias-T
  - [ ] Distance input to adjust PPS shift
  - [ ] DIP -> User-solderable CMS?
  - [ ] DCF77 receiver compatible output
  - [ ] System alarms
    - [ ] Loss of continuous operation (Critical)
    - [ ] PLL unlocked (Major)

Nice to haves
  - [ ] Backup battery for continuous operation. (Modular BMS?)
  - [ ] Built-in S-Meter measurement (via MCU) 

### Rev 2
  - [ ] Modular frequency generator?
  - [ ] GNSS receiver Add-in card? / Ext GPSDO input (PPS+NMEA)?
  - [ ] PPS shift auto-adjust based on ext PPS

## Citations
[^1]: [Construisez un récepteur de fréquence étalon et de signaux horaires sur France Inter 162kHz](doc/200103_signal_horaire_france_inter.pdf), F5RCT
[^2]: [Récepteur Horaire France Inter](https://www.rvq.fr/tech/fi.php), Hervé QUILLEVERE
[^3]: [Diffusion de l'heure par codage de la phase d'un émetteur de radiodiffusion à modulation d'amplitude](doc/l_onde_electrique_vol60_n10_1980.pdf), A. Gabry, L'onde électrique 1980, vol. 60, n°10
[^4]: ["France Inter" - L'émetteur Français de fréquence étalon et de signaux de temps codé](doc/bulletin_bnm_no63-64_p120_1986.pdf), B. Dubouis, Bulletin BNM, n°63, 1986
[^5]: [ALS162 Time Signal SDR Receiver for GNU Radio](https://pubs.gnuradio.org/index.php/grcon/article/view/134), Henning MAIER, Proceedings of the GNU Radio Conference, sep. 2023. [Associated slides](https://events.gnuradio.org/event/21/contributions/415/attachments/139/320/ALS162_slides_henningM1r.pdf)
