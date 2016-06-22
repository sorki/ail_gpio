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
