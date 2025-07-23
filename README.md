# ALS162 time signal receiver

This project will refresh F5RCT's time signal receiver, frequency standard.

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

## Alarm conditions
### Loss of continuous operation
Critical alarm
  - Happens when the internal clock loses its power supply.
  - This condition can self-clear, once the built-in clock has completed its warmup phase, PPS has locked, and a valid signal is received.
  - On Rev 2, continuous operation condition can be restored from the external GNSS source (jumpstart).

### PLL Unlock
Minor alarm
  - Happens when the reference signal is lost
  - This condition can self-clear, once reception is restored, and a valid signal has been received.

### External reference loss (Rev 2)
Minor alarm
  - Happens when no valid PPS signal is received
  - This condition can self-clear once continuous operation has been established.
