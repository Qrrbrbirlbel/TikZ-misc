# TikZ library `node-families`

Load with

    \usetikzlibrary{node-families}

**Files:**

* [`tikzlibrarynode-families.code.tex`][1]

This library has been created in response to “[Dependent node size][2]” where Op asks for automatic re-sizing of related nodes so that they have the same minimum size.

Using the keys

   * `Minimum Width=<family>`,
   * `Minimum Height=<family>`,
   * `Text Height=<family>`,
   * `Text Depth=<family>` and
   * `Text Width=<family>`

as an option to a `node` specifies a `<family>` of nodes that shall have the same dimensions.
This works on a per-picture basis and uses the `.aux` file so it will need at least two compilations.

**Caveat:** Nodes will only grow. The sizes are never reset unless the document is compiled without the same key-value pair.

## Example
**tikzpicture:**

    \begin{tikzpicture}[% http://tex.stackexchange.com/q/134983/16595
       nodes={circle, draw=black, Minimum Size=test, Text Height=test, Text Depth=test}]
      \node                 (A) {$n$};
      \node[right=0pt of A] (B) {$n+1$};
    \end{tikzpicture}

**Output:**

![Output of two nodes one with "n" and one with "n + 1" having the same size][3]


# `paths.ortho`
Load with

    \usetikzlibrary{paths.ortho}
   
**Files:**
* [`tikzlibrarypaths.ortho.code.tex`][4]
* [`tikzlibrarypaths.ortho.tex`][5]

This library provides two classes of path operatores, names

1. `hvvh` (the `h` stands for “horizontal” and the `v` for “vertical”) with the operators
  * `-|-` and 
  * `|-|` as well as
2. `udlr` (the letters stand for “up”, “down”, “left” and “right”) with the operatores
  * `r-ud` (up, horizontal and down)
  * `r-du` (down, horizontal and up)
  * `r-rl` (right, vertical and left)
  * `r-lr` (left, vertical and right)


[1]: tikzlibrarynode-families.code.tex
[2]: http://tex.stackexchange.com/q/107227/16595
[3]: https://i.stack.imgur.com/9fb2y.png
[4]: https://github.com/Qrrbrbirlbel/pgf/blob/master/tikzlibrarypaths.ortho.code.tex
[5]: https://github.com/Qrrbrbirlbel/pgf/blob/master/tikzlibrarypaths.ortho.tex

[9]: http://tex.stackexchange.com/a/110172/16595
[10]: http://tex.stackexchange.com/a/102409/16595
[11]: http://tex.stackexchange.com/a/106571/16595
[12]: http://tex.stackexchange.com/a/107144/16595
[13]: http://tex.stackexchange.com/search?q=user%3A16595+positioning-plus
