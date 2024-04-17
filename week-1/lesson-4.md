# Introduction to Starknet / Cairo

## Starknet Architecture Overview

Starknet is not an EVM-compatible chain. It does not run the EVM but the CairoVM. When you send your transactions to be executed, they're executed on the Cairo code on the CairoVM. 

The result of that execution is an execution trace. This trace forms the basis for a zero knowledge proof. This is sent to the prover that creates a validity proof (STARK) that is sent to the L1. Note that the proofs are batched into a single proof and then sent to the prover. 

### Actors Involved

Prover - Receives trace from Sequencer and creates STARK proofs to be verified. The prover submits the proof to the verifier that registers it on the L1.

Starknet OS - If you write a program in Cairo, it is executed by the OS. This OS also provides context about the Starknet blockchain (i.e. storage, events, etc).

Starknet State - The state is composed of contract's code and storage. 

Starknet L1 Contract - Defines the state of the system by storing the
commitment to the L2 state. The committed state on the L1 core contract acts as provides as the consensus mechanism of StarkNet, i.e., the system is secured by the L1 Ethereum consensus. In addition to maintaining the state, the StarkNet L1 Core Contract is the main hub of operations for StarkNet on L1. Specifically:
 - It stores the list of allowed verifiers (contracts) that can verify state update transactions
 - It facilitates L1 ↔ L2 interaction

Starknet Full nodes - Maintain the L2. If the connection between the Sequencer and the Full Node fails for some reason, you can recreate the L2 current state by indexing date from the Starknet L1 Core Contract independently.

## Safe Intermediate Representation (Sierra)

A new intermediate level representation. Transactions should always be provable, even when a transaction fails. Asserts are converted to if statements, if it returns false we don't do any modifications to storage.

Contracts will count gas. There is a limit to the amount you are allowed to spend when you're sending in a transaction. Currently, gas is paid to the Sequencer and it is the sequencer that determines the price for the transaction. 

Sierra bytecode:
 - cannot fail
 - counts gas
 - compiles to Cairo with virtually no overhead

Process:
Cairo Smart Contract => Sierra => Cairo Assembly (CASM) => Validity Proof

## Introduction to Rust

### Core Features
 - Memory safety without garbage collection
 - Concurrency without data races
 - Abstraction without overhead

### Variables

Variable bindings are immutable by default. But this can be overriden using the mut modifier. 

```
let x = 1;
let mut y = 1;
```

### Types

[See Rust book](https://doc.rust-lang.org/book/ch03-02-data-types.html)

## Some articles about version 2.0
Extropy [Starknet v0.12 Quantum Leap](https://extropy-io.medium.com/starknet-v0-12-quantum-leap-33f5103d68ce)
Starkware - [Quantum Leap](https://starkware.co/resource/starknet-quantum-leap-major-throughput-improvements-are-here/)
Starknet Forum - [Syntax Proposal](https://community.starknet.io/t/cairo-1-contract-syntax-is-evolving/94794)

## Starknet Resources
[Starknet Documentation](https://docs.starknet.io/documentation/)
[Starknet Book](https://book.starknet.io/)

## Cairo Resources
[Cairo Book](https://book.cairo-lang.org/)
[Cairo by example](https://cairo-by-example.com/)
[Starknet by example](https://starknet-by-example.voyager.online/)

## Starknet Foundry Book

[Link](https://foundry-rs.github.io/starknet-foundry/)

The notes are short since most of it can be referenced through the Cairo book and other resources linked.