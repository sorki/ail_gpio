all-is-lost gpio
================

Small bash wrapper over kernels GPIO sysfs interface.

Usage
-----


Clone and test::

        git clone https://github.com/sorki/ail_gpio
        cd ail_gpio/

        source ail_gpio
        output 4
        lo 4
        hi 4

        toggle 4
        echo "State of pin 4 is $( value 4 )"

        input 4
        value 4
        poll 4

        # poll can take additional parameter - a script to be called when
        # change occurs
        poll 4 handle

        # you can pass multiple pins to output, input, lo, hi and toggle
        pins="4 5 6"
        output $pins
        lo $pins
        toggle $pins

You can select different `gpiochip` by calling::

        gpiochip_base <ID>

For example on recent Linux kernel (4.17) and Raspberry Pi3 there are two gpiochips,
one providing access to `BCM283x` GPIO (`gpiochip1994`, address `3f200000`) and the second
one for `FXL6408` GPIO expander (`gpiochip1986`)::

        [root@nixos:]# ll /sys/class/gpio/
        total 0
        --w------- 1 root root 4096 Jul  5 19:50 export
        lrwxrwxrwx 1 root root    0 Jan  1  1970 gpiochip1986 -> ../../devices/platform/soc/soc:firmware/soc:firmware:gpio/gpio/gpiochip1986
        lrwxrwxrwx 1 root root    0 Jan  1  1970 gpiochip1994 -> ../../devices/platform/soc/3f200000.gpio/gpio/gpiochip1994
        --w------- 1 root root 4096 Jan  1  1970 unexport

To use the `BCM283x` GPIO in this case we call::

        source ail_gpio
        gpiochip_base 1994

This project was created to assist with GPIO on mainline Linux kernel which
in case of RaspberryPi uses different pin numbering, for mapping see the following
picture http://www.pighixxx.net/2015/06/raspberry-pi-v2-mod-b-pinout/

As we are limited by bash we cannot call `tell` or `select` to handle interrupts so we are
limited to polling pin state manually.
For a small C library that handles interrupts check out https://github.com/larsks/gpio-watch
