---
title: Practical Vim
subtitle: Edit Text at the Speed of Thought
author: Drew Neil
authors: Drew Neil
category: Computers
categories: Computers
publisher: Pragmatic Bookshelf
publishDate: 2015-10-28
totalPage: 487
coverUrl: http://books.google.com/books/content?id=LA9QDwAAQBAJ&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api
coverSmallUrl: http://books.google.com/books/content?id=LA9QDwAAQBAJ&printsec=frontcover&img=1&zoom=5&edge=curl&source=gbs_api
description: "Vim is a fast and efficient text editor that will make you a faster and more efficient developer. It's available on almost every OS, and if you master the techniques in this book, you'll never need another text editor. In more than 120 Vim tips, you'll quickly learn the editor's core functionality and tackle your trickiest editing and writing tasks. This beloved bestseller has been revised and updated to Vim 7.4 and includes three brand-new tips and five fully revised tips. A highly configurable, cross-platform text editor, Vim is a serious tool for programmers, web developers, and sysadmins who want to raise their game. No other text editor comes close to Vim for speed and efficiency; it runs on almost every system imaginable and supports most coding and markup languages. Learn how to edit text the &quot;Vim way&quot;: complete a series of repetitive changes with The Dot Formula using one keystroke to strike the target, followed by one keystroke to execute the change. Automate complex tasks by recording your keystrokes as a macro. Discover the &quot;very magic&quot; switch that makes Vim's regular expression syntax more like Perl's. Build complex patterns by iterating on your search history. Search inside multiple files, then run Vim's substitute command on the result set for a project-wide search and replace. All without installing a single plugin! Three new tips explain how to run multiple ex commands as a batch, autocomplete sequences of words, and operate on a complete search match. Practical Vim, Second Edition will show you new ways to work with Vim 7.4 more efficiently, whether you're a beginner or an intermediate Vim user. All this, without having to touch the mouse. What You Need: Vim version 7.4"
link: https://play.google.com/store/books/details?id=LA9QDwAAQBAJ
previewLink: http://books.google.co.uk/books?id=LA9QDwAAQBAJ&printsec=frontcover&dq=vim&hl=&as_pt=BOOKS&cd=2&source=gbs_api
isbn13: 9781680504101
isbn10: 168050410X
tags:
  - Book
Status: Reading
---
[[Books]]
## key points:
- . command is very useful. Use one key to move and one key to change (combine ; , * with .)
- Chunk your undos. If you have finished a sentence and are thinking what to write click Esc so you can do back by sentence
	- Up, Down, Left, Right and have the same affect as exiting insert mode (Also affects the . command - same as using i or o)
- Don't count if you can repeat dw. is better than 2dw as it is more repeatable with more control 
- When an operator command is invoked in duplicate, it acts upon the current line (dd)
- operator pending mode is the mode activates upon operator keys being activated. This means you can write custom motions for this mode
- Use operators over visual commands where possible
- using :t means you don't override the register, sometimes useful
- :normal has a lot of power good for . and @p commands use when running over many lines
- increase your command history by doing set history=200, this is useful as you can start the command type click the up arrow and cycle through
- use `<C-z>` to pause the job going back into bash then use fg to restart the job and go back into vim
- navigate using the search word
- use f to move and t for deleting and cutting, try use letters that are uncommon or just search word instead
- for quick word navigation use WORD instead
- use search in visual mode for quick deletions also just do d/word to delete to that word
- as a general rule aw is for deletion and iw if for cutting, same does with l, p, t, b or B
- using the `` command can be useful to jump to the other bracket in replacement (using %)
- move around using jumps list and change list
## commands:
- [[Normal Mode]]
- [[Insert Mode]]
- [[Command Mode]]
- [[Visual Mode]]

[[Files]]
[[Marks]]
[[Jumps]]
[[Registers]]
[[Macros]]
[[Pattern Matching]]
[[Substitution]]
## Cool Websites
- https://vimgolf.com