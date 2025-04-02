# Galois fields theory

This resources aims to simply extract every non-trivial result from [https://web.stanford.edu/~marykw/classes/CS250_W19/readings/Forney_Introduction_to_Finite_Fields.pdf].

### 7.2.2 Mod-n arithmetic

$r \equiv i \mod n$<br>
$->$<br>
$r = i + qn$<br>
$---$<br>
$s \equiv j \mod n$<br>
$->$<br>
$s = j + tn$<br>
$---$<br>
$->$<br>
$r + s = i + j + (q + t)n$<br>
$->$<br>
$r + s \equiv i + j \mod n$<br>
$---$<br>
$rs = ij + (qj + ti)n + qtn^{2}$<br>
$->$<br>
$rs \equiv ij \mod n$

### 7.3 Additive groups

The group operation $'+'$ can be specified by an $n \times n$ table whose entries are of the form $a_i + a_j$ (row $i$, column $j$). If $a_j \neq a_k$ then $a_i + a_j \neq a_i + a_k$ and this means that any elements in any row of the addition table are distinct, that is, each row contains each element of the group $G$ exactly once, and the same goes for the columns.

### 7.3.1 Alternative group axioms

The previously mentioned property of addition can be seen as a permutation of $G$, that is, each row of the table actually represents the set of the elements of $G$ in a different order. This property can be taken as one of the group axioms.

**Theorem 7.1** _Let $G = \{ a, b, c, \dots \}$ be a set of elements on which the addition operation is defined ($\mod$ something). Then $G$ is a group under the operation $+$ if and only if:_

- 
