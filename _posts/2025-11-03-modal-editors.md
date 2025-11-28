---
layout: post
title: Modal editors
---
(I use the term vi-like as a catch-all for editors and ways of using editors or other text-based programs which use key combinations like vi).

I first used a modal editor back in around 1987 when I had to use the HM Treasury tax and benefit (IGOTM) model. Part of this was written in C and the only way of editing the code at the time was to connect to the Treasury server and use vi. What was already a complex problem (understanding the model and C) became even more confusing with such an esoteric editor and strange invocations like the substitute command and regex.

With the growth of graphical interfaces and mice, you might have thought text editors that rely on keyboard shortcuts or combinations were well past their sell-by dates. But modal editors offer great advantages if you put in some time to learn them, and I really enjoy using them. There's nothing new in what I write below, just my random thoughts.

## What is a modal editor?
A modal editor has different modes to interact with a document. This contrasts with editors or IDEs like Notepad, Visual Studio Code or word processors like Word, where there is a single mode in which you edit text and move around. In the years since I was using it, several other modal editors have been spun off from vi, what I will call vi-like editors.

At the heart of vi-like editors is the desire to eliminate the use of the mouse and to keep the hands on the keyboard, and particularly the core keys for the right hand ( `hjkl`) as much as possible. At the hands (literally) of a practiced user, this can greatly speed up editing.

There is also something about interacting with text using the different key combinations which is absent when using a mouse. It seems somehow that you are closer to and more involved with the text.

There is also the (slightly smug) self-satisfaction of having mastered something seemingly so complex.

In addition, using the key combinations makes it much easier to switch devices, since the letter keys are always in the same place (albeit with slightly different sizes), which can't be said for keys like `Page up`, `Page down` or cursor keys, for which keyboard manufacturers seem to delight in finding new positions.

In what follows, I merely touch on the capabilities of modal editors, there are vastly more commands/operations than I mention - use the resources at the end to find out more.

## Modes
Vi-like editors have Normal, Insert, Visual and Command modes (there are others but let's keep it simple).

Normal mode is the default mode and enables you to quickly move around the file using key combinations. Since in Normal mode you are not entering text, these combinations do not need to use `Ctrl` or similar keys, and you usually enter these combinations one after the other.

Some functions just use a single key. At the simplest level, you can use `j` to move the cursor a line down, and `k` to move a line up. `h` to move a character backwards, and `l` to move a character forwards. These key choices make more sense when you look at the keys on the keyboard. And these can be combined with a number so `5j` will move 5 lines down. `52g` will move you to line 52.

But these movements only get you so far (puns will be reduced from now on). More powerful shortcuts include move forward by whole words `w`, `b` for words backward, or paragraphs `}` and `{`. Then there are combinations to get to the top of the file `gg` or the end `G`, the beginning of the line `^` or the end of the line `$`. Or `t` plus a character to get you to just before the character, e.g., `t=` to get to just before the next equal sign.

Letters can be combined, with the resultant "phrases" becoming second-nature over time, like `daw` for delete around word. Vi-like editors use an action-scope form, that is, things like delete come before the scope over which it operates. Helix turns this around, as we'll see below.

Since change (replace text by jumping into Insert mode)  is `c`, copying is `y` for "yank". Paste is still paste, with `p` for paste after the current position and `P` for before the current position.

Insert mode is much more like a "normal" editor in which you type the text you want entered. From Normal mode, you get into Insert mode with `i` if you want to insert at the current cursor position (there are alternatives like `A` to insert/append at the end of the current line).

From Insert mode, you return to Normal mode with `Esc`. The idea of modal editors is that you don't spend much time in Insert mode - you make most your movements and many of the changes in the other modes particularly Normal, moving into Insert mode merely for entry. There are shortcuts in Insert mode but I have trouble remembering them, and of course these have to use modifiers like `Ctrl` since otherwise the characters would be entered as text.

Visual mode is like highlighting text on which you can then carry out operations.

Command mode is extremely powerful and has many different commands - in fact, command mode is really the residual of an even older editor called ed (which metamorphosed through em, en and then ex), where there was no visual interface for the file and you had to instruct the editor describing which lines you wanted to change etc. Vi then denoted a "Visual" way of interacting. You enter Command mode by pressing `:` in Normal mode.

Command mode is also the usual way of exiting out of a file, either saving it or not. So, from Normal mode, `:wq` will enter Command mode, write the current file and then quit the editor. `:q` will just quit but will prevent you from doing so if the file has unsaved edits. `:q!` will exit without prompting you to save - so use with caution.

You can easily record a macro (many different combinations) using `q` plus a letter in Normal mode, with `q` again to stop recording. You then run the macro with `@` plus the letter you used.

## Which editors
The main modal editors many people will come across these days are Vim and Neovim, which are developments of the old vi. They are usually available on Linux systems or can easily be installed on most other operating systems.

Helix, my current favourite, is very vi-like but, as well as being completely rewritten for speed and having many things built-in which you have to add to Vim or Neovim, changes some of the ways Normal mode works so it combines aspects of Visual mode and some of the Normal shortcuts are slightly different, for example, `ge` (instead of `G`) goes to the end of the file. Instead of `^` and `$` to move to start and end of the line, you have the more consistent  `gh` and `gl` (think of those core keys `hjkl`).

Normal mode always has something selected, even if it's just the current character, so pressing `d` on an empty line will delete it.

Rather than `w` merely jumping words, it also selects them. This enables what I think is a more intuitive way of deleting words, as `wd` will select and delete the next word. Helix differs from the other vi-like editors in using this scope-action form.

`x` becomes a line selection rather than the single character deletion in vi, so `3xd` will select the next three lines and delete them. It also seems quite natural to keep pressing `x` to add lines to the selection, analogous to holding the control key down in more conventional editors.

Another of my favourite editors, Zed, has both Vim and Helix modes built-in. Whilst the latter is not quite a complete implementation, it still has the nearly all of the functions. Visual Studio Code also has Vim and Helix extensions.

## Vi-type movements in other applications
Obsidian has a built-in Vim mode which has the most useful commands. There is an extension that offers Helix commands, though I find it a bit basic and it sometimes has visual issues. I find myself often just opening a note in Zed or Helix for speed of editing.

Surprisingly, one of the best use of vi-type shortcuts is in a browser, to greatly speed up navigation. An extension like Vimium is necessary and when enabled is like using an editor in Normal mode. Using `j` and `k` to scroll slowly or `Ctrl-d` and `Ctrl-u` for faster scrolls is much quicker than hitting the scroll bar or taking your hands away from the home row to find page up or down, or to use the mouse. By adding your own shortcuts you can add in extra features like quickly closing or reopening tabs with Helix-like `d` and `u`.

## Learning
Both Vim and Helix have tutorials (`:tutor` inside Helix) and there is a wealth of other learning material on vi-type editors, start with https://learnbyexample.github.io/curated_resources/vim.html. There is much less on Helix - probably the best place to start is https://github.com/npupko/awesome-helix.
