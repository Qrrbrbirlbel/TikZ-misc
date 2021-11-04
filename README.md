# License

As per [#1](https://github.com/Qrrbrbirlbel/pgf/issues/1) all files are dual-licensed with

* GNU Public License, version 2.
* LaTeX Project Public License, version 1.3c.

(Please improve the code.)

# Libraries for PGF or TikZ
## TikZ library `node-families`

**Load with:**

    \usetikzlibrary{node-families}

**File:** [`tikzlibrarynode-families.code.tex`][nf-code]

**Inspiration:** [Dependent node size in TikZ][nf-insp]

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

**Caveat:** Nodes will only grow. The sizes are never reset unless the document is compiled without the specific node-family applied.

[**Example**][nf-ex-out] (→ [more Examples at TeX.sx][nf-more-examples]):
```latex
\begin{tikzpicture}[% http://tex.stackexchange.com/q/134983/16595
   nodes={circle, draw=black, Minimum Size=test, Text Height=test, Text Depth=test}]
  \node                 (A) {$n$};
  \node[right=0pt of A] (B) {$n+1$};
\end{tikzpicture}
```

## TikZ library `qrr.paths.ortho`
**Load with:**

    \usetikzlibrary{qrr.paths.ortho}
   
**Files:**
1. [`tikzlibraryqrr.paths.ortho.code.tex`][po-code1]
2. [`tikzlibraryqrr.paths.ortho.tex`][po-code2]

**Inspiration:**
1. [Vertical and horizontal lines in pgf-tikz][po-insp1]
2. [How to draw a return arrow from node-3 to node-1][po-insp2]
3. [Vertikale Verbindung zwischen zwei ungleich großen Elementen][po-insp3]

This library provides two classes of path operatores. These are

1. `-|-` and  `|-|` as well as
2. `r-ud` (up, horizontal and down), `r-du` (down, horizontal and up), `r-rl` (right, vertical and left) and `r-lr` (left, vertical and right).

The first two (`-|-` and `|-|`) are also provides for use in `to` or `edge` operators as `horizontal vertical horizontal` and `vertical horizontal vertical`.

There are a set of `only horizontal|vertical first|second` ones that are used in the third inspiration and they can be used to connect nodes orthogonally when they're not ligned up directly.

**Example** (→ [more examples at TeX.sx][po-ex]):
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
## TikZ library `qrr.paths.timer`

**Load with:**

    \usetikzlibrary{qrr.paths.timer}
   
**File:** [`tikzlibraryqrr.paths.timer.code.tex`][timer-code]

**Inspiration:**
1. [Is It Possible to Combine TikZ Distance and Line-To Operations?][timer-insp1]
2. [How to place a coordinate at parabola-path-position?][timer-insp2]

This library extends the node placing algorithm (a.k.a. timer) for the path operators

* `rectangle` where the corners are at `0` (south west), `0.25` (north west), `0.5` (north east), `0.75` (south east) and
* `parabola` where the bend is at `0.5`.

**Example:**
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

## TikZ library `patterns.images`
**Load with:**

    \usetikzlibrary{patterns.images}

**File:** [`tikzlibrarypatterns.images.code.tex`][pi-code]

**Inspiration:** [Define pattern with reference to external picture][pi-insp]

**Example:** For an example, take a look at the [inspiration][pi-insp].

## (PGF/)TikZ library `qrr.trans`
**Load with:**

    \usetikzlibrary{qrr.trans}
    
**Files:**
1. [`pgflibraryqrr.trans.code.tex`](pgfibraryqrr.trans.code.tex)
2. [`tikzlibraryqrr.trans.code.tex`](tikzlibraryqrr.trans.code.tex)

**Inspiration:**
1. [Is there a way in TikZ to reflect regular polygons of an arbitrary number of edges?](https://tex.stackexchange.com/a/149509/16595)
2. [What is the simplest way to draw this triangle exactly?](https://tex.stackexchange.com/a/142585/16595)

This TikZ library provides the key `mirror=(<p1>)--(<p2>)` that applies a transformation that mirrors at the line through `<p1>` and `<p2>`.
See the inspirations for examples.

## TikZ library `qrr.norm`
**Load with:**

    \usetikzlibrary{qrr.norm}
    
**File:** [`tikzlibraryqrr.norm.code.tex`](tikzlibraryqrr.norm.code.tex)

**Inspiration:** [How to normalize a vector in pgf/tikz?](https://tex.stackexchange.com/a/109926/16595)

This library provides a `norm cs` and two keys `norm` and `Norm`.

### Keys
 - `norm` is a `to path` that uses the `norm cs` to create an normalized vector.
 - `Norm` can be used to change the length of the normalized vector.

  The default is `1` in the current coordinate system. This has the advantage that any change in the coordinate system (the `x` and `y` keys can be used to change the coordinate system) the normalized vector is still of the length of `1` (and not `1cm` in the paper plane which is used with in other answers).

 The key, though, can also be used to set a fixed length (in the paper plane) which is used then.

### `norm cs`
The `norm cs` accepts as parameter any TikZ `<coordinate>` and an optional `from <another coordinate>` (the `<another coordinate>` is by default `(0,0)`, the origin). This will result in the normalized (according to `Norm` setting) vector.

Note that this does not draw any lines in any relation to the current point on the path.

    \draw (1,2) -- (norm cs: 3,0);
will result in a line from `(1,2)` to `(1,0)` and not `(2,2)` nor the point that is `1cm` from `(1,2)` to `(3,0)`. The `norm cs` will most likely be used with relative coordinates. The following will draw a line from `(1,2)` to `(2,2)`:

    \draw (1,2) -- ++(norm cs: 3,0);

If one wants to specify the point that is `1cm` from `(1,2)` to `(3,0)` one needs to use the `from` parameter

    \draw (1,2) -- ++(norm cs: 3,0 from 1,2);

or the `norm` `to path`:

    \draw (1,2) to[norm] (3,0);

## Shapes
### PGF/TikZ library `qrr.shapes.openrectangle`
**Load with** either:

    \usepgflibrary{qrr.shapes.openrectangle}
    \usetikzlibrary{qrr.shapes.openrectangle}

**Files:**

 1. [`pgflibraryqrr.shapes.openrectangle.code.tex`](pgflibraryqrr.shapes.openrectangle.code.tex)
 2. [`tikzlibraryqrr.shapes.openrectangle.code.tex`](tikzlibraryqrr.shapes.openrectangle.code.tex)

**Inspiration:** [Tikz shape similar to rectangle with selective drawing of borders][sh-openrectangle-insp]

[**Example:**][sh-openrectangle-ex-out]
```latex
\documentclass[tikz]{standalone}
\usetikzlibrary{chains} \usetikzlibrary{qrr.shapes.openrectangle}
\tikzset{nodes={rounded corners, text height=\heightof{f}, text width=\widthof{aaaa}, ultra thick, draw, open rectangle fill=blue!40, shape=open rectangle,
  append after command={(\tikzlastnode.south west) edge[to path={rectangle (\tikztotarget)}, very thin] (\tikzlastnode.north east)}}}
\begin{document}
\begin{tikzpicture}[x=1.1cm, Start chain/.style={start chain=ch#1 going below}, Start chain/.list={1,...,4}, node distance=+2pt]\ttfamily
\foreach \ch/\si in {1/{e, n, w, s},
                     2/{nws, ews, ens, enw},
                     3/{en, nw, ws, es},
                     4/{, full, ew, ns}}
  \foreach \Si in \si
    \node[at=(right:\ch), on chain=ch\ch, open rectangle sides=\Si] {\Si};
\end{tikzpicture}
\end{document}
```

### PGF/TikZ library `qrr.shapes.roundedrectangle`
**Load with** either:

    \usepgflibrary{qrr.shapes.roundedrectangle}
    \usetikzlibrary{qrr.shapes.roundedrectangle}

**Files:**

 * [`pgflibraryqrr.shapes.roundedrectangle.code.tex`](pgflibraryqrr.shapes.roundedrectangle.code.tex)
 * [`tikzlibraryqrr.shapes.roundedrectangle.code.tex`](tikzlibraryqrr.shapes.roundedrectangle.code.tex)

**Inspiration:** [Wie kann ich mit TikZ Node-Formen zeichnen, die entgegengesetzt abgerundet sind?][sh-roundedrectangle-insp]

[**Example:**][sh-roundedrectangle-ex-out]
```latex
\documentclass[tikz]{standalone}
\usetikzlibrary{qrr.shapes.roundedrectangle}
\tikzset{shape example/.style={
  color=black!30,draw,fill=yellow!30,line width=.1cm,inner xsep=2.5cm,inner ysep=0.5cm}}
\begin{document}
\begin{tikzpicture}[
  rectangle with rounded corners mode={o,i,h,v},
  rectangle with rounded corners radius={40pt,10pt,20pt,30pt}
  ]\Huge
  \node[shape example,rectangle with rounded corners,name=s]{Rectangle\vrule width 1pt height 2cm};
  \foreach \anchor/\placement in {north west/above left, north/above, north east/above right,
                                  west/left, center/above, east/right,
                                  mid west/right, mid/above, mid east/left,
                                  base west/left, base/below, base east/right,
                                  south west/below left, south/below, south east/below right,
                                  text/left, 10/right, 130/above%
                                 }
  \draw[shift=(s.\anchor)] plot[mark=x] coordinates{(0,0)} node[\placement] {\scriptsize\texttt{(s.\anchor)}};
\end{tikzpicture}
\end{document}
```
[nf-code]: tikzlibrarynode-families.code.tex
[nf-insp]: http://tex.stackexchange.com/q/107227/16595
[nf-ex-out]: https://i.stack.imgur.com/9fb2y.png
[nf-more-examples]: https://tex.stackexchange.com/search?q=user%3A16595+node-families
[po-code1]: tikzlibraryqrr.paths.ortho.code.tex
[po-code2]: tikzlibraryqrr.paths.ortho.tex
[po-insp1]: https://tex.stackexchange.com/q/45347/16595
[po-insp2]: https://tex.stackexchange.com/q/102385/16595
[po-insp3]: https://texwelt.de/fragen/1289
[po-ex]: https://tex.stackexchange.com/search?q=user%3A16595+paths.ortho
[timer-code]: tikzlibraryqrr.paths.timer.code.tex
[timer-insp1]: https://tex.stackexchange.com/q/106558/16595
[timer-insp2]: https://tex.stackexchange.com/a/543268/16595
[pi-code]: tikzlibrarypatterns.images.code.tex
[pi-insp]: https://tex.stackexchange.com/q/103980/16595
[sh-openrectangle-insp]: https://tex.stackexchange.com/q/140842/16595
[sh-openrectangle-ex-out]: https://i.stack.imgur.com/V8oS6.png
[sh-roundedrectangle-insp]: https://texwelt.de/fragen/1180
[sh-roundedrectangle-ex-out]: https://texwelt.de/upfiles/de1180-0_1.png

[^lineto]: TikZ uses the same timer `\tikz@timer@line` that's used for `--` also for `rectangle`. Without patching `\tikz@rect@B` this can't be changed.
