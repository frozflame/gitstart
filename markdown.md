
Markdown Syntax Notes
---------------------


#### Headers ####
> Setext-style headers for `<h1>` and `<h2>` are created by
> “underlining” with equal signs (=) and hyphens (-),
> respectively. You put 1-6 hash marks (#) at the beginning
> of the line — the number of hashes equals the resulting
> HTML header level.


=======================================

#### Links ####

Basic way

    This is [an example](http://example.com/ "Title") inline link.
    [This link](http://example.net/) has no title attribute.

Reference style (note that `[id]` is used, not `(id)`)

    This is [an example][1] reference-style link.
    [1]: http://example.com/  "Optional Title Here"    


