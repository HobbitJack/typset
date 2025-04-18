# typset
A very simple Unix pipeline-based typesetting package.

As of version v2.0.0, ``typset`` consists of five tools.
All included tools are designed around working with plain text, and a very small and trivial to learn typesetting language applies to help get certain types of special formatting out.
Note that these tools are designed around the way *I* write plain-text documents, as stories and such for my Creative Writing class, and occassionaly as write-ups for other classes. As such, this formatting style may not be what you need.
The special types of text are as follows.

First are SECTION TITLES. SECTION TITLES are in all caps and come on their own lines. These will stay on their own lines, and will be centered once typesetting is applied.

Next are //notes. //notes are lines that start with //C-style comments. Notes are treated as document text, but will not have special formatting like line joining or indenting applied. I use these to make reader's notes stand apart from body text.

After that are !shellouts. !shellouts are lines that start with !bangs. !shellouts will send the rest of the line verbatim to your shell, and pipe STDOUT from that command directly into the source of your typ document -- the output can then be typeset by ``typ`` and ``pag``.
The result doesn't typically look that bad, as long as your output isn't too long to fit on a single line.

Lastly are #comments. #comments are lines that belong in the source document but which are not wanted in the final document -- perhaps some notes about characters, or maybe your thoughts while writing the section. These will be removed by ``typ`` and so will not make it into a final document typeset with the ``typset`` pipeline.

## ``ljn`` -- line join
``ljn``, or line join, joins lines of text where each line is assumed to be a sentence on its own.
The behavior of this program can be modified with program flags.
For example, to treat quotations as a part of the document (for example, in typesetting an argumentative essay), you can pass -q to disable this behavior and treat them as simply sentences of their own.
The newline is kept for consistency as depending on what you do with this text, you may want to keep newlines as they are. For example, however, ``typ``, the next program in the package, strips these and adds its own.

## ``chr`` -- inser special characters
``chr``, or characters, allows you to insert some non-ASCII characters, like Greek letters or some math symbols, into your document.
Simply use ``chr -H | less`` to find the character you want and the escape sequence for it.
Nonsense escape sequences are ignored, and there is no fuzzy-matching.

## ``bib`` -- insert inline citations
``bib``, or bibliography, is a simple way to insert inline citations without disrupting the flow of your source document.
Somewhere in your document, simply include a SECTION TITLE starting with REFERENCES, BIBLIOGRAPHY, or WORKS CITED, and each line in that section will then have a short citation (e.g. Florb 2025), followed by a pipe ``|`` and the full citation (Florb, B. 2025, FlorbJournal, 45, 23).
Then, simply index into your list with [[N]] and the Nth short citation will be inserted in-line.

## ``typ`` -- typeset text
``typ``, or typeset, typesets lines of text where each line is a paragraph with multiple sentences.
For shorter text, the line length target is roughly 83% of the total line length. For longer lines, where it's less jagged to go to a newline, a target width of 93% is used instead.
This isn't perfect but it doesn't do terribly -- it will tend to do worse with very longer words.

## ``pag`` -- paginate text
``pag``, or paginate, paginates text and adds headers to pages. Headers are not used if the page is too short -- less than 10 lines. 
This can be used with other typsetting tools, so long as the text of the document is properly wrapped.

# Documentation
Right now, no. Soon, the help messages for each program will be filled out beyond usage, and man pages (don't get your hopes up, probably using ``help2man`` if we're being honest) will be written.

# Bugs
Please file a GitHub issue if you find any bugs or crashes. Alternatively, I'll fix them as I find them.

# License
The ``typset`` package is licenesed under the GNU GPLv3.0. See LICENSE for a full list of terms.
Copyright (C) HobbitJack 2025

# Recommended Software
With the addition of the !shellout feature in v2.0.0, some extra software is useful for making better technical documents.
I will include references to that software here as I find it:
- `utftex`: Insert typeset ASCII equations into the text stream
- `boxes`: Draw boxes around e.g. tables
