# Use Cases of ZKPs / L2

## Types of ZKPs

SNARKS / STARKS are general purpose systems for creating proofs.

We don't always need SNARKS or STARKS other techniques may be more efficient for our use
case.

### Other useful techniques

 - Blind signatures
 - Accumulators
 - Pedersen commitments
 - Sigma protocols

### Advantages of SNARKs

 - Small proof size
 - Fast verification
 - Generic approach

### Disadvantages of SNARKs

 - Require a trusted setup
 - Very long proving keys
 - Proof generation is impractical on constrained devices
 - Strong security assumptions haven't been well tested.
 - Theoretical background is difficult to understand

### Advantages of Sigma Protocols

 - Very economical for small circuits
 - Do not require a trusted setup
 - Security assumptions are weak and are well understood
 - Maths is fairly easy to understand

### Disadvantages of Sigma Protocols

 - Sigma protocols do not scale well, proof size, proof generation and verification size are linear in the complexity of the statement
 - Cannot easily handle generic computation, they are better suited to algebraic constructions.

## ZKP Use Cases

1. Privacy preserving cryptocurrencies - Zcash, MimbleWimble, Monero
2. Nuclear Treaty Verification
3. Prviacy preserving financial systems

## Scalability Introduction

### The scalability trilemma

How can we not talk about the trilemma, which is the main reason as to why ZKPs/rollups are used.

Most Layer 1 blockchains focus on decentralization and security because:

"The decentralization of a system is determined by the ability of the weakest node in the network to
verify the rules of the system." - Georgios Konstantopoulos

"For a blockchain to be decentralized, it's crucially important for regular users to be able to
run a node, and to have a culture where running nodes is a common activity."

Scalability is left out due to this. That's why we have ZKP solutions.

### Off-chain Scaling

Generally speaking, transactions are submitted to these layer 2 nodes instead of being submitted
directly to layer 1 (Mainnet). For some solutions the layer 2 instance then batches them into groups
before anchoring them to layer 1, after which they are secured by layer 1 and cannot be altered.
A specific layer 2 instance may be open and shared by many applications, or may be deployed by
one project and dedicated to supporting only their application.

### Rollups

Rollups are solutions that have:

 - transaction execution outside layer 1
 - data or proof of transactions is on layer 1
 - a rollup smart contract in layer 1 that can enforce correct transaction execution on layer 2 by using the transaction data on layer 1

The main chain holds funds and commitments to the side chains. The side chain holds state and performs execution. There needs to be some proof, either a fraud proof (optimistic) or a validity proof (zk).

Rollups require "operators" to stake a bond in the rollup contract. This incentivises operators to
verify and execute transactions correctly.

There are currently 2 types of rollups:
 - Zero Knowledge Proof rollups (a.k.a validity rollups)
 - Optimistic rollups

### ZKP or validity Rollups

These rollups rely on a proof of the correctness of the execution that produces the rollup block
state transition being supplied to a validator contract on L1.

The state transition on L2 will not be regarded as valid unless this proof has been validated. Although we use a zero knowledge proof, the zero knowledge aspect is usually ignored, the inputs
and data involved is usually public, the focus is on the correctness of computation. For this reason
some people prefer the term validity proof.

### Optimistic Rollups

The name Optimistic Rollups originates from how the solution works. 'Optimistic' is used because
aggregators publish only the bare minimum information needed with no proofs, assuming the aggregators run without commiting frauds, and only providing proofs in case of fraud. 'Rollups' is
used because transactions are commited to main chain in bundles (that is, they are rolled-up).

## Data Availability

In order to re create the state, transaction data is needed, the data availability question is where
this data is stored and how to make sure it is available to the participants in the system.

![](https://i.imgur.com/XZdQm1L.png)

StarkNet is currently in ZK-Rollup mode (see above). This means that upon the acceptance of a
state update on-chain, the state diff between the previous and new state is sent as calldata to
Ethereum.

This data allows anyone that observes Ethereum to reconstruct the current state of StarkNet. Note
that to update the StarkNet state on L1, it suffices to send a valid proof — without information on
the transactions or particular changes that this update caused. Consequently, more information
must be provided in order to allow other parties to locally track StarkNet’s state.

## Other projects

1. Filecoin (largest deployed zkSNARK network)
2. Tornado Cash
3. Dark Forest game
4. ZK Microphone