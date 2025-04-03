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
$->$<br>
$r \oplus s$<br>
$---$<br>
$rs = ij + (qj + ti)n + qtn^{2}$<br>
$->$<br>
$rs \equiv ij \mod n$<br>
$->$<br>
$r \otimes s$

### 7.3 Additive groups

The group operation $\oplus$ can be specified by an $n \times n$ table whose entries are of the form $a_i \oplus a_j$ (row $i$, column $j$). If $a_j \neq a_k$ then $a_i \oplus a_j \neq a_i \oplus a_k$ and this means that any elements in any row of the addition table are distinct, that is, each row contains each element of the group $G$ exactly once, and the same goes for the columns.

### 7.3.1 Alternative group axioms

The previously mentioned property of addition can be seen as a permutation of $G$, that is, each row of the table actually represents the set of the elements of $G$ in a different order. This property can be taken as one of the group axioms.

**Theorem 7.1** Let $G = \{ a, b, c, \dots \}$ be a set of elements on which the $\oplus$ operation is defined. Then $G$ is a group under the operation $\oplus$ if and only if:

- The operation is associative.
- There is an indentity element.
- For each $a \in G$, $a \oplus G$ is a permutation of $G$.

**Proof**. Basically we can derive the existence and uniqueness of inverses starting from the latter property, and also the algebraic closure, making the algebraic structure an additive group.

### 7.3.2 Cyclic groups

Of couse it's always possible to find a generator $g$ for additive groups.

$1g = g, 2g = g \oplus g, \dots, ig = g \oplus_{iTimes} g, \dots$

Since $g$ is a generator we must have $i \otimes g = 0$ for some $i$. Let $n$ be the smallest integer $n$ such that $n \otimes g = 0$ and $i \otimes g \neq 0$ for $1 \leq i \leq n - 1$. Adding $j \otimes g$ for any $j > 0$ to each side of $i \otimes g \neq 0$ results in $(i + j) \otimes g \neq j \otimes g$. Thus the elements $\\{ 1g, 2g, \dots, ng = 0 \\}$ must all be different. We can also add $j \otimes g$ to both sides of $n \otimes g = 0$, yielding $(j + n) \otimes g = j \otimes g$ for any $j > 0$. Thus, for each $i > n$, $i \otimes g$ is equal to some earlier element in the sequence, namely $(i - n) \otimes g$. The elements $\\{ 1g, 2g, \dots, ng = 0 \\}$ therefore constitute all of the distinct elements in $G$, and the order of $G$ is $|G| = n$. If we define $0g$ to be the identity, then we can represent the whole set as $G = \\{ 0g, 1g, \dots, (n - 1)g \\}$.

Note that in general when referring to a normal sum or product, the corresponding $\oplus, \otimes$ are implied under the hood. Also, this part is a little bit tricky but explains a really simple concept which I covered in a simplified manner at [https://github.com/Z323323/Group-theory-1/blob/main/README.md#additive-cyclic-groups] (even though here some more details are present). The image below shows the previous reasoning graphically.

![Circle](Circle.png)

It now results pretty clear that any $i$ can be written as $i = qn + r$ where $(r \equiv i \mod n) \in \\{ 0, 1, \dots, n - 1 \\}$. We also have $ig = (qn)g + rg \equiv rg \mod n$. The addition rule of $G$ is thus as follows: for each $0 \leq i, j < n$ we have $ig \oplus jg = [(i + j) \mod n] \otimes g$. Thus, any cyclic group of order $n$ is essentially identical to $Z_{n}$.

The correspondence $i \otimes g \in G \leftrightarrow i \in Z_{n}$ is preserved under addition, i.e. $ig \oplus jg \leftrightarrow i \oplus j$ for each $i, j \in Z_{n}$. This correspondence is called an _isomorphism_. Specifically, two finite groups $G$ and $H$ are _isomorphic_ if there exists an invertible function [ a function is called _invertible_ if for each $\beta \in H$ there is a unique $\alpha \in G$ such that $\beta = h(\alpha)$ ] $h: G \rightarrow H$ mapping each $\alpha \in G$ into a $\beta = h(\alpha) \in H$ such that $h(\alpha \oplus \alpha ') = h(\alpha) \oplus h(\alpha ')$, where $\oplus$ denotes the group operation of $G$ on the left and that of $H$ on the right.

Omomorphism, isomorphisms etc. are not easy concepts but they can become more familiar with some time. I delved both in the previous article linked, even though I can't say if it could be better to look at that resource.

**Theorem 7.2** The elements of a cyclic group $G$ of order $n$ with generator $g$ are $\\{ 0g, 1g, \dots, (n - 1)g \\}$. The addition rule is $ig \oplus jg = [(i + j) \mod n] \otimes g$, the identity is $0g$ and the inverse of $ig \neq 0g$ is $(n - i) \otimes g$ (because $i \otimes g + (n - i) \otimes g = (n - i + i) \otimes g = n \otimes g = 0$). Finally, $G$ is isomorphic to $Z_{n}$ under the $1:1$ correspondence $ig \leftrightarrow i$.

Since $Z_{n}$ is abelian, it follows that all cyclic groups are abelian.

In multiplicative notation, the elements of a cyclic group $G$ of order $n$ with generator $g$ are denoted by $\\{ g^{0} = 1, g^{1}, g^{2}, \dots, g^{n - 1} \\}$ (here the definitive hint regarding primality of $n$), the multiplication rule is $g^{i} \otimes g^{j} = g^{(i + j) \mod n}$, the identity is $g^{0} = 1$ and the inverse of $g^{i} \neq 1$ is $g^{n - i}$ (perhaps the easiest way to find an inverse, even though is computationally heavy).

For example if $\omega = e^{2\pi i / n}$, the set $\\{ 1, \omega, \omega^{2}, \dots, \omega^{n - 1} \\}$ of complex nth roots of unity is a cyclic group under complex multiplication, isomorphic to $Z_{n}$.

### 7.3.3 Subgroups

A subgroup $S$ of a group $G$ is an algebraic structure such that $S$ is itself a group and $S \subseteq G$. For any $g \in G$ we define the coset (translate) $S \oplus g = \\{ s \oplus g | s \in S \\}$ (where $|$ = 'such that' in this case). We also have $S \oplus 0 = S$ and $S \oplus g = S$ iff $g \in S$.

This resource is probably not the best to really grasp subgroups (I think it's a little bit advanced), I strongly recommend to play around with [https://github.com/Z323323/Group-theory-elements/blob/main/Zn.py].

**Lemma 7.3** Two cosets $S \oplus g$ and $S \oplus h$ are the same if $g - h \in S$ or disjoint if $g - h \not\in S$ (here I guess $g$ and $h$ represent two different generators for the subgroup $S$).

**Proof**. If $g - h \in S$ then the elements of $S \oplus h$ include $(g - h) \oplus h = g$ and therefore all elements of $S \oplus g$ (remember that this means that we can represent the whole set as $\\{ (g - h) \oplus h = g \otimes 1, g \otimes 2, \dots, g \otimes n \\}$) so $S \oplus g \subseteq S \oplus h$. Also, since $g - h \in S$ then $n - g + h \in S$ and $\\{ (n - g + h) \oplus g = h \otimes 1, h \otimes 2, \dots, h \otimes n \\} = S$, thus $S \oplus h \subseteq S \oplus g$ and therefore $S \oplus g = S \oplus h$. 

Otherwise if $g - h \not\in S$, then $g - h \oplus h = g$ should produce the previous structure (the same goes for $n - g + h$) but this is impossible because $g - h \not\in S$, and therefore the resulting set can't be $S$. The fact they are disjoint I think that it's actually wrong, but I could be wrong.



















