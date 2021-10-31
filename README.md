# License

As per [#1](https://github.com/Qrrbrbirlbel/pgf/issues/1) all files are dual-licensed with

* GNU Public License, version 2.
* LaTeX Project Public License, version 1.3c.

(Please improve the code.)

# TikZ library `node-families`

**Load with:**

    \usetikzlibrary{node-families}

**Files:**

* [`tikzlibrarynode-families.code.tex`][1]

**Inspiration:**
* [Dependent node size in TikZ][2]

Using the keys

   * `Minimum Width=<family>`,
   * `Minimum Height=<family>`,
   * `Text Height=<family>`,
   * `Text Depth=<family>` and
   * `Text Width=<family>`

as an option to a `node` specifies a `<family>` of nodes that shall have *the same dimensions*.
These nodes will have the same width as the widest node and the same height as the tallest node.
The same applies to `text height`, `text depth` and `text width`.

This works on a per-picture basis and uses the `.aux` file so it will need at least two compilations.

More [TeX.sx answers][91] where I used this library can be found with the search function.

**Caveat:** Nodes will only grow. The sizes are never reset unless the document is compiled without the specific node-family applied.

## [Examples][91]
**tikzpicture:**

    \begin{tikzpicture}[% http://tex.stackexchange.com/q/134983/16595
       nodes={circle, draw=black, Minimum Size=test, Text Height=test, Text Depth=test}]
      \node                 (A) {$n$};
      \node[right=0pt of A] (B) {$n+1$};
    \end{tikzpicture}

**Output:**

![Output of two nodes one with "n" and one with "n + 1" having the same size][3]


# TikZ library `paths.ortho`
**Load with:**

    \usetikzlibrary{paths.ortho}
   
**Files:**
* [`tikzlibrarypaths.ortho.code.tex`][4]
* [`tikzlibrarypaths.ortho.tex`][5]

**Inspiration:**
* [Vertical and horizontal lines in pgf-tikz][6]
* [How to draw a return arrow from node-3 to node-1][7]

This library provides two classes of path operatores, names

1. `hvvh` (the `h` stands for “horizontal” and the `v` for “vertical”) with the operators
    * `-|-` and 
    * `|-|` as well as
2. `udlr` (the letters stand for “up”, “down”, “left” and “right”) with the operatores
    * `r-ud` (up, horizontal and down)
    * `r-du` (down, horizontal and up)
    * `r-rl` (right, vertical and left)
    * `r-lr` (left, vertical and right)

**Caveat:** The library defines the keys `|-|`, `|-`, `-|`, `-|-`, `*-` and `-*` which might be used as arrow specification in TikZ.
The current workaround is to use `arrows=|-|`, `arrows=|-` and so on *or* the option `paths.ortho no dash`.

## [Example][92]
**tikzpicture:**

This example uses mostley the `to path`s that are also provided by the library.

    \documentclass[tikz]{standalone}
    \usetikzlibrary{positioning, paths.ortho}
    \tikzset{block/.style={rectangle, draw, minimum size=1cm},
             line/.style={draw, -latex}}
    \begin{document}
    \begin{tikzpicture}[node distance = 1cm]
      \node [block]             (a) {a}; \node [block, below=of a] (b) {b};
      \node [block, right=of a] (c) {c}; \node [block, below=of c] (d) {d};

      \path[line, very thick] (a) edge[ud] (c)
                              (c) edge[rl] (d)
                              (d) edge[du] (b)
                              (b) edge[lr] (a);

      \path[line, green, thick, udlr/distance=0.25cm] (a) edge[du] (c) 
                                                      (c) edge[lr] (d)
                                                      (d) edge[ud] (b)
                                                      (b) edge[rl] (a);

      \draw[red] (a) r-ud (c) r-rl (d) r-du (b) r-lr (a);
    \end{tikzpicture}
    \end{document}

**Output:**

![An example of paths.ortho applications][8]

[1]: tikzlibrarynode-families.code.tex
[2]: http://tex.stackexchange.com/q/107227/16595
[3]: https://i.stack.imgur.com/9fb2y.png
[4]: tikzlibrarypaths.ortho.code.tex
[5]: tikzlibrarypaths.ortho.tex
[6]: https://tex.stackexchange.com/q/45347/16595
[7]: https://tex.stackexchange.com/q/102385/16595
[8]: https://i.stack.imgur.com/kPV0p.png

[91]: https://tex.stackexchange.com/search?q=user%3A16595+node-families
[92]: https://tex.stackexchange.com/search?q=user%3A16595+paths.ortho
