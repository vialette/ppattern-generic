# PPattern :

## Permutations

### Basic manipulation

```haskell
λ: import qualified Data.Algorithm.PPattern.Perm as Perm
λ: let p = Perm.mk "acedb"
λ: p
[1,3,5,4,2]
λ: Perm.annotations p
"acedb"
λ: Perm.toList p
[T (Point (1,1),'a'),T (Point (2,3),'c'),T (Point (3,5),'e'),T (Point (4,4),'d'),T (Point (5,2),'b')]
λ: Perm.toPoints p
[Point (1,1),Point (2,3),Point (3,5),Point (4,4),Point (5,2)]
λ: Perm.xCoords p
[1,2,3,4,5]
λ: Perm.yCoords p
[1,3,5,4,2]
λ:
```

As you might have guessed, `show`reduces to `yCoords`:

```haskell
instance Show (Perm a) where
  show = show . yCoords
```

### Basic properties


### Ties

```haskell
λ: import qualified Data.Algorithm.PPattern.Perm as Perm
λ: let p = Perm.mk "ababc"
λ: p
[1,3,2,4,5]
λ:
```

### Transforming permutations

```haskell
λ: import qualified Data.Algorithm.PPattern.Perm as Perm
λ: let p = Perm.mk [3,5,7,1,8,4,2,6]
λ: Perm.reversal p
[6,2,4,8,1,7,5,3]
λ: Perm.complement p
[6,4,2,8,1,5,7,3]
λ: Perm.reversalComplement p
[3,7,5,1,8,2,4,6]
λ: Perm.inverse p
[4,7,1,6,2,8,3,5]
λ:
```

### Composing permutations

#### Sums

In combinatorics, the skew sum and direct sum of permutations are two operations
to combine shorter permutations into longer ones. Given a permutation <img alt="$\pi$" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/f30fdded685c83b0e7b446aa9c9aa120.svg?invert_in_darkmode" align=middle width="9.922935000000003pt" height="14.102549999999994pt"/> of
length <img alt="$m$" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/0e51a2dede42189d77627c4d742822c3.svg?invert_in_darkmode" align=middle width="14.379255000000002pt" height="14.102549999999994pt"/> and the permutation <img alt="$\sigma$" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/8cda31ed38c6d59d14ebefa440099572.svg?invert_in_darkmode" align=middle width="9.945705000000002pt" height="14.102549999999994pt"/> of length <img alt="$n$" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/55a049b8f161ae7cfeb0197d75aff967.svg?invert_in_darkmode" align=middle width="9.830040000000002pt" height="14.102549999999994pt"/>, the skew sum of <img alt="$\pi$" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/f30fdded685c83b0e7b446aa9c9aa120.svg?invert_in_darkmode" align=middle width="9.922935000000003pt" height="14.102549999999994pt"/> and
<img alt="$\sigma$" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/8cda31ed38c6d59d14ebefa440099572.svg?invert_in_darkmode" align=middle width="9.945705000000002pt" height="14.102549999999994pt"/> is the permutation of length <img alt="$m + n$" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/bfc06c99d626d9ab5e6e152d22661507.svg?invert_in_darkmode" align=middle width="44.25267pt" height="19.10667000000001pt"/> defined by
<p align="center"><img alt="$$&#10;  (\pi \ominus \sigma)(i) =&#10;    \begin{cases}&#10;      \pi(i)+n     &amp; \text{for } 1\leq i\leq m,\\&#10;      \sigma (i-m) &amp; \text{for } m+1\leq i\leq m+n,&#10;    \end{cases}&#10;$$" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/66a478f811a8a009451d9ce715cb7654.svg?invert_in_darkmode" align=middle width="351.49454999999995pt" height="49.131389999999996pt"/></p>

<!-- and the direct sum of π and σ is the permutation of length m + n defined by
{\displaystyle (\pi \oplus \sigma )(i)={<p align="center"><img alt="\begin{cases}\pi (i)&amp;{\text{for }}1\leq i\leq m,\\\sigma (i-m)+m&amp;{\text{for }}m+1\leq i\leq m+n.\end{cases}" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/7387bcd3b1c905b9aed066e22afbe315.svg?invert_in_darkmode" align=middle width="293.11589999999995pt" height="49.131389999999996pt"/></p>}} (\pi \oplus \sigma )(i)={<p align="center"><img alt="\begin{cases}\pi (i)&amp;{\text{for }}1\leq i\leq m,\\\sigma (i-m)+m&amp;{\text{for }}m+1\leq i\leq m+n.\end{cases}" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/7387bcd3b1c905b9aed066e22afbe315.svg?invert_in_darkmode" align=middle width="293.11589999999995pt" height="49.131389999999996pt"/></p>}
 -->

```haskell
λ: import qualified Data.Algorithm.PPattern.Perm as Perm
λ: import qualified Data.Algorithm.PPattern.Perm.Sum as Perm.Sum
λ: let p = Perm.mk [2,4,1,3]
λ: let q = Perm.mk [3,5,1,4,2]
λ: Perm.Sum.skewSum p q
[7,9,6,8,3,5,1,4,2]
λ: Perm.Sum.directSum p q
[2,4,1,3,7,9,5,8,6]
λ:
```

### Basic statistics

```haskell
λ: import qualified Data.Algorithm.PPattern.Perm as Perm
λ: import qualified Data.Algorithm.PPattern.Perm.Statistics as Perm.Statistics
λ: let p = Perm.mk [7,5,3,8,2,1,4,9,6]
λ: Perm.Statistics.leftToRightMinima p
[7,5,3,2,1]
λ: Perm.Statistics.leftToRightMaxima p
[7,8,9]
λ: Perm.Statistics.rightToLeftMinima p
[1,4,6]
λ: Perm.Statistics.rightToLeftMaxima p
[9,6]
λ: Perm.Statistics.ascents p
[3,1,4]
λ: Perm.Statistics.doubleAscents p
[1]
λ: Perm.Statistics.descents p
[7,5,8,2,9]
λ: Perm.Statistics.doubleDescents p
[7,8]
λ: Perm.Statistics.peaks p
[8,9]
λ: Perm.Statistics.valleys p
[3,1]
λ:
```

### Permutation graphs

## Pattern matching

### Generic pattern matching

### Monotone patterns

### Separable patterns

### Size-3 patterns

### Size-4 patterns

## Permutation classes

### Separable permutations

A separable permutation is a permutation that can be obtained from the trivial
permutation 1 by direct sums and skew sums;
separable permutations may be characterized by the forbidden permutation patterns
2413 and 3142
(see <https://en.wikipedia.org/wiki/Separable_permutation>).

```haskell
λ: import qualified Data.Algorithm.PPattern.Perm as Perm
λ: import qualified Data.Algorithm.PPattern.SeparatingTree as SeparatingTree
λ: let p = Perm.mk [3,1,4,2,6,5,7]
λ: -- p does not avoid 2413 and 3142, and hence is not separable
λ: Perm.isSeparable p                  
False
λ: -- so that no separating tree of p can be obtained
λ: SeparatingTree.mk <img alt="$ Perm.toPoints p&#10;Nothing&#10;λ: let q = Perm.mk [3,1,2,4,6,5,7]&#10;λ: Perm.isSeparable q                             -- q does avoid 2413 and 3142, and hence is separable&#10;True&#10;λ: import Data.Maybe&#10;λ: fromJust . SeparatingTree.mk $" src="https://rawgit.com/in	git@github.com:vialette/ppattern/master/svgs/c7be5bdfada4253d65cf69b07d4cdacb.svg?invert_in_darkmode" align=middle width="1011.5407499999999pt" height="45.82083000000002pt"/> Perm.toPoints q -- so that a separating tree of q can be obtained
+ Interval (1,7)
.+ Interval (1,6)
..+ Interval (1,4)
...- Interval (1,3)
....Point (1,3)
....+ Interval (1,2)
.....Point (2,1)
.....Point (3,2)
...Point (4,4)
..- Interval (5,6)
...Point (5,6)
...Point (6,5)
.Point (7,7)

λ:
```

### (213,231)-avoiding patterns

## Computing a base
