# rot8

## automatic display rotation using built-in accelerometer

Automatic rotate modern Linux desktop screen and input devices. Handy for
convertible touchscreen notebooks like the Kaby Lake model of the HP Spectre x360.

Compatible with [sway](http://swaywm.org/) and [X11](https://www.x.org/wiki/Releases/7.7/).

## Build

Rust language and the cargo package manager are required to build the binary.

```
$ git clone https://github.com/spezifisch/rot8
$ cd rot8 && cargo build --release
$ cp target/release/rot8  /usr/bin/rot8
```

## Sway Configuration

For Sway map your input to the output device:

```
$ swaymsg <INPUTDEVICE> map_to_output <OUTPUTDEVICE>
```

Call rot8 from sway configuration file ~/.config/sway/config:

```
exec rot8
```

## X11 Configuration

For X11 set Touchscreen Device

```
rot8 --touchscreen <TOUCHSCREEN>
```

## Usage

There are the following args.

```
--sleep // Set sleep millis (500)
--display // Set Display Device (eDP-1)
--touchscreen // Set Touchscreen Device X11 (ELAN0732:00 04F3:22E1)
--keyboard // Set keyboard to deactivate upon rotation
--threshold // Set a rotation threshold between 0 and 1 (0.5)
--x-file // Manually specify file for x direction of accelerometer
--y-file
--x-invert // Invert x direction of accelerometer
--y-invert
--scale // Scale factor to bring raw accelerometer values into range [-1.0; 1.0]
```

## Examples

### Lenovo Duet

```
rot8 --display DSI-1 --threshold 0.97 --x-file '/sys/bus/iio/devices/iio:device1/in_accel_y_raw' --y-file '/sys/bus/iio/devices/iio:device1/in_accel_x_raw' --scale 0.00011400952 --y-invert
```

Using the scale factor in `/sys/bus/iio/devices/iio:device1/scale` leads to values up to about `10.5`. Dividing the value in that file by that number leads to the scale factor used in this example.

