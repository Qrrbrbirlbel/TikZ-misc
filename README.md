# License

As per [#1](https://github.com/Qrrbrbirlbel/pgf/issues/1) all files are dual-licensed with

* GNU Public License, version 2.
* LaTeX Project Public License, version 1.3c.

(Please improve the code.)

# TikZ library `node-families`

**Load with:**

    \usetikzlibrary{node-families}

**File:**

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

```latex
\begin{tikzpicture}[% http://tex.stackexchange.com/q/134983/16595
   nodes={circle, draw=black, Minimum Size=test, Text Height=test, Text Depth=test}]
  \node                 (A) {$n$};
  \node[right=0pt of A] (B) {$n+1$};
\end{tikzpicture}
```
**Output:**

![Output of two nodes one with "n" and one with "n + 1" having the same size][3]


# TikZ library `qrr.paths.ortho`
**Load with:**

    \usetikzlibrary{qrr.paths.ortho}
   
**Files:**
* [`tikzlibraryqrr.paths.ortho.code.tex`][4]
* [`tikzlibraryqrr.paths.ortho.tex`][5]

**Inspiration:**
* [Vertical and horizontal lines in pgf-tikz][6]
* [How to draw a return arrow from node-3 to node-1][7]
* [Vertikale Verbindung zwischen zwei ungleich großen Elementen][15]

This library provides two classes of path operatores. These are

1. `-|-` and  `|-|` as well as
2. `r-ud` (up, horizontal and down), `r-du` (down, horizontal and up), `r-rl` (right, vertical and left) and `r-lr` (left, vertical and right).

The first two (`-|-` and `|-|`) are also provides for use in `to` or `edge` operators as `horizontal vertical horizontal` and `vertical horizontal vertical`.

There are a set of `only horizontal|vertical first|second` ones that are used in the last inspiration and they can be used to connect nodes orthogonally when they're not ligned up directly.

## Example
```latex
\begin{tikzpicture}[small node/.style={font=\small,inner sep=+1pt,above,sloped}]
    \draw[help lines] (-.5,-1.25) grid (5.25,5.5);
    \node[circle, draw] (a) {A};\node[circle, draw] at (3,5) (b) {B};
    \draw                      (a) |-|                           (b) node[small node, pos=.125] {.125};
    \draw[hvvh/spacing=0, red] (a) -|-[ratio=.3333, from center] (b) node[small node, pos=1.5]  {top};
    \draw[rotate=45, blue]     (a) r-du[distance=1cm, from center] (b)
                                   node[small node, pos=.5, transform shape] {middle};
\end{tikzpicture}
```
# TikZ library `qrr.paths.timer`

**Load with:**

    \usetikzlibrary{qrr.paths.timer}
   
**File:**
* [`tikzlibraryqrr.paths.timer.code.tex`][9]

**Inspiration:**
* [Is It Possible to Combine TikZ Distance and Line-To Operations?][10]
* [How to place a coordinate at parabola-path-position?][11]

This library extends the node placing algorithm (a.k.a. timer) for the path operators

* `rectangle` where the corners are at `0` (south west), `0.25` (north west), `0.5` (north east), `0.75` (south east) and
* `parabola` where the bend is at `0.5`.

## Example
```latex
\begin{tikzpicture}
    \draw[help lines]  (-2.25,-1.25) grid (2.25,3.25);
    \draw              ( 2,-1) parabola bend (0,0) (-1,3);
    \draw[ultra thick] (-2,-1) parabola bend (0,0) ( 1,3) foreach \pos in {1,...,4,6,7,...,9}
                               {node[pos=\pos/10,sloped,fill=white,font=\tiny,inner sep=+0pt]{\pos}};
\end{tikzpicture}
\begin{tikzpicture}
	\draw[help lines, overlay] (-3,-3) grid (1.25, 1);
	\draw                      (-2,-2) parabola (1,0)
	     foreach \pos in {0,1,...,10} {node[pos=\pos/10, alias=@, inner sep=+1pt,
		    append after command={(@) edge node[pos=1,font=\tiny,inner sep=+0pt,anchor=-18*\pos+90]
		       {\pos} ++(-18*\pos+270:.5cm) }] {.}};
\end{tikzpicture}
```

# TikZ library `patterns.images`
**Load with:**

   \usetikzlibrary{patterns.images}

**File:**
 * [`tikzlibrarypatterns.images.code.tex`][12]

**Inspiration:**
 * [Define pattern with reference to external picture][13]

## [Example][14]

[1]: tikzlibrarynode-families.code.tex
[2]: http://tex.stackexchange.com/q/107227/16595
[3]: https://i.stack.imgur.com/9fb2y.png
[4]: tikzlibraryqrr.paths.ortho.code.tex
[5]: tikzlibraryqrr.paths.ortho.tex
[6]: https://tex.stackexchange.com/q/45347/16595
[7]: https://tex.stackexchange.com/q/102385/16595
[8]: https://i.stack.imgur.com/kPV0p.png
[9]: tikzlibraryqrr.paths.timer.code.tex
[10]: https://tex.stackexchange.com/q/106558/16595
[11]: https://tex.stackexchange.com/a/543268/16595
[12]: tikzlibrarypatterns.images.code.tex
[13]: https://tex.stackexchange.com/q/103980/16595
[14]: https://tex.stackexchange.com/a/107144/16595
[15]: https://texwelt.de/fragen/1289
[91]: https://tex.stackexchange.com/search?q=user%3A16595+node-families
[92]: https://tex.stackexchange.com/search?q=user%3A16595+paths.ortho
[^lineto]: TikZ uses the same timer `\tikz@timer@line` that's used for `--` also for `rectangle`. Without patching `\tikz@rect@B` this can't be changed.
