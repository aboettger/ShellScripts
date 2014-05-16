#!/bin/bash
#
# Dreht ein Video um 90° im Uhrzeigersinn
#
# 0 = 90CounterCLockwise and Vertical Flip (default)
# 1 = 90Clockwise
# 2 = 90CounterClockwise
# 3 = 90Clockwise and Vertical Flip

function errorexit
{
  echo "$1" 1>&2
  exit 1
}

usage="Usage: $0 [-d 0|1|2|3] file"
transpose=0

while getopts 'd:h' opt ; do
  case "$opt" in
    d)   transpose="$OPTARG";;
    h)  echo "$usage"
    exit 0;;
    [?]) echo "$usage"
    exit 2;;
  esac
done
shift $(($OPTIND-1))

if [ "$1" == "" ]
then
  errorexit "Zu drehendes Video angeben. Abbruch."
elif [ ! -f "$1" ]
then
  errorexit "\"$1\" ist keine Datei. Abbruch."
fi

directory=$(dirname "$1")
filename=$(basename "$1")
filenameWithoutSuffix=${filename%.*}
suffix="${filename##*.}"

newFilename="$filenameWithoutSuffix.rotated.$suffix"
echo $newFilename

ffmpeg -i "$directory/$filename" -vf "transpose=$transpose" "$directory/$newFilename"

exit 0

