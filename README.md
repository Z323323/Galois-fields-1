# Galois fields

This resource extracts every non-trivial result (basically everything) from [https://web.stanford.edu/~marykw/classes/CS250_W19/readings/Forney_Introduction_to_Finite_Fields.pdf] + provides some insights regarding non intuitive concepts (where possible).

![MEP3](MEP3.jpg)

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

In multiplicative notation, the elements of a cyclic group $G$ of order $n$ with generator $g$ are denoted by $\\{ g^{0} = 1, g^{1}, g^{2}, \dots, g^{n - 1} \\}$, the multiplication rule is $g^{i} \otimes g^{j} = g^{(i + j) \mod n}$, the identity is $g^{0} = 1$ and the inverse of $g^{i} \neq 1$ is $g^{n - i}$ (perhaps the easiest way to find an inverse, even though is computationally heavy).

For example if $\omega = e^{2\pi i / n}$, the set $\\{ 1, \omega, \omega^{2}, \dots, \omega^{n - 1} \\}$ of complex nth roots of unity is a cyclic group under complex multiplication, isomorphic to $Z_{n}$.

### 7.3.3 Subgroups

A subgroup $S$ of a group $G$ is an algebraic structure such that $S$ is itself a group and $S \subseteq G$. For any $g \in G$ (not necessarily generators for $G$) we define the coset (translate) $S \oplus g = \\{ s \oplus g | s \in S \\}$ (where $| =$ 'such that' in this case). We also have $S \oplus 0 = S$ and $S \oplus g = S$ iff $g \in S$.

This resource is probably not the best to really grasp subgroups (I think it's a little bit advanced), I strongly recommend to play around with [https://github.com/Z323323/Group-theory-elements/blob/main/Zn.py].

**Lemma 7.3** Two cosets $S \oplus g$ and $S \oplus h$ are the same if $g - h \in S$ or disjoint if $g - h \not\in S$.

**Proof**. If $g - h \in S$ then the elements of $S \oplus h$ include $(g - h) \oplus h = g$ and therefore all elements of $S \oplus g$ (remember that this means that we can represent the whole set as $\\{ (g - h) \oplus h = g \otimes 1, g \otimes 2, \dots, g \otimes n \\}$) so $S \oplus g \subseteq S \oplus h$. Also, since $g - h \in S$ then $n - g + h \in S$ and $\\{ (n - g + h) \oplus g = h \otimes 1, h \otimes 2, \dots, h \otimes n \\} = S$, thus $S \oplus h \subseteq S \oplus g$ and therefore $S \oplus g = S \oplus h$. 

Otherwise if $g - h \not\in S$, then $g - h \oplus h = g$ implies $g \not\in S$ and $n - g + h \oplus g$ implies $h \not\in S$; this means that $g$ doesn't share cofactors with $h$ and this means that the two subgroups are disjoint. This is clearer if you look at [https://github.com/Z323323/Group-theory-1/blob/main/README.md#additive-cyclic-groups].

It follows that the distinct cosets $S \oplus g$ and $S \oplus h$ of a subgroup $S \subseteq G$ form a disjoint partition of $G$, since every element $g \in G$ lies in some coset, namely $S \oplus g$.

The elements $s \oplus g$ of a coset $S \oplus g$ are all distinct, since $s \oplus g = s' \oplus g$ implies $s = s'$. Therefore if $S$ is finite then all cosets of $S$ have the same size, namely the size $|S|$ of $S = S \oplus 0$ (basically we can define $S$ cosets taking some $k \neq g$ which shares the same cofactors with $n$ and computing $S \oplus k | k \in S$; since $k$ and $g$ share the same cofactors with $n$ they produce a set which has order $|S|$). If $G$ is finite then is the disjoint union of a finite number $|C|$ of cosets of $S \subseteq G$, each of size $|S|$ (this doesn't mean they'll all have the same size, $|S|$ is a general form here), so $|G| = |C||S|$.

**Theorem 7.4 (Lagrange)** If $S$ is a subgroup of a finite group $G$, then $|S|$ divides $|G|$. This derives simply from the fact that the order of cosets depends on cofactors between the generators and the order $n$ of $G$ (not so easy for multiplicative groups though [https://github.com/Z323323/Group-theory-elements/tree/main?tab=readme-ov-file#lagranges-theorem]). Additive and multiplicative finite groups are more similar than what it might seem at first.

### 7.3.4 Cyclic subgroups

Let $g$ be some element of a group $G$; then $S(g) = \\{ g, g \oplus g, \dots \\}$ is a cyclic subgroup of $G$. We have $|S(m)| = n / gcd(n, m)$ (or $|S(m)| = lcm(n, m) / m$). We have $S(m) = Z_{n}$ iff $gcd(n, m) = 1$, that is, $n$ is prime, or $n$ and $m$ are coprime. We have $\phi(n)$ subgroups of order $n$. $\\{ 0 \\}$ is always of order $1$, and $\\{ 1 \\}$ of order $n$. In general, $Z_{n}$ has a cyclic subgroup $S_{d}$ of order $d$ for each integer $d$ that divides $n$, including $1$ and $n$. $S_{d} = \\{ 0, n / d, 2n / d, \dots, (d - 1)n / d \\}$ and is isomorphic to $Z_{d}$. $S_{d}$ contains $\phi(d)$ elements that are relatively prime to $d$, each of which has order $d$ and generates $S_{d}$. The remaining elements of $S_{d}$ belong also to smaller cyclic subgroups. This last two sentences are not the easiest to digest; to better explain them, the first one is because every element necessarily shares the same cofactors as the generator, thus taking those elements which don't share any other cofactor with $n$ (because they are coprime with $d$) we are basically taking elements of the same order of the generator; the second one is the opposite of the first, that is, numbers which share some other cofactor with $n$ will have necessarily a smaller order $(orderOfGenerator / furtherSharedCofactor(s))$. Since every element of $Z_{n}$ has some definite order $d$ that divides $n$, we have $n = \sum_{d | n} \phi(d)$. This last formula is not simple at all at first, I have a 'simple' proof of it at [https://github.com/Z323323/Number-theory-interlude-2?tab=readme-ov-file#sum_d--n-phid--n]. In this context I guess this formula can even be easier to get, since from the previous reasoning, for every divisor $d$ of $n$ we have $\phi(d)$ elements which have the same order, if we sum up all the $\phi(d)$ we end up having the number of elements of $Z_{n}$, that is, $n$. It's even less intuitive than this actually, because doing so we would get $n - 1$ not $n$, since the Totient function doesn't consider the $0$, but it's also true that we are considering only $n - 1$ numbers, and so we can safely add $\phi(0) = 1$ obtaining $n$.

### 7.4 Fields

A field is a set $F$ of at least two elements, with two operations $\oplus, \otimes$, for which the following axioms are satisfied:

- The set $F$ forms an abelian group under the operation $\oplus$ (identity: $0$).
- The set $F^{\star} = F - \\{ 0 \\} = \\{ a \in F, a \neq 0 \\}$ forms an abelian group (identity: $1$) under the operation $\otimes$.
- For all $a, b, c \in F, (a \oplus b) \otimes c = (a \otimes c) \oplus (b \otimes c)$ (distributive law).

### 7.4.1 Prime fields

A fundamental example of a finite (Galois) field is the set $F_{p}$ of $mod-p$ remainders, where $p$ is prime.

**Theorem 7.5** For every prime $p$, the set $R_{p} = \\{ 0, 1, \dots, p - 1 \\}$ forms a field $(F_{p})$ under $mod-p$ addition and multiplication.

**Proof**. The proof is quite trivial, since we just proved that $mod-p$ ops form an additive group. For the multiplicative group the proof is quite simple and I'm not going to rewrite it, feel free to read it at linked document from Stanford. I also wrote something related at [https://github.com/Z323323/From-Fermat-to-the-group-theory?tab=readme-ov-file#proof-of-existence-and-uniqueness-of-inverses-in-z_p-and-z_phinast]. That document contains every non-trivial detail needed.

One interesting detail we can spot from the Stanford proof is that for any $a \in F_{p}, \\{a \otimes 1, a \otimes 2, \dots, a \otimes (p - 1)\\}$ forms a permutation of $F_{p}$.

**Inner theorem** $F_{p}$ is the only field with $p$ elements, and all fields with $p$ elements are isomorphic.

**Proof**. Two fields $F$ and $G$ are isomorphic if there is an invertible function $h: F \rightarrow G$ mapping each $\alpha \in F$ into $\beta = h(\alpha) \in G$ such that $h(\alpha \oplus \alpha ') = h(\alpha) \oplus h(\alpha ')$ and $h(\alpha \otimes \alpha ') = h(\alpha) \otimes h(\alpha ')$. Less formally, $F$ and $G$ are isomorphic if there is a one-to-one correspondence $F \leftrightarrow G$ that translate the addition and multiplication tables of $F$ to those of $G$ and viceversa.<br>
Let $F$ be any field with a prime $p$ number of elements. By the field axioms, $F$ has an additive identity $0$ and multiplicative identity $1$. Consider the additive cyclic subgroup generated by $1, S(1) = \\{ 1, 1 \oplus 1, \dots \\}$. By Lagrange's theorem, the order of $S(1)$ divides $|F| = p$, indeed it's trivially $p$, this means that $S(1) = F$, and the additive group is isomorphic to $Z_{p}$, thus we may denote $F$ by $(\\{ 0, 1, 2, \dots, p - 1 \\}, + \mod p, \star \mod p)$. The only remaining question is whether this correspondence $F \leftrightarrow Z_{p}$ under addition extends to multiplication (this is the main problem). The distributive law shows that it does: $j \otimes i$ is the sum of $j$ terms each equal to $i$, so $j \otimes i = (ji \mod p)$.

**Theorem 7.6** Every field $F$ with a prime number $p$ of elements is isomorphic to $F_{p}$ via the correspondence $1 \oplus \dots \oplus 1 \in F \leftrightarrow i \in F_{p}$.

In view of this elementary isomorphism, we will denote any field with a prime number $p$ elements by $F_{p}$. It's important to note that $Z_{n}$ does not form a field if $n$ is not prime. This is because $n = ab$ implies $ab \equiv 0 \mod n$, so the set of nonzero elements of $Z_{n}$ is not closed under multiplication mod $n$. Nonetheless we will see that there do exist finite fields with non-prime numbers of elements that use other rules for addition and multiplication (this is the main purpose of Galois fields). Homomorphisms and isomorpisms are really abstract concepts, I'll provide further analysis if required, but for the moment let's go over.

### 7.4.2 The prime subfield of a finite field

A subfield $G$ of a field $F$ is a subset of the field that is itself a field under the operations of $F$. Every finite field $F_{q}$ has a subfield that is isomorphic to a prime field $F_{p}$. Let $F_{q}$ be a finite field with $q$ elements; by the field axioms, $F_{q}$ has an additive identity $0$ and a multiplicative identity $1$. Consider now the cyclic subgroup of the additive group of $F_{q}$ that is generated by $1, S(1) = \\{ 1, 1 \oplus 1, \dots \\}$. We have $n = |S(1)|$. $S(1)$ is isomorphic to $Z_{n}^{+} = (\\{ 1, 2, \dots, n - 1 \\}, + \mod n)$. By the distributive law in $F_{q}$, $i \otimes j$ (in $F_{q}$) of two nonzero elements in $S(1)$ is simply the sum of $ij$ $1s$, which is an element of $S(1)$, namely $ij \mod n$. Since this is a product of nonzero elements of $F_{q}$ $ij \mod n$ must be non zero for every nonzero $i, j$. This will be true iff $n$ is prime.

Thus $S(1)$ forms a subfield of $F_{q}$ with a prime number $p$ of elements. By the prime field of the previous subesection, $S(1)$ is isomorphic to $F_{p}$. Thus the elements of $S(1)$, which are called the integers of $F_{q}$, may be denoted by $F_{p} = \\{ 0, 1, dots, p - 1 \\}$ and the addition and multiplication rules of $F_{q}$ reduce to $mod-p$ addition and multiplication in $F_{p}$.

The prime $p$ is called **characteristic** of $F_{p}$. Since the $p-fold$ sum of the identity $1$ with itself is $0$, the $p-fold$ sum of every field element $\beta \in F_{p}$ with itself is $0$: $p\beta = 0$.

**Theorem 7.7** The integers $\\{ 1, 1 \oplus 1, \dots \\}$ of any finite field $F_{q}$ form a subfield $F_{p} \subseteq F_{q}$ with a prime number $p$ of elements, where $p$ is the characteristic of $F_{q}$.


























