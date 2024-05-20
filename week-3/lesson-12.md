# zkSNARK theory / PLONK

Topics:
 - Polynomial Introduction
 - Polynomial Commitment Schemes
 - Proving Systems in general
 - zkSNARK process
 - Plonkish protocols

## Polynomial Introduction

[Same as from 3.7 to 3.11 from Lesson 1](https://github.com/mcgrathcoutinho/zk-encode/blob/main/week-1/lesson-1.md#37-polynomial-introduction)

## Polynomial Commitment Schemes

### Introduction

A polynomial commiment is a short object that "represents" a polynomial, and allows you to verify evaluations of that polynomial, without needing to actually contain all of the data in the polynomial.

That is, if someone gives you a commitment $c$ representing $P(x)$, they can give you a proof that can convince you, for some specific $z$, what the value of $P(z)$ is. There is a further mathematical result that says that, over a sufficiently big field, if certain kinds of equations (chosen before $z$ is known) about polynomials evaluated at a random $z$ are true, those same equations are true about the whole polynomial as well.

For example, if $P(z). Q(z) + R(z) = S(z) + 5$ for a particular $z$, then we know that it's overwhelmingly likely that $P(x). Q(x) + R(x) = S(x) + 5$ in general. Using such polynomial commitments, we could very easily check all of the above polynomial equations above - make the commitments, use them as input to generate $z$, prove what the evaluations are of each polynomial at $z$, and then run the equations with these evaluations instead of the original polynomials.

A general approach is to have the evaluations in a merkle tree, the leaves of which the verifier can select at random, along with merkle proof of their membership.

### Role in ZKPs

Commitment schemes generally allow the properties of:

1. Binding. Given a commitment $c$, it is hard to compute a different pair of message and randomness whose commitment is $c$. This property guarantees that there is no ambiguity in the commitment scheme, and thus after $c$ is published it is hard to open it to a different value.
2. Hiding. It is hard to compute any information about $m$ given $c$.

Given the size of the polynomials used in ZKPs, with say $10^8$ terms, they help with succinctness by reducing the size of the information that needs to be passed between the prover and verifier.

#### Comparison of Schemes and their underlying assumptions

[ZKP Study Group](https://www.youtube.com/watch?v=bz16BURH_u8)

### Idealized Proving System

There is much missed out, and assumed here, this is just to show a general process.

#### Use of randomness

The prover uses randomness to achieve zero knowledge, the verifier uses randomness when generating queries to the prover, to detect cheating by the prover.

Steps:
1. Prover claims Statement $S$
2. Verifier provides some constraints about the polynomials
3. Prover provides (or commits to) $P_i...P_k$ : polynomials
4. Verifier provides $z ∈ 0, ... p − 1$
5. Prover provides evaluations of polynomials: $P_1(z). . . P_k(z)$
6. Verifier decides whether to accept $S$

The degree expected are typically about $10^6$ (still considered low degree)

Note the probability of accepting a false proof is < 10.d/p , where p is the size of the field, so of the order of $2^(−230)$ if our finite field has p of ~ $2^(256)$.