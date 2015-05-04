#!/bin/bash

# if the session is already running, just attach to it.
tmux has-session -t 4panel
if [ $? -eq 0 ]; then
  sleep 1
  tmux attach -t 4panel
else 
  tmux new-session -d -s 4panel
  tmux split-window -v
  tmux split-window -h
  tmux select-pane -t 0
  tmux split-window -h
  tmux select-pane -t 0
  tmux -2 attach-session -d
fi
