# Alarm conditions

## Loss of continuous operation
Critical severity
  - Happens when the internal clock loses its power supply.
  - This condition can self-clear, once the built-in clock has completed its warmup phase, PPS has locked, and a valid signal is received.
  - On Rev 2, continuous operation condition can be restored from the external GNSS source (jumpstart).

## PLL Unlock
Minor severity
  - Happens when the reference signal is lost
  - This condition can self-clear, once reception is restored, and a valid signal has been received.

## Loss of primary power supply
Major severity
  - Happens when the device runs on its internal battery.
  - Self-clears on main power restoration.

## External reference loss (Rev 2)
Minor severity
  - Happens when no valid PPS signal is received
  - This condition can self-clear once continuous operation has been established.
