#!/bin/bash
#screenWidth=$(xdpyinfo | grep dimensions | grep -o '[0-9]*' | head -n1)

#width=$(xdotool getactivewindow getwindowgeometry --shell | head -4 | tail -1 | sed 's/[^0-9]*//')
height=$(xdotool getactivewindow getwindowgeometry --shell | head -5 | tail -1 | sed 's/[^0-9]*//')

xdotool getactivewindow windowsize 75% "$height"

exit 0
