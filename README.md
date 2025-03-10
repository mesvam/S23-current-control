# Purpose
These scripts facilitate reading and writing max77705 registers to view and change various system currents not exposed under `/sys/class/power_supply/battery` on Galaxy S23 (model SM-S911B, codename dm1q). Root is required.

# Explanation
Galaxy S23 uses the max77705 IC for charging. It controls everything from USB current, battery charging current, SoC estimation, and more. Not all parameters are directly exposed by the Samsung kernel via the sysfs interface at `/sys/class/power_supply/battery`, but other parameters can be read and modified using register values from `/sys/class/power_supply/max77705-charger/data` and `/sys/class/power_supply/max77705-fuelgauge/fg_data`.

# Usage examples

Get max battery charging current in mA

    > get-max-charge-current-s23
    3750

Set max battery charging current to 500 mA

    > set-max-charge-current-s23 500
    a

Get USB current in uA

    > get-usb-current-s23
    33750

Set USB current limit to 1000 mA

    > set-max-usb-current-s23 1000
    27

# Notes
`get-avg-system-current-s23` is only valid for the Galaxy S23; it will return incorrect results on other variants like S23+, S23 Ultra, or S23 FE. Each model has slightly different hardware (different current sense resistor values), making some of the formulas different. Check the kernel source code to adapt scripts to your specific device model.
