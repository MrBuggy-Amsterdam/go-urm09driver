# go-urm09driver

This is a Go module useful for controlling the URM09 ultrasonic ranging sensor on a Raspberry Pi or similar devices. The board is controlled over i2c.

> **Note**: this driver is by no means done or fully tested. 

## Installation

```bash
go get github.com/MrBuggy-Amsterdam/go-urm09driver
```

## Usage

After initializing the sensor on a specific **bus** (the i2c device used) and **address** (0x11 by default) you will have access to the `ReadDinstance()` function and can also enable passive mode as shown below (See the [official docs](https://wiki.dfrobot.com/URM09_Ultrasonic_Sensor_Gravity_Trig_SKU_SEN0388)). 

```Go
package main

import (
    urm09 "github.com/MrBuggy-Amsterdam/go-urm09driver"
)

func main() {
	urm := urm09.Initialize(1, 0x11)

	// Enable passive mode for  on-demand ranging
	err := urm.EnablePassiveMode()
	if err != nil {
		// Do something with the error
	}

	distance, err := urm.ReadDistance()
	if err != nil {
		// Do something with the error
	}
}
```

## Troubleshooting

A good start is to use `i2cdetect` to scan your i2c bus and confirm that your device is connected. Also make sure to read the [official docs](https://wiki.dfrobot.com/URM09_Ultrasonic_Sensor_Gravity_Trig_SKU_SEN0388).

Open an issue or PR to let us know of any issues you encounter.