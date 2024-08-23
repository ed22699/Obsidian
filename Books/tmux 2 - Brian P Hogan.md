---
title: tmux 2
subtitle: Productive Mouse-Free Development
author: Brian P. Hogan
authors: Brian P. Hogan
category: Computers
categories: Computers
publisher: Pragmatic Bookshelf
publishDate: 2016-11-17
totalPage: 149
coverUrl: http://books.google.com/books/content?id=kA9QDwAAQBAJ&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api
coverSmallUrl: http://books.google.com/books/content?id=kA9QDwAAQBAJ&printsec=frontcover&img=1&zoom=5&edge=curl&source=gbs_api
description: Your mouse is slowing you down. The time you spend context switching between your editor and your consoles eats away at your productivity. Take control of your environment with tmux, a terminal multiplexer that you can tailor to your workflow. With this updated second edition for tmux 2.3, you'll customize, script, and leverage tmux's unique abilities to craft a productive terminal environment that lets you keep your fingers on your keyboard's home row. You have a database console, web server, test runner, and text editor running at the same time, but switching between them and trying to find what you need takes up valuable time and breaks your concentration. By using tmux 2.3, you can improve your productivity and regain your focus. This book will show you how. This second edition includes many features requested by readers, including how to integrate plugins into your workflow, how to integrate tmux with Vim for seamless navigation - oh, and how to use tmux on Windows 10. Use tmux to manage multiple terminal sessions in a single window using only your keyboard. Manage and run programs side by side in panes, and create the perfect development environment with custom scripts so that when you're ready to work, your programs are waiting for you. Manipulate text with tmux's copy and paste buffers, so you can move text around freely between applications. Discover how easy it is to use tmux to collaborate remotely with others, and explore more advanced usage as you manage multiple tmux sessions, add custom scripts into the tmux status line, and integrate tmux with your system. Whether you're an application developer or a system administrator, you'll find many useful tricks and techniques to help you take control of your terminal.
link: https://play.google.com/store/books/details?id=kA9QDwAAQBAJ
previewLink: http://books.google.co.uk/books?id=kA9QDwAAQBAJ&pg=PT133&dq=tmux&hl=&as_pt=BOOKS&cd=5&source=gbs_api
isbn13: 9781680505160
isbn10: 1680505165
tags:
  - Book
Status: Read
---
[[Books]]
key points:
`<C-b>` is the command prefix, this comes before all tmux commands
## Tmux commands (all prefixed by `<C-b>`)

| Command  | Effect                                                         |
| -------- | -------------------------------------------------------------- |
| `t`      | large clock appears on screen                                  |
| `d`      | detach from a session                                          |
| `c`      | create new window                                              |
| `,`      | rename window                                                  |
| `n`      | next window                                                    |
| `p`      | previous window                                                |
| `0`      | go to window 0                                                 |
| `w`      | visual menu of windows                                         |
| `f`      | search for window containing string of text                    |
| `&`      | close a window                                                 |
| spacebar | toggle through pane layouts                                    |
| `x`      | closes a pane or window if theres only one pane in that window |
| `?`      | list all predefined tmux key bindings                          |
| `[`      | enters copy mode, where you can move around with vim motions   |
| `]`      | pastes                                                         |
| `=`      | list all paste buffers and pastes selected buffer contents     |
| `!`      | turns pane into window                                         |
| `(`      | go to previous sesson                                          |
| `)`      | move to next session                                           |
| `s`      | display a list of sessions                                     |
| `.`      | move window to another session                                 |

- when you detach from a tmux session you're not actually closing tmux, any programs running will stay running (even if you close the terminal window)
## Console commands

| Command                                   | Effect                                                            |
| ----------------------------------------- | ----------------------------------------------------------------- |
| `tmux new[-session] -s basic`             | creates a session labeled basic                                   |
| `tmux new -s basic -n shell`              | creates session basic with first window named shell               |
| `exit`                                    | exits tmux (destroys session) or closes a window or closes a pane |
| `tmux list-sessions` or `tmux ls`         | lists tmux sessions                                               |
| `tmux a[ttach]`                           | attach to last session                                            |
| `tmux attach -t session-name`             | attaches to session called session-name                           |
| `tmux kill-session -t session-name`       | cills the session called session-name                             |
| `tmux split-wondow -h -t development`     | splits the window in the development session                      |
| `tmux split-window -v -t development`     | vertical split of window in development                           |
| `tmux move-window -s process:1 -t editor` | move window to the session editor                                 |


## Command mode
use `<C-b>:` to enter command mode

| Command                          | Effect                                                                                                                                    |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `new-window -n console "{cmd}"`  | create a new window named console (best not to do this with a command)                                                                    |
| `source-file ~/.tmux.conf`       | reload your config                                                                                                                        |
| `capture-pane`                   | copies the pane                                                                                                                           |
| `show-buffer`                    | shows the contents of the buffer                                                                                                          |
| `save-buffer buffer.txt`         | save buffer content to file buffer                                                                                                        |
| `choose-buffer`                  | pick a buffer to paste from                                                                                                               |
| `join-pane -s panes:1`           | take window 1 of the panes session and join it to the current window                                                                      |
| `join-pane -s panes:1.1`         | does the same but with the first pane in the first window                                                                                 |
| `[session_name]:[window].[pane]` | the format used to take a pane from a different source session. You can specify a target window using the `-t` flag and the same notation |
| `pipe-pane -o "cat >> mylog.txt` | pipes tmux activity to the mylog.txt file (if you repeat this command it will deactivate)                                                 |
### Pane layouts

| `even-horizontal` | stacks all panes horizontally, left to right                                                                 |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| `even-vertical`   | stacks all panes vertically, top to bottom                                                                   |
| `main-horizontal` | create one larger pane on the top and smaller panes underneath                                               |
| `main-vertical`   | create one large pane on the left side of the screen and stack the rest of the panes vertically on the right |
| `tiled`           | arrange all panes evenly on the screen                                                                       |

## Scripting Project configuration
```bash
# Check if session already created
tmux has-session -t development
if [ $? != 0 ]
then
   # Create session and open up neovim in the devproject directory
   tmux new-session -s development -n editor -d
   tmux send-keys -t development 'cd ~/devproject' C-m
   tmux send-keys -t development 'nvim .' C-m
   # Create new pane
   tmux split-window -v -t development
   tmux select-layout -t development main-horizontal
   tmux send-keys -t development:1.2 'cd ~/devproject' C-m
   # Create new window
   tmux new-window -n console -t development
   tmux send-keys -t development:2 'cd ~/devproject' C-m
   tmux select-window -t development:1
fi
tmux attach -t development
```
- you can create special configuration files where you can open up tmux in these different ways, for example you could add this script (minus the tmux prefix) into a config called `app.conf`. If you now load up the session with `tmux -f app.conf attach`. Note this will look at your `tmux.conf` file first so you will not lose base settings

### Tmuxinator
- a tool for creating and managing different tmux configs.
- run `tmuxinator open development` to create a new project named development
To get the same effect at the above script run
```yaml
name: development
root: ~/devproject
windows:
  - editor:
      layout: main-horizontal
      panes:
          - nvim
          - 
  - console:
```
- to run this run `tmuxinator development`
- `tmuxinator debug development` will show the script that Tmuxinator will use

## Working with buffers
- enter with `<C-b>[` and exit with `<CR>` 
- copy by pressing space to start and enter to end. Paste with `<C-b>]`
- `capture-pane` can be used to copy the pane, commands such as `capture-pane; save-buffer buffer.txt` saves the pane to a file called buffer
- you can also pick a buffer to paste from

## Pair Programming
- for security it is best you use a VPS or virtual machine to create the environment
### Pairing with a shared account
1. enable SSH access on host
```bash
# create tmux user
tmux@puzzles$ adduser tmux
# switch to user
su tmux
# create folder for keys (only tmux user should be able to rwx this)
mkdir ~/.ssh
touch ~/.ssh/authorized_keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```
2. install and configure tmux
```bash
# user generates their public key
ssh-keygen
# user transfers public key over to the server
cat ~/.ssh/id_rsa.pub | ssh tmux@your_server 'cat >> .ssh/authorized_keys'
# and alternative way to transfer key is via
ssh-copy-id tmux@your_server
# then configure the server with version control, text editors, etc
```
3. create a tmux session
```bash
# create a new tmux session
tmux new-session -s Pairing
```
4. second user logs into machine with same user account and attaches to the session
```bash
# other member of the team can now log onto this session
tmux attach -t Pairing
```

#### Grouped Sessions
- when two people are attached to the same tmux session, they usually both see the same thing and interact with the same window
- with grouped sessions you can work on different windows without completely taking over control
```bash
# create session
tmux new-session -s groupedsession
# another user joins by creating a new session that targets the original session
tmux new-session -t groupedsession -s mysession
```
- second user can `kill-session` and the groupedsession will persist. However if all windows are closed original session will also close

## Pairing with tmate
- a fork of tmux designed for pair programming
- fire up tmate with `tmate`, when launched the connection address will be displayed in the bottom of the window where the status line would be
- you can view this address again with `tmate show-messages`, here you can also give a read-only address as well
- use these addresses to connect
- this can be used with Tmuxinator (see p60)

## Pairing with separate accounts and sockets
- tmux supports sockets 
```bash
# create two new users for the session
sudo adduser sonny
sudo adduser jack
# create tmux grop and the folder to hold the shared sessions
sudo addgroup tmux
sudo mkdir /var/tmux
# change group ownership of /var/tmux so tmux group has access
sudo chgrp tmux /var/tmux
# alter permissions on folder so new files will be accessible for group members
sudo chmod g+ws /var/tmux
# add the users to the group
sudo usermod -aG tmux sonny
sudo usermod -aG tmux jack
```
- create and share sessions we need to create the session using the -S switch (`new-session` uses default socket location so is not reachable by every user)
```bash
# log in to server as sonny and create new tmux session
tmux -S /var/tmux/pairing
# in another terminal window log jack and attach to session via socket file
tmux -S /var/tmux/pairing attach
```
>[!NOTE]
>  the `.tmux.conf` used is that of the person who launched the session
- this means jack is kept out of sonny's home directory