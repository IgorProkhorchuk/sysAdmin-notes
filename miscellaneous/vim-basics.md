Basic Commands
r : Replace the character under the cursor with a specified character.

v : Visual Mode for selecting text.

y : Yank (copy) selected text into the buffer.

p : Paste text after the cursor.

P : Paste text before the cursor.

:%s/old/new/g : Substitute all instances of old with new in the entire file.

Copy & Paste
v + y : Yank (copy) the selected character or text.

yy : Yank the entire current line.

"+y : Yank into the system clipboard.

"+p : Paste from the system clipboard.

dd : Delete the entire current line (also copies it).

Visual Mode
v : Enter Visual Mode for character-wise selection.

V : Enter Visual Line Mode for line-wise selection.

Ctrl+V : Enter Visual Block Mode for block selection.

Replace & Substitute
r<character> : Replace the character under the cursor with <character>.

:%s/a/b/g : Replace all instances of a with b in the entire file.

:%s/a/<Ctrl+R>"\/g : Replace all instances of a with the yanked character in the entire file.

:s/a/b/ : Replace the first instance of a with b in the current line.

Deleting
x : Delete the character under the cursor.

dw : Delete from the cursor to the end of the word.

d$ : Delete from the cursor to the end of the line.

D : Delete the rest of the line (same as d$).

Undo & Redo
u : Undo the last change.

Ctrl+r : Redo the undone change.

Navigating
h : Move left.

j : Move down.

k : Move up.

l : Move right.

0 : Move to the beginning of the line.

$ : Move to the end of the line.

gg : Move to the beginning of the file.

G : Move to the end of the file.

Miscellaneous
: : Enter command-line mode.

/ : Search for a string in the file.

n : Move to the next search result.

N : Move to the previous search result.

:w : Write (save) the file.

:q : Quit Vim.

:wq : Write and Quit.

:q! : Quit without saving.