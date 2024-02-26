# Overview / Maths & Cryptography Introduction

## Some simple quotes before jumping in:

`"Human dignity demands that personal information, like medical and forensic data, be hidden from
the public. But veils of secrecy designed to preserve privacy may also be abused to cover up lies
and deceit by institutions entrusted with Data, unjustly harming citizens and eroding trust in central
institutions." - Starkware`

`"ZK gives out similar vibe as ML. More and more people just mention ZK as a magic solution that
fixes everything with no context of its current limitation." - 0xMisaka`

**TLDR:** 
1. ZK can help reduce abuse in systems as well as help with privacy and human dignity due to the zero knowledge aspect. 
2. Although the ZK buzzword sounds cool, there are scenarios where it can be applied well (good use case) and where it cannot be applied well. 

## Introductory Maths 

This section contains various mathematical concepts/terminologies (not a specific branch of mathematics) that are relevant to understanding ZK.

### Numbers

When using ZK technology, we restrict ourselves in the types of numbers we use. Usually, we stick with integers. There are other sets than those mentioned below: 

The set of Integers is denoted by Z e.g. {⋯,−4,−3,−2,−1,0,1,2,3,4,⋯}

The set of Rational Numbers is denoted by Q e.g. {. . . 1, 3/2, 2, 22/7, . . . }

The set of Real Numbers is denoted by R e.g. {2, −4, 613, π, √2,…}

Fields are denoted by $F$. 

The set of numbers we are particularly interested in is represented by $Z^*_p$ (read as Z subscript p with an asterisk). This is a finite field of integers (which means there is a maximum value). The maximum value is 1 less than p (a prime number). When we do arithmetic for that field, we do it mod (modulus) that prime number. The * represents special properties of the field. In short, it is a representation of a finite field of integers mod prime p with multiplicative inverses.

**Why are we interested in this particular field?**

It makes our lives easier. We use finite fields for cryptography, because elements have “short”, exact representations and useful properties.

### Modular Arithmetic

Modular Arithmetic is sometimes referred to as "clock math" because of how numbers wrap around. 

When we write n mod k we mean simply the remainder when n is divided by k. Thus,

25 mod 3 = 1

15 mod 4 = 3

The remainder should be positive.

### Group Theory

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

**Sub groups**

If a subset of the elements in a group also satisfies the group properties, then that is a subgroup of the original group.

**Cyclic groups and generators**

A finite group can be cyclic. That means it has a generator element. If you start at any point and apply the group operation with the generator as argument a certain number of times, you go
around the whole group and end in the same place.

**Finding an inverse**

From Fermat's little theorem (way to find inverse element in a group where the operation is multiplication a.k.a multiplicative inverse).

Finding multiplicative inverses for finite fields that use modular arithmetic is not as easy as one thinks. But it can be made easier, if we use the following formula:

Let's say a is the element and $a^{-1}$ is the inverse of element a.

$a^{−1} ≡ a^{p−2}(modp)$

Let p = 7 and a = 2. We can compute the inverse of a as:

$a^{p−2} = 2^5$ = 32 ≡ 4 

The final answer is 4 since we apply modulo 7 on 32 i.e. 32 mod p = 32 mod 7 = 4 as remainder. Thus, for element a = 2, the $a^{-1}$ = 4.

This is easy to verify: $a * a^{-1}$ = 2 x 4 ≡ 8 (mod 7) = 1 (which is the identity element).

**Equivalance classes**

Modular arithmetic and inverses splits up our number space into what are called equivalence classes.

In the above examples where we used p = 7, anytime we got a number that falls out of the finite field (which has max = p - 1 = 6), we used to apply mod p on it. **Note: Numbers even within the field range [0,6] have the mod p applied, except that the result is the number itself. Due to that, it's not necessary to explicitly mod p them.**

Since 6 mod 7 = 6, 13 mod 7 = 6, 20 mod 7 = 6 ..., we can say that 6, 13, 20 ... form an equivalence class

In short, numbers giving the same remainder on mod p form an equivalence class.

Thus if we are trying to solve the equation

x mod 7 = 6

x could be 6, 13, 20 ...

This gives us the basis for a one way function (many-to-one function).

### Fields

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

**What is the difference between groups and fields?**

Fields are similar to groups just that we have an extra operation. Fields can be thought of an extension of what we do with groups. 

In ZK technology/proving systems, we tend to work with finite fields.

**Finite fields and generators**

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

**Group Homomorphisms**

Another terminology that we'll come across is the idea of homomorphisms.

A homomorphism is a map between two algebraic structures of the same type, that preserves the
operations of the structures.

This means a map f : A → B between two groups $A$, $B$ equipped with the same structure such that,
if ⋅ is an operation of the structure (here a binary operation), then
f(x ⋅ y) = f(x) ⋅ f(y)


## Cryptography Background

