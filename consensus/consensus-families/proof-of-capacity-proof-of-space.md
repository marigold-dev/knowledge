# Proof of Capacity/Proof of Space

## Basic definition

Proof-of-space/Proof-of-capacity are similar to proof-of-work algorithms, with storage replacing computation: to show you have a legitimate interest in the service you need to allocate a non-trivial amount of memory or disk space to solve the challenge.

Proof-of-space = piece of data sent by the prover to the verifier to show the prover has allocated a certain amount opf space.

The verification needs to efficient (small amount of space and time) for practicality. For soudness it should be hard for the prover to pass verification is the claimend amount of space is not reserved => hard-to-pebble graphs.

## Protocol

1. verifier asks the prover to build a labeling of hard-to-pebble graph
2. prover commits to the labeling
3. verifier asks the prover to open several (chosen at random) locations in the commitment

## Used by

* Burstcoin (miners allowed to pre-calcultate/plot PoW functions)
* Chia (proof-of-space and proof-of-time, does not store useful data, intense write activity => concern over shortened lifespans of drives)
* Spacemint (non-interactive proptocel since each individual oin the network has to behave as verifier)

## Features&#x20;

* similar to PoW but space replaces computation (more environmental friendly)
* related to malware detection, anti-spam measure, denial service attack prevention

## Disavantages

* incentivization can be issue
