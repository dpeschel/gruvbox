# The basic idea

In diffs mode, use only the four Gruvbox background colors `bg0`–`bg3`
to show changes. This creates more understated colors than the existing
highlighting. It also shows per-language syntax highlighting (C, LISP,
Vimscript, etc.) and changes at the same time. And it handles light and
dark backgrounds.

*Deletions* have the most shading (`bg2` or `bg3`), the *changed parts*
of changed lines have medium shading (`bg1`), and *additions* and the
*unchanged parts* of changed lines have no shading (`bg0`). I tried
giving the *unchanged parts* of changed lines `bg1` and the
*changed parts* `bg0`—so that the new version of the file always had
`bg0`—but in practice this looks less confusing.

# How I got here

The default gruvbox scheme using solid colors and reverse video is easy
to read but very intense. I replaced the reverse video colors with
different background shades and kept the foreground colors, in order to
present the same information in multiple ways.
[Solarized](https://github.com/altercation/solarized)
and [Selenized](https://github.com/jan-warchol/selenized)
do roughly the same thing.

Then I looked more carefully. When comparing two LISP files, `set syntax`
prints `lisp`, not `diff`. And the LISP colors appear on lines that don't
contain diffs! Could I stop Gruvbox from setting the foreground colors,
so I had `lisp` syntax coloring of all lines _and_ `diff` shading of the
background? Yes.

Initially I thought of a range of dark->light shades:
1. the "all dashes" lines darkest,
2. identical text
3. the unchanged parts of changed-text lines
4. the changed parts of changed-text lines
5. added text

But how do you choose the shading of completely-unchanged lines?
And the window bar, tab bar, and fold column? I simplified the range
to the current one.

You need to look at both windows to understand the type of change.
For example, the shading for deletions only appears in one window;
the other window has no shading on the same lines. (Gruvbox inherits
this from the default Vim colors.) Compare the highlighting of `diff`
output.
