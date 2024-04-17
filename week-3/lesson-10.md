# zkEVM Solutions

Compared to Starknet, zkEVM solutions i.e. the L2 chains are trying to maintain max EVM compatibility. 

## Rollup Recap

Rollups are solutions that have:
 - transaction execution outside layer 1
 - transaction data and proof of transactions is on layer 1
 - a rollup smart contract in layer 1 that can enforce correct transaction execution on layer 2 by
using the transaction data on layer 1

The main chain holds funds and commitments to the side chains.
The side chain holds additional state and performs execution.
There needs to be some proof, either a fraud proof (Optimistic) or a validity proof (zk).

Rollups require “operators” to stake a bond in the rollup contract. This incentivises operators to
verify and execute transactions correctly.

## zkVM Introduction

### Background - Virtual Machines

Virtual Machines (VMs) are designed to provide the functionality a computer, usually wholly in software (there is a subtle difference between virtualisation and emulation). The Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software.

There are 3 main types , register based, stack based and accumulator based, most VMs are of the
first 2 types. The Ethereum Virtual Machine is stack based.

In this course we will look at zkEVMs such as Polygon zkEVM / zkSync Era, and also zkVMs such
as Risc zero. Essentially, zkEVM is a subset of zkVM. 

A zkVM is a zero-knowledge proof-based virtual machine that combines a zk proof and a Virtual
Machine. The zkVM typically consists of two important components: a compiler that can compile
high-level languages such as C++ and Rust into intermediate (IR) expressions for the ZK system to
perform; the other is the ISA (Instruction Architecture) instruction set framework, which mainly
executes instructions about CPU operations and is a series of instructions used to instruct the CPU
to perform operations.

### zkEVM phases

#### Proof focused

 - Circuit creation
 - Setup
    - Parameters created - gives proving key and verification key
 - Proof creation
 - Proof aggregation
 - Proof acceptance on L1 and verification

#### L2 aspects

As we have seen for validity rollups, we also have processes to:

 - Submit data to the DA layer
 - Allow L1 <-> L2 messaging
 - Provide an escape hatch via forced transactions

## zkEVM workflow

The general workflow for an zkEVM would be:

 - Receive a transaction
 - Execute the relevant bytecode
 - Make state changes and transaction receipts
 - Using the zkEVM circuits with the execution trace as input produce a proof of correct execution
 - Aggregate proofs for a bundle of transactions and submit them to L1
 - Submit data to the appropriate data availability layer.

## Types of zkEVM

![](image.png)

## zkSync 

[Link](https://docs.zksync.io/build)

## Polygon

[Polygon ZK Rollups](https://www.alchemy.com/overviews/polygon-zk-rollups)

[Strategy](https://polygon.technology/blog/polygons-zero-knowledge-strategy-explained)

Summary:
 - Polygon Edge - Infrastructure
 - Polygon PoS - Original side chain
 - Polygon zkEVM - zkEVM based rollup
 - Polygon CDK - App chain development
 - Polygon Miden - zkVM using STARKs

[Vision & Proposed Architecture](https://polygon.technology/blog/polygon-2-0-protocol-vision-and-architecture)

### Polygon Nightfall

From a collaboration with EY it is designed to allow private transactions. It is a combination Optimistic rollups and zero knowledge, optimistic rollups for scalability and zk for privacy.

There is a beta version available on mainnet.

## Scroll

[Link](https://scroll.io/blog/zkevm)

[Scroll Architecture](https://scroll.mirror.xyz/nDAbJbSIJdQIWqp9kn8J0MVS4s6pYBwHmK7keidQs-k)

