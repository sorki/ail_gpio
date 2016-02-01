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

        input 4
        value 4
        poll 4

        # poll can take additional parameter - a script to be called when
        # change occurs
        poll 4 handle
