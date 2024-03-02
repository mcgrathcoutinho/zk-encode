# ZKP Theory / Zokrates

Topics:
 - Cryptography : FHE
 - Complexity Theory
 - ZKP Theory - zkSNARKS
 - Zokrates
 - zkSNARK process in more details

## FHE

### Background

Fully Homomorphic Encryption , the ‘holy grail’ of cryptography, is a form of encryption that allows
arbitrary computations on encrypted data. This field is not specific to the ZK area but is a helpful tool to ZK.

We encrypt some data => send it off to a third-party to do some operation/computation (maybe they have more resources) => third-party sends it back to us => we decrypt the data

Here the thid-party does not learn anything about the encrypted data. 

Homomorphic encryption can be viewed as an extension of either symmetrickey or public-key cryptography.

### Bitcoin split-key vanity mining

A vanity address is an address generated from parameters such that the resultant hash contains a human-readable string (e.g., 1BoatSLRHtKNngkdXEeobR76b53LETtpyT). This allows people to create addresses with some numbers or letters they might want. 

Given that ECDSA key pairs have homomorphic properties for addition and multiplication, one can
outsource the generation of a vanity address without having the generator know the full private key
for this address.

For example:

1. Alice generates a private key (a) and public key (A) pair, and publicly posts A.
2. Bob generates a key pair (b, B) such that hash(A + B) results in a desired vanity address. He sells b and B to Alice.
3. A, B, and b are publicly known, so one can verify that the address = hash(A + B) as desired.
4. Alice computes the combined private key (a + b) and uses it as the private key for the public key (A
+ B).
5. Similarly, multiplication could be used instead of addition.

Although private key **b** is publicly known, the generator does not know the full private key for **(A + B)** due to private key **a** still being only known to alice. 

## Complexity Theory

Complexity theory is to classify how difficult problems are to solve and verify. Computer scientists and mathematicians haev tried to group problems that have similar properties into classes. Usually they are classified according to the time required to find/verify a solution or maybe even the amount of memory involved in finding/verifying the solution. 

If the time taken in the worst case grows as a polynomial of n, that is roughly proportional to $n^k$ for some value $k$, we put these problems in class P for polynomial. These problems are seen as
tractable.

Decision Problem: A problem with a yes or no answer

### Complexity Classes

#### P

P is a complexity class that represents the set of all decision problems that can be solved in
polynomial time. That is, given an instance of the problem, the answer yes or no can be decided in
polynomial time.

The polynomial refers to the size of the input.

#### NP

NP is a complexity class that represents the set of all decision problems for which the instances
where the answer is “yes” have proofs that can be verified in polynomial time, even though the
solution may be hard to find.

#### NP-Complete

NP-Complete is a complexity class which represents the set of all problems X in NP for which it is
possible to reduce any other NP problem Y to X in polynomial time.

Intuitively this means that we can solve Y quickly if we know how to solve X quickly.

#### NP-hard

Intuitively, these are the problems that are at least as hard as the NP-complete problems. Note that
NP-hard problems do not have to be in NP, and they do not have to be decision problems.

The precise definition here is that a problem X is NP-hard, if there is an NP-complete problem Y,
such that Y is reducible to X in polynomial time

#### IP

A class that lies at the heart of zkps is the Interactive Proof class.

In complexity theory they are related to the other complexity classes

### Big O Notation

In plain words, Big O notation describes the complexity of your code using algebraic terms.
It describes the time or space required to solve a problem in the worse case in terms of the size of
the input.

We use this notation when comparing ZKP systems

## ZKP Theory - zkSNARKs

Currently zkSNARKS are the most common proof system being used, for example they form the
basis for the privacy provided in ZCash.

The process of creating and using a zk-SNARK can be summarised as

A zk-SNARK consists of three algorithms $C, P, V$ defined as follows:

The Creator takes a secret parameter lambda (secret randomness) and a program $C$, and generates two publicly available keys (pieces of data we create in a setup):
 - a proving key $pk$
 - a verification key $vk$

These keys are **public parameters** that only need to be generated once for a given program C.
They are also known as the Common Reference String.

### Process of creating/verifying a proof

The prover Peggy takes a proving key $pk$, a public input $x$ and a private witness $w$.

Peggy generates a proof $pr = P(pk, x, w)$ that claims that Peggy knows a witness $w$ and that the
witness satisfies the program $C$.

The verifier Victor computes $V (vk, x, pr)$ which returns true if the proof is correct, and false
otherwise.

Thus this function returns true if Peggy knows a witness $w$ satisfying:

$C(x, w) = true$

### Trusted Setups and Toxic Waste

Note the secret parameter lambda in the setup, this parameter sometimes makes it tricky to use zkSNARK in real-world applications. The reason for this is that anyone who knows this parameter can
generate fake proofs.

Specifically, given any program $C$ and public input $x$ a person who knows lambda can generate a
proof $pr2$ such that $V (vk, x, pr2)$ evaluates to true without knowledge of the secret $w$.

Usually, a multi-party computation (MPC) ceremony is used for the setup.