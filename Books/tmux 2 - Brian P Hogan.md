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
Status: Reading
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

- when you detach from a tmux session you're not actually closing tmux, any programs running will stay running (even if you close the terminal window)
## Console commands

| Command                             | Effect                                                            |
| ----------------------------------- | ----------------------------------------------------------------- |
| `tmux new[-session] -s basic`       | creates a session labeled basic                                   |
| `tmux new -s basic -n shell`        | creates session basic with first window named shell               |
| `exit`                              | exits tmux (destroys session) or closes a window or closes a pane |
| `tmux list-sessions` or `tmux ls`   | lists tmux sessions                                               |
| `tmux a[ttach]`                     | attach to last session                                            |
| `tmux attach -t session-name`       | attaches to session called session-name                           |
| `tmux kill-session -t session-name` | cills the session called session-name                             |

## Command mode
use `<C-b>:` to enter command mode

| Command                         | Effect                                                                 |
| ------------------------------- | ---------------------------------------------------------------------- |
| `new-window -n console "{cmd}"` | create a new window named console (best not to do this with a command) |
| `source-file ~/.tmux.conf`      | reload your config                                                     |
### Pane layouts

| `even-horizontal` | stacks all panes horizontally, left to right                                                                 |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| `even-vertical`   | stacks all panes vertically, top to bottom                                                                   |
| `main-horizontal` | create one larger pane on the top and smaller panes underneath                                               |
| `main-vertical`   | create one large pane on the left side of the screen and stack the rest of the panes vertically on the right |
| `tiled`           | arrange all panes evenly on the screen                                                                       |