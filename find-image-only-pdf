#!/bin/bash
#

shopt -s nullglob
shopt -s nocaseglob

# Enable alias expansion in command substitution
shopt -s expand_aliases

red="\e[0;31m"
green="\e[0;32m"
yellow="\e[0;33m"
TOA="\e[0m" # No Color

# Vefify that we have gettext available
gettext "Bye." &> /dev/null
if [ $? -gt 0 ]; then
  alias ck_gettext="echo -e"
else
  alias ck_gettext="gettext -s --"
fi

# Prints OK or FAILED! depending on previous command return value
function okfail () {
  if [ $? -gt 0 ]; then
    logError "There was an error. Aborting."
    return 1
  else
    logInfo "OK"
    return 0
  fi
}

function logInfo () {
    echog "${green}$1${TOA}"
}

function logWarn () {
  echog "${yellow}$1${TOA}"
}

function logError () {
  echog "${red}$1${TOA}"
}

## echo with newline at the end
function echog() {
  local format="$1"
  shift
  printf -- "$(ck_gettext "$format")\n" "$@" >&2
}

find "$1" -depth -type f -name "*.pdf" | { while read -r path;
do
  logInfo "Processing \"$path\""
  a=$(tempfile)
  pdftotext "$path" "$a"
  lines=$(wc -l < "$a")
  # echo "$a -> $lines"
  if [ "$lines" == "0" ]
  then
    echog "${yellow}no text found${TOA}"
  fi
  echo
done
}
