#!/bin/bash

title=$(pdfinfo "$1" | grep "Title" | awk '{sub(/[^ ]+ /, ""); print $0}' | sed 's/^[ \t]*//;s/[ \t]*$//')
author=$(pdfinfo "$1" | grep "Author" | awk '{sub(/[^ ]+ /, ""); print $0}' | sed 's/^[ \t]*//;s/[ \t]*$//')

values=$(yad \
  --center \
  --selectable-labels \
  --form \
  --text="The changes are made ​​to this file:\n$1" \
  --text-align=center \
  --columns=2 \
  --class="pdfmetadata-gui" \
  --name="PDF Metadata GUI" \
  --title="$(basename "$0") - $1" \
  --center \
  --width=400 \
  --separator="~/~" \
  --field=Title \
  "$title" \
  --field=Author \
  "$author" \
  --field="Update":CHK \
  "TRUE" \
  --field="Update":CHK \
  "TRUE" \
)
[[ -z "$values" ]] && exit 1

newTitle=$(echo "$values" | awk -F "~/~" '{print $1}')
newAuthor=$(echo "$values" | awk -F "~/~" '{print $2}')

updateTitle=$(echo "$values" | awk -F "~/~" '{print $3}')
updateAuthor=$(echo "$values" | awk -F "~/~" '{print $4}')

[[ $updateTitle == "TRUE" ]] && exiftool -overwrite_original -Title="$newTitle" "$1"
[[ $updateAuthor == "TRUE" ]] && exiftool -overwrite_original -Author="$newAuthor" "$1"

exit 0
