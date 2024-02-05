# Snippets

Temp snippet document until I get a solution made with LuaSnip's `snippet_list`. It may be a bit terse, so feel free to make an issue or reformat it.

> :warning: **Warning:** As mentioned in the README, most snippets require [VimTeX](https://github.com/lervag/vimtex) for the condition/show-condition to work.

## `commands.lua`

### Labels/References
- `alab`: add label, of the form `\label{${1:type}:${2:number}}$0`
- `[acCer]ref`: add reference of the form `\(auto|c|C|eqn)ref{${1:type}:${2:number}}$0`
    * `cref/Cref` requires the `cleveref` package

### Single-Command Snippets
All of them are of the form `\COMMAND_NAME{$1}$0`, with those with `*` also having labels of the form `\label{type:${1:number}}`

- `sec(*)`, `ssec(*)`, `sssec(*)`*: section, subsection, subsubsection respectively. Add `*` for the starred commands.
- `sq`, `qq`: enquote* and enquote (single and double quotes). Requires `csquotes` package.
- `bf`, `it`, `ttt`, `sc`, `tu`, `tov`: Text modifications (bold, italic, typewriter, small caps, underline, and overline).

## `environments.lua`

`beg` creates a generic environment snippet.

```tex
\begin{$1}
$0
\end{$1}
```

`-i` creates the itemize environment, and there's a choice of which bullet point to set (either default or custom bullets with `\item []` notation).

```tex
\begin{itemize}
\item ${1:[$2]|}
\end{itemize}
```

`-e` deals with the enumerate environment. This one is a bit more involved than the itemize environment snippet, as it allows you to choose which labels and provides two defaults, lowercase roman numerals and lowercase alphabetical characters.
```tex
\begin{enumerate}${1:|[label=${2:(\alph*)|(\roman*)|}]}
\item ${3:[$4]|}
\end{enumerate}
```

`--`, `!-` are the accompanying commands for bullet points, which map to `\item` and `\item []` respectively. These only work at the beginning of the line in itemize/enumerate environments.


## `math.lua`

### Entering Math Mode
- `mk`: inline math `$$1$$0`
- `dm`: display math
- `ali`: align(|*|ed)
- `gat`: gather(|*|ed)
- `eqn`: equation(|*)

### Useful Math Dynamic Snippets
`[bBpvV]mat(%d)x(%d)(a|r)`: creates a dxd matrix, either augmented or not. Requires [this fix](https://tex.stackexchange.com/a/2238) for augments.

For instance, `bmat2x2r` creates:
```tex
\begin{bmatrix}
$1 & $2 \\
$3 & $4 \\
\end{bmatrix}
```

`(%d)?cases`: creates a cases array with d rows; if no input is supplied it defaults to 2 rows.

For instance, `3cases` creates:
```tex
\begin{cases}
$1 & $2 \\
$3 & $4 \\
$5 & $6 
\end{cases}
```

## `math-commands.lua`
## Autobacksash

An automatic backslash `\` will be appended to the following commands (in math mode).

Autobackslash|
---|
arcsin|
sin
arccos
cos
arctan
tan
cot
csc
sec
log
ln
exp
ast
star
perp
sup
inf
det
max
min
argmax
argmin

## Greek Letters

Trigger| Tex | Output 
---|:---:|---
`;a` | `\alpha` | $\alpha$
`;b` | `\beta` |$\beta$
`;g` | `\gamma` |$\gamma$
`;d` | `\delta` |$\delta$
`;ee` | `\epsilon` |$\epsilon$
`;e` | `\varepsilon` |$\varepsilon$
`;z` | `\zeta` |$\zeta$
`;et` | `\eta` |$\eta$
`;th` | `\theta`|$\theta$
`;vth`| `\vartheta` | $\vartheta$
`;i` | `\iota` | $\iota$
`;k` | `\kappa` | $\kappa$
`;l` | `\lambda` |$\lambda$
`;m` | `\mu` |$\mu$
`;n` | `\nu` |$\nu$
`;x` | `\xi`|$\xi$
`;oc` | `\omicron` | $\omicron$
`;p` | `\pi` |$\pi$
`;r` | `\rho` |$\rho$
`;vr` | `\varrho`| $\varrho$
`;s` | `\sigma` |$\sigma$
`;ta` | `\tau` | $\tau$
`;u` | `\upsilon` | $\upsilon$
`;ph` | `\phi` | $\phi$
`;vph` | `\varphi` |$\varphi$
`;c` | `\chi` | $\chi$
`;ps` | `\psi` | $\psi$
`;o` | `\omega` |$\omega$

Trigger| Tex | Output 
---|:---:|---
`;G` | `\Gamma` |$\Gamma$
`;D` | `\Delta` |$\Delta$
`;TH` | `\Theta`|$\Theta$
`;L` | `\Lambda` |$\Lambda$
`;X` | `\Xi`|$\Xi$
`;P` | `\Pi` |$\Pi$
`;S` | `\Sigma` |$\Sigma$
`;U` | `\Upsilon` | $\Upsilon$
`;PH` | `\Phi` | $\Phi$
`;PS` | `\Psi` | $\Psi$
`;O` | `\Omega` |$\Omega$

## Superscripts

To use the following, insert a word, then the trigger:
`<prefix><trigger>`

Trigger| Tex | Output 
---|:---:|---
sr | `^2` | `<prefix>`$^2$
cb | `^3` | `<prefix>`$^3$
compl | `^{c}` | `<prefix>`$^{c}$
vtr | `^{T}` | `<prefix>`$^{T}$
inv | `^{-1}` | `<prefix>`$^{-1}$

## Multi-Argument Functions

#### Fractions

The trigger for fractions is `//`. The tex will be of the form

`\frac{<>}{<>}`

If you place a value first, then you can use `/` to fill in the rest: `<stuff>/<otherstuff>`

#### Limits

The trigger for limits is `lim`. The tex will be of the form
`\lim<><><>`

#### Sum

The trigger for sums is `sum`. The tex will be of the form
`\sum<> <>`

#### Product

The trigger for products is `prod`. The tex will be of the form
`\prod<> <>`

#### Coproduct

The trigger for coproducts is `cprod`. The tex will be of the form
`\coprod<> <>`

#### Sets

The trigger for sets is `set`. The tex will be of the form
` \{<>\}`

#### Big Unions

The trigger for big unions (bigcup) is `nnn`. The tex will be of the form
`\bigcap<> <>`

#### Big Intersections

The trigger for big intersections (bigcap) is `uuu`. The tex will be of the form
`\bigcup<> <>`

#### Binomial

The trigger for n choose k  is `bnc`. The tex will be of the form
`\binom{<>}{<>}`

#### Partial Derivatives

The trigger for partial derivatives (Legendre notation) is 
`pd`. The tex will be of the form `\frac{\partial <>}{\partial <>}`

## Symbols

Trigger| Tex | Output 
---|:---:|---
`!=` | `\neq` |$\neq$
`<=` | `\leq`  |$\leq$
`>=` | `\geq` |$\geq$
`<<` | `\ll` |$\ll$
`>>` | `\gg` |$\gg$
`~~` | `\sim` |$\sim$
`~=` | `\approx` |$\approx$
`~-` | `\simeq` |$\simeq$
`-~` | `\backsimeq` |$\backsimeq$
`-=` | `\equiv`|$\equiv$
`=~` | `\cong` |$\cong$
`:=` | `\definedas` |$\definedas$
`**` | `\cdot`|$\cdot$
`xx` | `\times`|$\times$
`!+` | `\oplus`|$\oplus$
`!*` | `\otimes`|$\otimes$
`NN` | `\mathbb{N}`|$\mathbb{N}$
`ZZ` | `\mathbb{Z}`|$\mathbb{Z}$
`QQ` | `\mathbb{Q}`|$\mathbb{Q}$
`RR` | `\mathbb{R}`|$\mathbb{R}$
`CC` | `\mathbb{C}`|$\mathbb{C}$
`OO` | `\emptyset`|$\emptyset$
`pwr` | `\powerset`|$\powerset$
`cc` | `\subset`|$\subset$
`cq` | `\subseteq`|$\subseteq$
`qq` | `\supset`|$\supset$
`qc` | `\supseteq`|$\supseteq$
`\\\\\\` | \setminus|$\setminus$
`Nn` | `\cap`|$\cap$
`UU` | `\cup`|$\cup$
`::` | `\colon`|$\colon$
`AA` | `\forall`|$\forall$
`EE` | `\exists`|$\exists$
`inn` | `\in`|$\in$
`notin` | `\not\in`|$\not\in$
`!-` | `\lnot`|$\lnot$
`VV` | `\lor`|$\lor$
`WW` | `\land`|$\land$
`!W` | `\bigwedge`|$\bigwedge$
`=>` | `\implies`|$\implies$
`=<` | `\impliedby`|$\impliedby$
`iff` | `\iff`|$\iff$
`->` | `\to`|$\to$
`!>` | `\mapsto`|$\mapsto$
`<-` | `\gets`|$\gets$
`dp` | `\partial`|$\partial$
`-->` | `\longrightarrow`|$\longrightarrow$
`<->` | `\leftrightarrow`|$\leftrightarrow$
`2>` | `\rightrightarrows`|$\rightrightarrows$
`upar` | `\uparrow`|$\uparrow$
`dnar` | `\downarrow`|$\downarrow$
`ooo` | `\infty`|$\infty$
`lll` | `\ell`|$\ell$
`dag` | `\dagger`|$\dagger$
`+-` | `\pm`|$\pm$
`-+` | `\mp`|$\mp$

## Single Commands

Trigger| Tex  
---|:---:
`tt` | `\text`
`sbf` | `\symbf`
`syi` | `\symit` 
`udd` | `\underline`
`conj` | `\overline`
`__` | `_` 
`td` | `^` 
`sbt` | `\substack` 
`sq` | `\sqrt` 

## Postfix

`<stuff><trigger>`

Trigger| Tex
---|:---:
`mbb` | `\mathbb{} `
`mcal` | `\mathcal{}` 
`mscr` | `\mathscr{}`
`mfr` | `\mathfrak{}`
`hat` | `\hat{}` 
`bar` | `\overline{}`
`tld` | `\tilde{}`


## `delimiters.lua`

`lr(aAbBcmp)` creates a snippet of the form `\left[delim] $1 \right[delim] $0`; delimiters are created following this table:

```lua
-- brackets
local brackets = {
	a = { "\\langle", "\\rangle" },
	A = { "Angle", "Angle" },
	b = { "brack", "brack" },
	B = { "Brack", "Brack" },
	c = { "brace", "brace" },
	m = { "|", "|" },
	p = { "(", ")" },
}
```
