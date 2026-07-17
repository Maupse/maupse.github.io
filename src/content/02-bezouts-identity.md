---
title: "Bézouts Lemma"
pubDate: "2026-07-15"
description: "Proofing Bézouts lemma"
draft: true
---

- Replace the infinite case of the well-ordering proof because it currently uses min(X) while trying to prove that min(X) exists.
- Add the assumption that x is nonzero modulo p in the modular-inverse theorem.
- Remove the circular assumption xy = 1 + pk from the modular-inverse proof and instead obtain y and k from Bézout’s identity.
- Replace the congruence notation equiv_p with the standard notation equiv 1 pmod p.

## 1. Euclids Division Lemma
Let n be any natural number and let q be a positive integer.
Then there exist natural numbers k and r where $0 <= r < q$ satisfying:
$$
n = k \cdot q + r
$$

Proof.  

We will use induction.

[Base case]  
Let n = 0 and q be arbitrary, then
$0 = 0 * q + 0$, so $k=0,r=0$ satisfy the equation.

[Induction hypothesis]  
Suppose our proposition holds for an arbitrary fixed natural number z
and an arbitrary positive integer q.

[Induction step]  
Let z be some arbitrary natural number and let q be some arbitrary positive integer.
From our induction hypothesis we know that there exist k and r with 0 <= r < q s.t.
$z = k \cdot q + r$ | + 1
$(z+1) = k \cdot q + r + 1$.
Now there are two cases, either $r = q-1$ in which case $(r+1) = q$ or 
$r < q-1$ in which case $(r+1) < q$.

[case $(r+1) < q$]  
Then $(z+1) = k \cdot q + (r+1)$ satisfies the equation and we are done.

[case $(r+1) = q$]  
Then $(z+1) = k \cdot q + q = (k+1) \cdot q$ and we are done.

Thus the equation holds for $(z+1)$ and by the principle of mathematical induction
the equation therefore holds for all natural numbers n.
Since q was arbitrary it holds for all natrual numbers n and all positive integers q. $\square$


## 2. Bézouts Identity

### Infinite Descent
There is no sequence $(a_n)_{n=0}^\infty$ of natural numbers that is in infinite
descent, i.e. $a_{n+1} < a_n$ for all n.

Proof.  
Suppose there was a sequence in infinite descent, lets call it $(a_n)_{n=0}^\infty$.
We will use induction to proof that $\forall n,k. a_n \geq k$ by inducting on k.

[Base case]  
$a_n \geq 0$ since all $a_n$ are natural numbers.

[Induction hypothesis]  
Suppose that $a_n \geq k$ for all natural numbers n and an arbitrary but fixed
natural number k.

[Induction step]  
Let n be arbitrary. By the induction hypothesis, $a_{n+1} \geq k$.
Since $(a_n)_{n=0}^\infty$ is in infinite descent,
$a_n > a_{n+1} \geq k$, so $a_n > k$.
Thus $a_n \geq (k+1)$ and by the prinicple of mathematical induction
and because $n$ was arbitrary we know that $a_n \geq k$ for all n and all k.

But that is a contradiction, since any $a_n$ is a natural number and there
can be no natural number greater than all natural numbers. $\square$

### Well-ordering principle
Let $X \subseteq \mathbb N$ be a non-empty subset of the natural numbers.
Then X has a minimum element.

Proof.  

X is either finite or countable.  
Suppose X is finite.  

[Base case $\#X = 1$]  
Then $X = \{x\} for some natural number x.  
This element is trivially a minimum of X.

[Induction hypothesis]  
Suppose for arbitrary $k \in \mathbb N$ that if X is a subset of the natural
numbers and $\#X = k$ then it has a minimum element.

[Induction step]  
Let Y be a subset of the natural numbers such that $\#Y = k+1$, then
$Y = X \cup \{x\} for some set $X$ where $\#X = k$.  
Thus by the induction hypothesis this set has a minimum element,
let $m:= min(X)$ be that element.

Then either $x \leq m$ in which case $x \leq y$ for all y in Y,
or $x > m$ in which case $m \leq y$ for all y in Y.

Thus Y has a minimum element. $\triangle$

Now suppose that X is infinite.  
Since X is non-empty we can choose some x in X.  
Let $a_0 := x$.  
Now define $X_0 := X$ and $X_n := X \setminus \{a_i \mid i < n\}$.

$X_n$ cannot have a minimum since if it had, since \{a_i \mid i < n\} is finite,
we could use $min(min(X_n), min(\{a_i \mid i < n\}))$ which would be a minimum of X.

Therefore, $X_n$ always must have one element that is smaller than all elements in $\{a_i \mid i < n\}$, let us pick on of those elements, call it $y \in X_n$.

Then we define $a_n$ to be that $y$.

Thus $a_{n+1} < a_{n}$ for all n, but that is a contradiction, there is no sequence
of natural numbers in infinite descent.

We conclude that $X$ must have a minimum element. $\square$


### Bézouts Indentity
$\exists k, k'. gcd(a, b) = ka + k'b$

Proof.  

Let $a, b$ be two arbitrary natural numbers such that they are not both 0.
Let $g := \min\{ka + k'b \mid k, k' \in \mathbb Z \land ka + k'b > 0\}$.  

**Existence**  
This set is always non-empty, since one of a or b are not 0 and if
$k=k'=1$ the element will be greater than 0, thus there exist $k$ and $k'$
such that $g = ka + k'b$.

**1. g divides both a and b**  
Suppose g does not divide a, the case for b follows by similarity.  
Then $a = gl + r$ for some positive integer r where $0 < r < g$
by euclids division lemma, since $r \neq 0$ because $g \nmid a$.

So $a = (ka +k'b)l + r = kal + k'bl + r$.  
Rearranging we get: 
$a - kal - k'bl = r$
$\iff a(1 - kl) + (-k'l)b = r$  
But that is a linear combination of a and b which is greater than 0 and therefore in the set that g is the minimum of, a contradiction, since $r < g$ can't be true.

We conclude that $g \mid a, b$. $\triangle$

**2. Every divisor of both a and b divides g**  
Let c be a common divisor of a and b.

$g = ka + k'b$ for some integers $k, k'$  
$\iff g = k(cl) + k'(cl')$ for integers $k, k', l, l'$  
$\iff g = c(kl + k'l')$, meaning $c \mid g$ as desired. $\triangle$

**3. g is the greatest common divisor of a and b**  
For both the arithmetic and divisor definitions, (1.) and (2.) suffice to
conclude that, since if a number divides g then it must be smaller or equal to g.

Thus g is the greatest common divisor of a and b. $\square$

## 3. Existence of inverses modulus a prime
Let p be a prime number and let x be some integer.

Then $\exists y \in \mathbb Z. xy \equiv_p 1$

Proof.  
Let x be an arbitrary integer in $\mathbb Z_p$ and p be some prime number.  
Then $xy = 1 + pk$ for some integer k.
Equivalently $xy + (-k)p= 1$, since p is prime $gcd(p, x) = 1$, thus
$xy + (-k)p = gcd(x, p)$.

By Bézouts lemma, there are integers $y, -k$ that satisfy this equation. $\square$