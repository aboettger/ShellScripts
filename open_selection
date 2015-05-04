#!/bin/bash
selected_text=$(xclip -o)
if [[ "$selected_text" == ~* ]]; then
    file_name=$(readlink -f ${selected_text/\~/$HOME})
else
    file_name="$selected_text"
fi

notify-send "Open selection" "$file_name"
xdg-open "$file_name"
