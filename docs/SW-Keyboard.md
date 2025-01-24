{:menu SW}


# Configuring the Macintosh Keyboard

* toc
{:toc}

With apologies to Windows and Linux users, I am primarily familiar with hacking a Mac to make its keyboard more useful.

## Overview

MacOS comes with a variety of keyboard shortcuts installed for you
automatically, but you may not realize that they are there—or how convenient
they can be! For those of us raised on EMACS, they are so thoroughly embedded in
our fingers that it is difficult to adjust to computers and operating systems
that lack them. What's more, you can create key sequences that allow you to
quickly type Greek or other letters without having to switch keyboard layouts.

## Modifier keys

It strains my finger to use the control key where it is on current Mac
keyboards, and I basically never have any use for **caps lock**. So, I make the **caps
lock** key another **control** key using **System Preferences > Keyboard > Keyboard >
Modifier Keys**. As you'll see below, the control key is extremely convenient
for navigation on a Mac (which is why I find it difficult to adjust to
applications in X and Windows, which use the control key to fire menu commands,
for which the Mac uses the **command** key).

## Built-in navigation keys

Before computer keyboards were outfitted with wonderful innovations like arrow
keys, we still had to move around the screen. Even on keyboards with arrow keys,
it can be awkward to strike those keys without looking for them because they
usually live in inconvenient places compared to the home row. Two main solutions
emerged: the vi(m) solution and the emacs solution.

## VI and VIM

VI (VIsual editor) used a key to toggle between editing mode, in which letters
produced text, and command/navigation mode, in which letters launched a variety
of editing operations, such as moving the cursor up, down, left, or right. (In
VI, j and k go left and right, while h and l go up and down. Not very mnemonic,
but definitely clustered.)

## EMACS

EMACS (Editor MACroS) was created by Richard Stallman in 1976 and based on a
different trick to allow letters to play multiple roles. Instead, one uses
modifier keys to modify the meaning of a letter, which is essentially an
extension of the shift key (which modifies lowercase letters to give uppercase
versions, and changes numbers into various symbols). The primary modifier key is
the control key, which (importantly) was often located where the caps lock key is
found these days. Which means to say, it was in a very convenient location to be
pressed with the left pinky to modify the meaning of the letter key to be
pressed. Stallman sought to use letters with sensible hints to their meaning (at
least for English speakers). Hence, the following list of control keys (which
is just a subset of the available.

| keystroke | meaning                                                      |
|-----------+--------------------------------------------------------------|
| ^f        | forward one character (i.e., right arrow)                    |
| ^b        | back one character (left arrow)                              |
| ^n        | next line (down arrow)                                       |
| ^p        | previous line (up arrow)                                     |
|-----------+--------------------------------------------------------------|
| ^a        | beginning of the line (like beginning of the alphabet)       |
| ^e        | end of the line                                              |
|-----------+--------------------------------------------------------------|
| ^t        | transpose (swap the characters on either side of the cursor) |
| ^k        | kill (delete from the cursor) to the end of the line         |
|-----------+--------------------------------------------------------------|

## Accessing Greek unicode characters

You can create key sequences to type Greek letters. I use the prefix `^g`
followed by the corresponding letter: a for $$\alpha$$, b for $$\beta$$, etc. The mapping
is defined in a file called `DefaultKeyBinding.dict` which gets stored in the
directory `~/Library/KeyBindings/`.  Create a text file with the name
`DefaultKeyBinding.dict` and enter the following text, then save the file in the
`KeyBindings` directory. Applications that are open at the time you save this
file will not notice the changes, but any application you open once the file is
saved should adopt the added bindings.

~~~~ shell
/* Greek unicode letters */
"^g" = {
    "a" = ("insertText:", "\U03B1");
    "b" = ("insertText:", "\U03B2");
    "g" = ("insertText:", "\U03B3");
    "d" = ("insertText:", "\U03B4");
    "e" = ("insertText:", "\U03B5");
    "z" = ("insertText:", "\U03B6");
    "h" = ("insertText:", "\U03B7");
    "q" = ("insertText:", "\U03B8");
    "k" = ("insertText:", "\U03BA");
    "l" = ("insertText:", "\U03BB");
    "m" = ("insertText:", "\U03BC");
    "n" = ("insertText:", "\U03BD");
    "x" = ("insertText:", "\U03BE");
    "p" = ("insertText:", "\U03C0");
    "r" = ("insertText:", "\U03C1");
    "s" = ("insertText:", "\U03C3");
    "t" = ("insertText:", "\U03C4");
    "u" = ("insertText:", "\U03C5");
    "c" = ("insertText:", "\U03C7");
    "y" = ("insertText:", "\U03C8");
    "w" = ("insertText:", "\U03C9");
    "f" = ("insertText:", "\U03D5");
    "F" = ("insertText:", "\U03C6");
    "G" = ("insertText:", "\U0393");
    "D" = ("insertText:", "\U0394");
    "P" = ("insertText:", "\U03A0");
    "Q" = ("insertText:", "\U0398");
    "S" = ("insertText:", "\U03A3");
    "W" = ("insertText:", "\U03A9");
    "X" = ("insertText:", "\U039E");
};
~~~~


## Additional sources of information

- [Old Apple documentation](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/EventOverview/TextDefaultsBindings/TextDefaultsBindings.html)
- [https://ss64.com/osx/syntax-keybindings.html](https://ss64.com/osx/syntax-keybindings.html)
- [Cocoa Text System](https://www.hcs.harvard.edu/~jrus/Site/Cocoa%20Text%20System.html)
