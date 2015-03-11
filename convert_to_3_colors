#!/bin/bash
shopt -s nullglob
for file in *.png
do
        convert "$file" +dither -colors 3 -quality 100 -type bilevel "3colors.$file"
done
