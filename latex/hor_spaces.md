# Horizontal spaces

The horizontal spacing macros available for LaTeX are:

* In **math-mode**:

    * `\,` inserts a `\thinmuskip` (i.e. `3mu`)
    * `\!` inserts a negative `\thinmuskip`
    * `\>` or `\:` insert `\medmuskip` (i.e. `4.0mu`)
    * `\;` inserts `\thickmuskip` (i.e. `5.0mu`)

* In **text-mode**:

    * `\,` inserts a `\thinspace` (i.e. `.16667em`)

* In either mode:

    * `\enspace` inserts a space of `.5em`
    * `\quad` inserts a space of `1em`
    * `\qquad` inserts a space of `2em`
    * `\kern <len>` or `\hskip <len>` insert a skip of `<len>` (may be negative)
    * `\hspace{<len>}` inserts a space of length `<len>` (may be negative)
    * `\hphantom{<stuff>}` inserts space of length equivalent to `<stuff>`
    * `\`  inserts a "control space"
    * `~` inserts an "unbreakable" space (similar to an HTML `&nbsp;`)
    * `\hfill` inserts a so-called "rubber length" or stretch between elements

As a reminder,

* `em`: nominal width of an `m`

* `mu`: math unit, `1 em = 18 mu`
