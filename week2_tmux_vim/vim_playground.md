This is a Vim playground where we will practice our vim-craft.

You will use superpowers
to remove this lame set
of lines that are taking
up space for no reason.

# The FIRST thing we need to do is play around in "NORMAL"  mode. 
Press [Esc] a couple times.

LETS NAVIGATE using **motions**

We can perform basic navigation with [h],[j],[k],[l].
We can also move a bit quicker between words with [w], [e], and [b]
We can move to the beginig of a line with [^] or the end of a line with [$].
(We (can move to the bracket partner) with [%])
We can move to the end of a file with [G].
We can go to any line (like line 6 for example) with [:6]
We can jump with [f&] to jump to any character (like &), jump back with[F&]


LETS PERFORM 1-KEY ALTERATIONS

Re Ean Peplace Lharacters Aith Che [r] Eey!
We R can E remove M single O characters V with E [x] key!
We can paste with [p] from the "default register"
-------(    .    )-------paste on the "." 
We can paste with the [P] from the "default register"
-------(    .    )-------paste on the "." 


LETS SAVE NOW

We have made changes so we can save or "write" wit [:w]


LETS PERFORM 2-KEY ALTERATIONS

I really like this line let's "yank" it with [yy].
-------(    .    )-------paste on the "." 
This line needs to go let's delete it with [dd].
-------(    .    )-------paste on the "." 


THE POWER OF VIM COMES FROM ITS KEY COMBINATIONS

Vim can combine **operators** (like [d]) with motions (like [w])REMOVE.
We can combine operators or motions with counts [d3d] removes 3 lines.
    You will remove this.
    You will remove this.
    You will remove this.
Get vimified with [d3w] to REMOVE REMOVE REMOVE remove thos pesky words.
Using a **range** we can remove the lines from the header [:3,6d]


# The SECOND thing we need to do is add text in "-- INSERT --" mode. 
Press [Esc] a couple times.

LETS ADD TEXT (remember [Esc] takes you out of INSERT)

Adding text at your cursor is easy with [i]
-------(    .    )-------place your cursor on "." and type [i]
Adding text after your cursor is easy too, with [a] 
-------(    .    )-------place your cursor on "." and type [a]
How about adding text to the begining of the line with [I]
-------(    .    )-------place your cursor on "." and type [I]
I bet you can guess how to add to the end of the line
-------CNJCx is very

# The THIRD thing we need to do is select text in the "-- VISUAL --" modes. 
Press [Esc] a couple times.

WORKING IN " -- VISUAL--" MODE, [v]

Press [v] go go into visual mode, you can select characters now!


WORKING IN "-- VISUAL LINE--" MODE, [V]

Removing a chunk of code is easy in this mode, hit [d]?
    for curr_word in ["I'm", "a", "bad", "chunk"]:
        print(curr_word)
    end

COMMENTING IN "-- VISUAL BLOCK--" MODE, [Ctrl-v]

add any character you like
to the start of each of these
lines with [I] after you
have selected them with [Ctrl-v]
It will look like it's just
working on the first line before
you hit [Esc].

# The LAST thing we need to do is learn how to search

TO FORWARD SEARCH [/<characters>]
TO REVERSE SEARCH [?<characters>]

TO SEARCH the REPLACE [:s/<search>/<replace>/]

Roses are SOMETHING.
Violets are a SOMETHING.

After you search [:noh] gets rid of your highlights.

# Bonus check my spelling

[:set spell] turn it on
[:set nospell]  turn it off
[ ]s ]  go to next word
[ [s ]  go to previous word


We can move the beginning of a file with [gg]
