#!/bin/bash
notify-send --hint int:transient:1 "$(basename "$0")" "start ($1)"

"$HOME"/bin/extract_and_write_keywords_into_calibre "$1"

notify-send --hint int:transient:1 "$(basename "$0")" "finished ($1)"
