# Tmux Tutorial
## Session
```
tmux new -s <session-name>
tmux detach //Ctrl+b d
tmux ls //tmux list-session //Ctrl+b s
tmux attach -t 0 //tmux attach -t <session-name>
tmux kill-session -t 0 //tmux kill-session -t <session-name>
tmux switch -t 0 //tmux switch -t <session-name>
tmux rename-session -t 0 <new-name> //Ctrl+b $
```
## Window
```
tmux split-window //up and down Ctrl+b "
tmux split-window -h //left and right  Ctrl+b %
tmux new-window (-n <window-name>) //Ctrl+b c
tmux select-window -t <window-number>/<window-name> //Ctrl+b p/n/<number>/w
tmux rename-window <new-name> //Ctrl+b ,

```
## Mouse
```
tmux select-pane -U  
tmux select-pane -D  
tmux select-pane -L
tmux select-pane -R
Ctrl+b <arrow key>
```
## Swap Pane
```
tmux swap-pane -U
tmux swap-pane -D
Ctrl+b {: to left
Ctrl+b }: to right
Ctrl+b x: close
Ctrl+b !: to a single window
Ctrl+b z: maximum or exit maximum
Ctrl+b Ctrl+<arrow key>: change size
Ctrl+b q: show number
```
## Others
```
tmux list-keys
tmux list-commands
tmux info
tmux source-file ~/.tmux.conf
```
