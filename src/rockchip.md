# Rockchip

## RK3588

The boot ROM uses the internal 12-bit 1MS/s SARADC to read `SARADC_IN0_BOOT` on
power. It selects a boot mode based on the following table:

| ADC value | Voltage | Mode |
|-----------|---------|------|
|         0 |       0 | USB  |
|       682 |     0.3 | SD card, USB |
|      1365 |     0.6 | eMMC, USB |
|      2047 |     0.9 | FSPI M0, USB |
|      2730 |     1.2 | FSPI M1, USB |
|      3412 |     1.5 | FSPI M2, USB |
|      4095 |     1.8 | FSPI M2, FSPI M1, FSPI M0, eMMC, SD card, USB |

It will search each device in the order listed above for a valid image.

`SARADC_IN0_BOOT` is often routed to a button, which when pressed is connected
to ground (i.e. 0 V) and otherwise is 1.8V.

Additional channels of the ADC may be routed to jumper headers to be used by
later boot loader stages.
