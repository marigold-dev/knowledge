---
description: "Eduardo + GA\_stance on Deku"
---

# Deku for the noobs

### Where does the name "Deku" come from?

Not from [Zelda](https://zelda.fandom.com/wiki/The\_Great\_Deku\_Tree)! Deku is the main character in [My Hero Academia](https://en.wikipedia.org/wiki/My\_Hero\_Academia). He's a great character that starts his story with no power at all before wielding tremendous powers.&#x20;

### Why would a private company need a blockchain?

Many actors are interested in running their business through blockchains as they are safe and resilient to failures.

Indeed, blockchains naturally mitigate insider attacks (malevolent system administrator, rogue employee, compromised employee account) since a single person can't commit a transaction. Moreover, decentralization makes the system resistant to both technical failures (hardware issues, software upgrade issues, etc) and human-related errors (human errors or violence-related issues). Additionally, decentralization protects an actor from unforeseen threats such as having a tsunami in Japan, a flood in Australia, a hurricane in Florida, a power outage in Poland and the big one hitting California at the same time.

However, **typical blockchains lack the ability to tailor to specific needs** such as:

* making a buffer available to companies with high NFT throughput without commiting every single operation on a major blockchain,
* creating deterministic operating systems,
* enhancing an organization's bus factor through slight decentralization,
* freeing an organization from systemic risks via a blockchain's collateral advantages.

Unfortunately, creating a brand new blockchain from scratch yields a **massive design, implementation and infrastructure overhead** that most actors aren't willing to deal with.

All those specific needs can be addressed without a huge overhead by a **single type of layer 2: a sidechain, to which data and/or computations are offloaded**.

### What is a sidechain?

Basically, a sidechain is a **secondary blockchain that is paired to a parent blockchain** and is able to communicate with it. A sidechain works like any blockchain and has the same core properties, with the added feature that its consensus is witnessed by the mainchain.

To use a real-life analogy, think of a rehearsal studio who lends instruments to musicians as a parent blockchain. The band member who books a rehearsal slot and the required instruments is the sole responsible for all the instruments for the whole band. This band member makes sure nothing bad happens when the instruments change hands, takes care of them and is the one responsible for eventually returning them intact to the studio. In this situation, the studio doesn't have the necessary means to oversee every details and defers the responsability to this band member. This person can be thought of as a the studio's sidechain.

In practice, witnessing is about providing a basic proof such as having the signatures of 2/3rd of the validators.

### How sidechains are related to Deku?

Right now, the Deku team focuses on **building a Tezos sidechain** and the team's long term goal is to create a framework for creating sidechains, all tailored to specific needs. In the long run, Deku would offer "sidechain formulas" depending on the main features the layer 2 needs to have to suit the specific need.

(Deku could create "pure" blockchains by creating sidechains who witness no blockchains.)

Bear in mind that Deku would not allow you to choose every single parameter that exist while creating a blockchain. Mainly because blockchain is a very recent field and that those parameters are not all discovered and specified in nice equations. Since that, as of now, blockchains parameters are all inter-dependant, Deku aims to offer "formulas" depending on the main features you want your sidechain to offer.

### What are the main challenges on the project?

Right now, the Deku team focuses on **building a Tezos sidechain** and the team's long term goal is to create a framework for creating sidechains, all tailored to specific needs.

The main challenges are to understand, study and implement various possibilities of **known blockchain building blocks** such as **networking** (typical problem: efficient communication between all nodes), **consensus** (defining a single consensus that works both in a private PoA setting and a public PoS setting), **state transition** (how to extract parallelism from a blockchain state machine), **cryptoeconomics** (finding the proper minimal values required to make the whole system run smoothly) while maintaining **redundancy and a framework vibe** in the architecture and code.

From a human perspective, a huge challenge is to work with people from different backgrounds, living in different timezones with different sleep patterns. The biggest one might be that more hands are needed in the Deku team which means spending a considerable amount of time on finding suitable candidates, hiring the right people and training newcomers.

###
