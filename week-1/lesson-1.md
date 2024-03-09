# Overview / Maths & Cryptography Introduction

## [1] Some simple quotes before jumping in:

`"Human dignity demands that personal information, like medical and forensic data, be hidden from
the public. But veils of secrecy designed to preserve privacy may also be abused to cover up lies
and deceit by institutions entrusted with Data, unjustly harming citizens and eroding trust in central
institutions." - Starkware`

`"ZK gives out similar vibe as ML. More and more people just mention ZK as a magic solution that
fixes everything with no context of its current limitation." - 0xMisaka`

**TLDR:** 
1. ZK can help reduce abuse in systems as well as help with privacy and human dignity due to the zero knowledge aspect. 
2. Although the ZK buzzword sounds cool, there are scenarios where it can be applied well (good use case) and where it cannot be applied well. 

## [2] Introductory Maths 

This section contains various mathematical concepts/terminologies (not a specific branch of mathematics) that are relevant to understanding ZK. Think of it like a ZK cryptographer's toolbox. 

### [2.1] Numbers

When using ZK technology, we restrict ourselves in the types of numbers we use. Usually, we stick with integers. There are other sets than those mentioned below: 

The set of Integers is denoted by Z e.g. {⋯,−4,−3,−2,−1,0,1,2,3,4,⋯}

The set of Rational Numbers is denoted by Q e.g. {. . . 1, 3/2, 2, 22/7, . . . }

The set of Real Numbers is denoted by R e.g. {2, −4, 613, π, √2,…}

Fields are denoted by $F$. 

The set of numbers we are particularly interested in is represented by $Z^*_p$ (read as Z subscript p with an asterisk). This is a finite field of integers (which means there is a maximum value). The maximum value is 1 less than p (a prime number). When we do arithmetic for that field, we do it mod (modulus) that prime number. The * represents special properties of the field. In short, it is a representation of a finite field of integers mod prime p with multiplicative inverses.

**[2.1.1] Why are we interested in this particular field?**

It makes our lives easier. We use finite fields for cryptography, because elements have “short”, exact representations and useful properties.

### [2.2] Modular Arithmetic

Modular Arithmetic is sometimes referred to as "clock math" because of how numbers wrap around. 

When we write n mod k we mean simply the remainder when n is divided by k. Thus,

25 mod 3 = 1

15 mod 4 = 3

The remainder should be positive.

### [2.3] Group Theory

The concept of group theory is really abstract but the terms are usually used in ZK technology.

A group is a set of elements {a,b,c,...} plus a binary operation. The binary operation operates on two elements within that group.

To be considered a group, this combination needs to have certain properties. Below we represent the binary operation (+, -, /, ...) as •

1. Closure
  For all a, b in G, the result of the operation, a • b, is also in G
2. Associativity
  For all a, b and c in G, (a • b) • c = a • (b • c)
3. Identity element
  There exists an element e in G such that, for every element a in G, the equation e • a = a • e =
  a holds. Such an element is unique and thus one speaks of the identity element.
4. Inverse element
  For each a in G, there exists an element b in G, commonly denoted a−1 (or −a, if the operation
  is denoted "+"), such that a • b = b • a = e, where e is the identity element.

**[2.3.1] Sub groups**

If a subset of the elements in a group also satisfies the group properties, then that is a subgroup of the original group.

**[2.3.2] Cyclic groups and generators**

A finite group can be cyclic. That means it has a generator element. If you start at any point and apply the group operation with the generator as argument a certain number of times, you go
around the whole group and end in the same place.

**[2.3.3] Finding an inverse**

From Fermat's little theorem (way to find inverse element in a group where the operation is multiplication a.k.a multiplicative inverse).

Finding multiplicative inverses for finite fields that use modular arithmetic is not as easy as one thinks. But it can be made easier, if we use the following formula:

Let's say a is the element and $a^{-1}$ is the inverse of element a.

$a^{−1} ≡ a^{p−2}(modp)$

Let p = 7 and a = 2. We can compute the inverse of a as:

$a^{p−2} = 2^5$ = 32 ≡ 4 

The final answer is 4 since we apply modulo 7 on 32 i.e. 32 mod p = 32 mod 7 = 4 as remainder. Thus, for element a = 2, the $a^{-1}$ = 4.

This is easy to verify: $a * a^{-1}$ = 2 x 4 ≡ 8 (mod 7) = 1 (which is the identity element).

**[2.3.4] Equivalance classes**

Modular arithmetic and inverses splits up our number space into what are called equivalence classes.

In the above examples where we used p = 7, anytime we got a number that falls out of the finite field (which has max = p - 1 = 6), we used to apply mod p on it. **Note: Numbers even within the field range [0,6] have the mod p applied, except that the result is the number itself. Due to that, it's not necessary to explicitly mod p them.**

Since 6 mod 7 = 6, 13 mod 7 = 6, 20 mod 7 = 6 ..., we can say that 6, 13, 20 ... form an equivalence class

In short, numbers giving the same remainder on mod p form an equivalence class.

Thus if we are trying to solve the equation

x mod 7 = 6

x could be 6, 13, 20 ...

This gives us the basis for a one way function (many-to-one function).

### [2.4] Fields

A field is a set of say Integers together with two operations called addition and multiplication. For example, set of Real Numbers under addition and multiplication or set of
Integers mod a prime number with addition and multiplication.

The field operations are required to satisfy the following field axioms. In these axioms, a, b and c
are arbitrary elements of the field F.

1. Associativity of addition and multiplication: a + (b + c) = (a + b) + c and a · (b · c) = (a · b) · c.
2. Commutativity of addition and multiplication: a + b = b + a and a · b = b · a.
3. Additive and multiplicative identity: there exist two different elements 0 and 1 in F such that a + 0 = a and a · 1 = a.
4. Additive inverses: for every a in F, there exists an element in F, denoted −a, called the additive
inverse of a, such that a + (−a) = 0.
5. Multiplicative inverses: for every a ≠ 0 in F, there exists an element in F, denoted by $a^{−1}$, called the multiplicative inverse of a, such that a · $a^{−1}$ = 1.
6. Distributivity of multiplication over addition: a · (b + c) = (a · b) + (a · c).

**[2.4.1] What is the difference between groups and fields?**

Fields are similar to groups just that we have an extra operation. Fields can be thought of an extension of what we do with groups. 

In ZK technology/proving systems, we tend to work with finite fields.

**[2.4.2] Finite fields and generators**

A finite field is a field with a finite set of elements, such as the set of integers mod p where p is a prime number.

Try out operations on finite fields [here (includes some readings as well)](https://asecuritysite.com/encryption/finite).

A terminology to come across is the order of the field. The **order** of the field is the number of element's in the field's set. 

The order of the field is the number of elements in the field’s set.

For a finite field the order must be either:
 - prime ( a prime field)
  or
 - the power of a prime (an extension field)

An element can be represented as an integer greater or equal than 0 and less than the field’s
order: {0, 1, ..., p-1} in a simple field.

Every finite field has a generator (minimum 1). A generator is capable of generating all of the elements in the set by exponentiating the generator .

So for generator g we can take ${g^0}$, ${g^1}$, ${g^2}$ and eventually this will give us all elements in the group.


For example, taking the set of integers and prime p = 5, we get the group $Z^*_5 = {0,1,2,3,4}$.

In the group $Z^*_5$, operations are carried out modulo 5; hence, we don’t have 3 × 4 = 12 but instead have 3 × 4 = 2, because 12 mod 5 = 2.

$Z^*_5$ is cyclic and has two generators, 2 and 3, because $2^1$ = 2, $2^2$ = 4, $2^3$ = 3, $2^4$ = 1 and $3^1$ = 3, $3^2$ = 4, $3^3$ = 2, $3^4$ = 1.

In a finite field of order q, the polynomial $X^q − X$ has all q elements of the finite field as roots.

As we delve more into zero knowledge proofs and dig into the theory, we'll find out that it's pretty much all about polynomials. One of the very useful things we do with polynomials is to look at their roots and simplify them by expressing them in a certain way. 

**[2.4.3] Group Homomorphisms**

Another terminology that we'll come across is the idea of homomorphisms.

A homomorphism is a map between two algebraic structures of the same type, that preserves the
operations of the structures.

This means a map f : A → B between two groups $A$, $B$ equipped with the same structure such that,
if ⋅ is an operation of the structure (here a binary operation), then
f(x ⋅ y) = f(x) ⋅ f(y)


## [3] Cryptography Background

### [3.1] Hash functions

Hash functions are one-way functions. For the same input, you receive the same digest. For different inputs, you receive different outputs/digests (extremely low-probability of hash collisions).

Input => Hash Function => Digest

It's easy to go from input to digest but not the other way around. The only way to do this is through brute force and trying out all possibilities. 

### [3.2] Encryption

**Symmetric Encryption**

Alice and Bob encrypt and decrypt messages using a shared key.

**Asymmetric Encryption**

Both Alice and Bob have a public-private key pair. 

1. Messaging: Alice encrpyts a message using Bob's public key and bob decrypts it using his private key.
2. Alice signs a message with her private key and Bob decrypts it using her public key.

### [3.3] Verifiable Random Functions

A Verifiable Random Function (VRF) is a cryptographic primitive (function) that maps inputs to verifiable
pseudorandom outputs

A better explanation about these can be found [here](https://medium.com/algorand/algorand-releases-first-open-source-code-of-verifiable-random-function-93c2960abd61).

### [3.4] Elliptic Curves

People choose a particular curve because it provides useful properties to the system they're building on that curve (for example, maybe some shortcuts or good performance etc). 

An elliptic curve is a set of points $(x, y)$ that satisfy an equation such as:

$y^2 = x^3 + ax + b$

where a and b are constants.

The points on the curve obey the group axioms since the curve is a group itself.

For certain equations they will satisfy the group axioms
 - every two points can be added to give a third point (closure);
 - it does not matter in what order the two points are added (commutatitivity);
 - if you have more than two points to add, it does not matter which ones you add first either (associativity);
 - there is an identity element (the point at infinity);

We find that some curves do indeed form a group under the "point addition" operation.
Point addition combines two points on the curve to produce a third point on the curve.
The point addition operation has special rules based on the geometric properties of elliptic curves,
which ensure that the result of the addition is also a point on the curve.
Point addition is geometrically motivated, and it allows us to define scalar multiplication, which is
the basis for elliptic curve cryptography.

### [3.5] Scalar Multiplication

Scalar multiplication is an operation in which a point on an elliptic curve is added to itself a certain number of times. The result of this operation is another point on the elliptic curve.

Given an elliptic curve E defined by the equation $y^2 = x^3 + ax + b$ (a.k.a Weierstrass form), where $a$ and $b$ are constants, and a point $P(x, y)$ on the curve $E$, scalar multiplication is defined as follows:

$kP = P + P+. . . +P (k times)$

where $k$ is a scalar and the addition operation is the point addition operation defined on the elliptic curve.

In short, scalar multiplication is repetitive addition.

### [3.6] Roots of Unity

Recall, over a finite field $F_p$, where $p$ is a prime number, an elliptic curve has a finite number of points (including a special "point at infinity" denoted as $O$).

The set of points on an elliptic curve forms a group under point addition

Roots of unity are points on the curve that, when added to themselves a certain number of times
using point addition, result in the identity element $O$.

In other words, for a point $P$ on the elliptic curve, there exists a positive integer $n$ such that:

$nP = P + P+. . . +P (n times) = 1$

Here, $n$ is called the **order** of the point $P$.

The smallest positive integer $n$ for which this condition holds is the order of the point $P$.

### [3.7] Polynomial Introduction

A polynomial is an expression that can be built from constants and variables by means of addition,
multiplication and exponentiation to a non-negative integer power.

e.g. $3x^2 + 4x + 3$

Quote from Vitalik Buterin
"There are many things that are fascinating about polynomials. But here we are going to zoom in
on a particular one: polynomials are a single mathematical object that can contain an
unbounded amount of information (think of them as a list of integers and this is obvious)."
Furthermore, a **single equation between polynomials can represent an unbounded number of
equations between numbers**.

The polynomial above only has three terms. The polynomials we use in ZK proving systems will probably have a million terms or more.

#### [3.7.1] Roots of a polynomial

For a polynomial $P$ of a single variable $x$ in a field $K$ and with coefficients in that field, the root $r$ of $P$ is an element of $K$ such that $P(r) = 0$.

A very useful technique we use in ZK is that:

Using polynomial long division method, we can refactor a polynomial $P(x)$ of degree n if we know one of its root $r$:

$(x − r)(Q(x))$

where

$Q(x)$ is a polynomial of degree $n − 1$.

$Q(x)$ is simply the quotient obtained from the division process; since r is known to be a root of $P(x)$. It is known that the remainder must be zero.

Note: Degree of $n$ means the highest power used on the polynomial $P(x)$.

### [3.8] Schwartz-Zippel Lemma

Different polynomials are different at most points.

Polynomials have an advantageous property, namely, if we have two non-equal polynomials of
degree at most d, they can intersect at no more than d points.

Basically, if you evaluate some polynomial at a particular point and you evaluate a different polynomial at the same point, if those polynomials are different they are liable to evaluate to a different value. Another way of saying this is, different polynomials have very few points where they evaluate to the same value.

**Why is this useful?**

It allows us to simply check whether two polynomials are the same or not. This might sound straightforward but when we do our theory around proofs, we often want to do this and hide information. What we often want to do with our proving systems is to check whether two polynomials are equal or not, which is basically checking whether a proof exists or not. 

if $f$ and $g$ are polynomials and are equal, then

$f(x) = g(x)$ for all $x$

if $f$ and $g$ are polynomials and are NOT equal, then

$f(x) ≠ g(x)$ for all pretty much any $x$

### [3.9] What does it mean to say 2 polynomials are equal?

1. They evaluate to the same value on all points
2. They have the same coefficients

If we are working with real numbers, these 2 points above would go together, however that is not the case when we are working with finite fields.

For example all elements of a field of size $q$ satisfy the identity

$x^q = x$

The polynomials $X^q$ and $X$ take the same values at all points, but do not have the same coefficients.

### [3.10] Lagrange Interpolation

There is another way we can think of polynomials and that is through the points produced or evaluations of that polynomial. 

If you didn't have the equation of a polynomial and only had the points it evaluates to, then you can work out the eqn of the polynomial through interpolation. A particular type of interpolation used is Lagrange interpolation. 

### [3.11] Represenations of Polynomials

We effectively have 2 ways to represent polynomials:

1. Coefficient form
   
$f(x) = a_0 + a_1x + a_2x^2 + a_3x^3 . . .$

2. Point value form
   
$(x1, y1),(x2, y2), . . .$

We can switch between the two forms by evaluation or interpolation.

## [4] Zero Knowledge Proof Introduction

**What is a zero knowledge proof (ZKP)?**

A loose definition:

It is a proof that there exists or that we know something, plus a zero knowledge aspect, that is the
person verifying the proof only gains one piece of information - that the proof is valid or invalid.

**Actors in a ZKP system**

Mainly Prover and Verifier.

 - Creator - optional, maybe combined with a prover
 - Prover (trying to get their claim accepted)
 - Verifier (trying to check that the prover is not cheating in some way)

The prover proves to the verifier that it knows something without revealing the full information. The verifier verifies this by testing that the proof is correct and that the prover is not lying.

Quote from Vitalik Buterin:

"You can make a proof for the statement "I know a secret number such that if you take the word
‘cow', add the number to the end, and SHA256 hash it 100 million times, the output starts with `0x57d00485aa` ". The verifier can verify the proof far more quickly than it would take for them to run 100 million hashes themselves, and the proof would also not reveal what the secret number is."

### [4.1] Proving Systems

A statement is a proposition we want to prove. It depends on:

1. Instance variables, which are public.
2. Witness variables, which are private.

Given the instance variables, we can find a **short proof (succinct)** that we know witness variables that make
the statement true (possibly without revealing any other information).

What do we require of a proof ?

 - Completeness: there exists an honest prover P that can convince the honest verifier V of any
correct statement with very high probability.
 - Soundness: even a dishonest prover P running in super-polynomial time cannot convince an
honest verifier V of an incorrect statement. Note: P does not necessarily have to run in
polynomial time, but V does. Super-polynomial time meaning that the dishonest prover would require a huge amount of computational resources and time to prove an incorrect proof the verifier, thus making it infeasbile.

To make our proof zero knowledge we also need 'zero knowledginess'

To oversimplify: represented on a computer, a ZKP is nothing more than a sequence of numbers,
carefully computed by Peggy, together with a bunch of boolean checks that Victor can run in order
to verify the proof of correctness for the computation.

A zero-knowledge protocol is thus the mechanism used for deriving these numbers and defining
the verification checks.

### [4.2] Interactive VS Non-Interactive Proofs

In the world of blockchains, interactive proofs are not very practical, which is why we use non-interactive proofs (only 1 step - prover proves and verifier either accepts or rejects the proof).

In non-interactive zero knowledge protocols there is no repeated communication between the prover and the verifier. Instead, there is only a single "round", which can be carried out asynchronously.

Using publicly available data, Peggy (prover) generates a proof, which she publishes in a place accessible to Victor (verifier) (e.g. on a distributed ledger).

Following this, Victor can verify the proof at any point in time to complete the “round”. Note that
even though Peggy produces only a single proof, as opposed to multiple ones in the interactive
version, the verifier can still be certain that except for negligible probability, she does indeed know the secret she is claiming.

### [4.3] Succinct VS Non Succinct

Succinctness is necessary only if the medium used for storing the proofs is very expensive and/or if
we need very short verification times.

### [4.4] Proof vs Proof of Knowledge

A proof of knowledge is stronger and more useful than just proving the statement is true. For
instance, it allows me to prove that I know a secret key, rather than just that it exists.

### [4.5] Argument vs Proof

In a proof, the soundness holds against a computationally unbounded prover and in an argument,
the soundness only holds against a polynomially bounded prover. Arguments are thus often called "computationally sound proofs".

The Prover and the Verifier have to agree on what they’re proving. This means that both know the
statement that is to be proven and what the inputs to this statement represent.