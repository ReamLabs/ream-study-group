# ream-study-group

A collection of learning materials on the Beam chain and Ream client.

## Beacon Chain

### Beacon chain specs
- [Ethereum Proof-of-Stake Consensus Specifications](https://ethereum.github.io/consensus-specs/) (2018 - current)
    - This is the official consensus specs. It consists of the base Phase0 specs followed by incremental changes per each upgrade.
        - **Phase0**
            - **The beacon chain**
                - Defines the necessary **data types, parameters, operations** (e.g. depositing, proposing, attesting and voluntary exiting), **state accessors** (e.g. get_current_epoch, get_block_root, get_beacon_committee) and **other helpers** (e.g. math, crypto, predicates)
                - Defines the **state transition function** (how to proceed from one block to another), **epoch processing** (e.g. epoch justification/finalization, randao mixes), and **block processing** (e.g. attestation, deposits, voluntary exits, proposer slashing, attester slashing)
            - **Deposit contract** - Defines the constants, config values, smart contract functions and event logs and reference to the actual implementation of the deposit contract.
            - **Beacon chain fork choice** - Defines how the chain selects a contentious block e.g. due to late arrival of the block, late attestations, etc.
            - **Honest validator guide** - Defines the responsibility of a validator, e.g. use of BLS public key, withdrawal credentials, committee assignments, how to propose a block, how to attest, how to aggregate attestations,
            - **P2P networking** - Defines how validators discover and communicate with each other.
                - TCP libp2p transport for both dialing and listening
                - libp2p-noise for secure channel handshake with secp256k1 for encryption
                - multistream-select 1.0
                - mplex/6.7.0 for multiplexing
                - discv5 for discovery
                - SSZ for serialization
                - Snappy for compression
                - Gossipsub v1 and v1.1 extension
            - **Weak subjectivity** - Defines how one creates and uses a weak subjectivity checkpoint for a faster chain sync
        - **Altair**
            - **Beacon chain changes** - Introduce sync committees. Increases penalty values for inactivity and slashing. Incentive accounting reforms to reduce spec complexity.
            - **Light client sync protocol** - Defines the new features required to support light clients. E.g, new configurations, new gossipsub topics and messages, new Req/Resp endpoints.
            - **Honest validator guide changes** - Defines changes to the validator behaviors to support sync committees. E.g. checking if a validator is assigned to the sync committees, aggregating sync committee signatures, incorporating sync committee signatures into block proposals, signing and broadcasting beacon block roots.
            - **P2P networking** - Defines the changes to the P2P layer to support sync committees e.g. changes to gossipsub existing topics and messages, changes to the existing Req/Resp endpoints, and adding a new bitfield to the discv5 ENR to facilitate sync committees subnet discovery.
        - **Bellatrix (The Merge)** - Prior to Bellatrix, the beacon chain runs in parallel to the Proof-of-Work chain and does not have transaction execution. The Bellatrix upgrade brought in transaction execution and completely phased out Proof-of-Work.
            - **Beacon Chain changes**
                - Increased penalty parameters (inactivity & slashing) to their final values.
                - Defines the configurations for the transition e.g. TERMINAL_TOTAL_DIFFICULTY
            - **Fork choice changes** - [WIP]
            - **Honest validator guide changes** - [WIP]
            - **P2P networking** - [WIP]
        - **Capella** - [WIP]
        - **Deneb** - [WIP]
- [Ethereum Proof-of-Stake Consensus Spec Tests](https://github.com/ethereum/consensus-spec-tests) (2019 - current) - The test vectors for the consensus specs.

### Beacon chain _annotated_ specs

- [Weak Subjectivity in Eth2.0](https://notes.ethereum.org/@adiasg/weak-subjectvity-eth2) - Aditya Asgaonkar (Sep 2020)
- [Phase 0 for Humans \[v0.10.0\]](https://notes.ethereum.org/@djrtwo/Bkn3zpwxB) - Danny Ryan (Jul 2021)
- [Upgrading Ethereum: A technical handbook on Ethereum's move to proof of stake and beyond](https://eth2book.info/capella/) - Ben Edgington (2023)
- [Engine API: A Visual Guide](https://hackmd.io/@danielrachi/engine_api) - Daniel Ramirez (Feb 2024)

### Beacon chain design rationales

- [Vitalik's annotated eth2 spec with a focus on design rationale](https://github.com/ethereum/annotated-spec) - Vitalik (2020 - current)
- [Serenity Design Rationale](https://notes.ethereum.org/@vbuterin/serenity_design_rationale) - Vitalik (Jan 2022)

### Beacon chain pitfalls, lessons learnt & improvement ideas

- [**Reducing Beacon Chain Bandwidth for Institutional and Home Stakers**](https://www.youtube.com/watch?v=u8JJh-E-VMg) ([slides](https://archive.devcon.org/resources/6/reducing-beacon-chain-bandwidth-for-institutional-and-home-stakers.pdf)) - Adrian Manning, Diva (SigmaPrime/Lighthouse) at Devcon Bogota (Oct 2022)
- [**Beacon chain design mistakes**](https://www.youtube.com/watch?v=10Ym34y3Eoo) ([slides](https://docs.google.com/presentation/d/1LkxHrXjQyRh2i75R13yjndc_aUp9oXTAdAw538XfJhk/edit?usp=sharing)) - Justin Drake at EthStaker's Staking Gathering (Nov 2023)
- [**Ethereum Node Message Propagation Bandwidth Consumption**](https://ethresear.ch/t/ethereum-node-message-propagation-bandwidth-consumption/19952) - yiannisbot (Jul 2024)
- [**Where’s the home staking bandwidth research?**](https://ethresear.ch/t/wheres-the-home-staking-bandwidth-research/20507) - ryanberckmans (Sep 2024)
- [**Staking Incidents**](https://ethstaker.cc/incidents) - EthStakers (2023 - 2024)

## Beacon chain client-specific analyses

- [**Compare ROI of 3 eth2 Clients**](https://trademotif-46434.medium.com/compare-roi-of-3-eth2-clients-d5862b372c0d) - motif (Oct 2020)
- [**Move from teku to prysm**](https://www.reddit.com/r/ethstaker/comments/ph3h7z/move_from_teku_to_prysm/) - r/ethstaker (Sep 2021)
- [**Which clients are having issues post-merge? Recommendations?**](https://www.reddit.com/r/ethstaker/comments/xmrriw/which_clients_are_having_issues_postmerge/) - r/ethstaker (Sep 2022)
- [**Considering Client Diversity through the lens of Network Performance**](https://ethresear.ch/t/considering-client-diversity-through-the-lens-of-network-performance/18885) - U. Natale and G. Sofia (Mar 2024)

## Beam chain proposals

- [**Keynote: [title redacted]**](https://www.youtube.com/watch?v=Gjuenkv1zrw) - Justin Drake at Devcon SEA (Nov 2024)
- [**Ethereum Roadmap & Beamchain**](https://www.youtube.com/watch?v=8mJDt8TGebc) - Justin Drake at Bankless Summit (Nov 2024)
- [**Deep Dive into Ethereum's Beam Chain**](https://www.youtube.com/watch?v=88FDeg5JaUk) - Justin Drake with The Defiant (Nov 2024)
    - Proposing to rewrite the consensus layer instead of applying incremental upgrades
    - **Rationales**
        - Small incremental upgrades are only applicable to certain types of changes and not the others
        - Governance batching optimization: research, spec writing, EIP proposal, prioritization, testing → Batch everything to a single fork so we only go through the process once (the process will be longer per the one fork but more concentrated effort)
        - Avoid existing technical debts
    - **Comparison to The Merge**
        - *Similarity:* It’s a big change lumped together and requires a large fork
        - Difference: The Merge introduced a new set of consensus participants (from PoW miners to PoS stakers) so the two chains need to be merged. The beam chain will not change the set of consensus participants. We’ll just choose a slot number and do the change of rules at that slot number.
    - 9 items in Vitalik’s roadmap, 4-5 can be done incrementally, the rest are big ticket items that are hard to do incrementally and more suited to be done from scratch. Proposing 2 parallel R&D tracks:
        - **Beacon chain tracks** - Implement incremental changes to the Beacon Chain
            - **Block production:**
                - (1) censorship resistance (FOCIL)
                - (2) isolated validators
            - **Staking:**
                - (3) Smarter issuance
                - (4) Smaller validators
            - **Cryptography:**
                - (5) Strong randomness
        - **Beam chain tracks** - Develop the Beam Chain for the next 3-4 years and transition to it in a single hard fork
            - **Block production:** (1) Faster slots (4 seconds)
            - **Staking:** (2) Faster finality
            - **Cryptography:**
                - (3) Chain snarkification
                    - Generate a real-time, Snark proof for each and every block
                    - Required changes: hash function, signature scheme, serialization, merklelization
                - (4) Quantum security
                    - Replacing BLS signature
            - What it could enable
                - **Native Rollups** - Once the EVM is snarkified, we can expose a precompile that allows anyone to deploy an exact and as many copy of the EVM as an L2/rollup as possible, allowing horizontal scaling with customizations e.g. roll their own fee token, their own governance mechanism, their own sequencer, etc.
                    - Arbitrum and Optimism tries to be EVM-equivalent but it’s hard (keeping track of L1 changes can cause bugs, non-equivalent properties, keeping track of the L1 EVM changes). With precompiles of the L1 they can fully inherit the security of L1 and remove the governance required for upgrades.
        - To complete the roadmap in 4-5 years so **Ethereum can go into maintenance mode and start thinking about ossification like Bitcoin.**
- [**Ethereum’s Three Front War**](https://youtu.be/jUFVOUq0-fc?si=4ayhCrWKLNiv2q10&t=2936) - Bankless Podcast with Justin Drake (Dec 2024)
    - [50:17](https://youtu.be/jUFVOUq0-fc?si=skZHo978yWa1nDjP&t=3017) “The beam chain upgrade is trying to take the slowest parts of the roadmap and accelerate them so that we can complete the full Ethereum roadmap in a timely fashion.”
    - [50:55](https://youtu.be/jUFVOUq0-fc?si=PyyG8TC30Q9CjYsy&t=3055) “You can think of it as an invitation to think strategically about the Ethereum roadmap, widen the discourse and overturn window. To discuss the opportunity and necessity to do an ambitious upgrade, embrace ZK technology, reject technical debt, and optimize approach to Ethereum governance.”
    - [53:32](https://youtu.be/jUFVOUq0-fc?si=IB9w9cuGRb9wGUaA&t=3212) “One of my fears is that Ethereum ossifies prematurely not because there is a lack of good research ideas or a lack of collective desire to innovate, but because of a lack of ability to coordinate fast enough to match the ambition of the roadmap as well as the rapid growth of the ecosystem.”
    - [56:32](https://youtu.be/jUFVOUq0-fc?si=vhTB4geOZ2W0rauP&t=3392) “To a very large extent, what the consensus layer upgrades are all about is maximizing the viability of being a solo validator. 3 memes, altogether to be the renaissance of solo validating.
        - **Zen Staking** - Stakers become only responsible for attestations
        - **Fish Staking** - Reduce minimum staking amount (after increasing Max EB)
        - **Fiverr Staking** - Snarkify everything so you can validate on a smart watch
    - [1:12:13](https://youtu.be/jUFVOUq0-fc?si=5cp_8TP-tSMRrqVT&t=4333) On rollups
        - “If you consume settlement, we say that you are an L2.”
        - “If you consume DA, we say that you are a rollup.”
        - “If you consume the sequencing, we say that you’re based.”
        - “If you consume the virtual machine, we say that you are native.”
        - “If you do all these things, i.e. you are a based, native, and a rollup, then you are an ultrasound rollup, you are the maximally aligned thing possible. But it’s up to you how determined you want to be aligned with Ethereum.”

### Concerns about the Beam chain

- [**Bundling too many things, however, has problematic characteristics…**](https://x.com/peter_szilagyi/status/1856353010349400398) - Péter Szilágyi (Nov 2024)

## Discussions

- **Isn't the beam chain roadmap compatible or something existing client teams (Lighthouse, Prysm, Nimbus, etc.) naturally will adopt anyway?**
    
    > The plan is definitely for existing teams to write beam clients :)
    
- **Are you seeing new client teams tackling the beam chain in new ways and how?**
    
    > The new client teams will add diversity (e.g. jurisdictional, financial, and language diversity) as well as add fresh blood and dynamism. I'm also hoping that the beam fork is the last significant L1 upgrade and that the new client teams can help Ethereum enter maintenance mode.
    
- **Is it necessary to comply with the current consensus spec?**
    
    > Nope! Having said that, a bunch of ancillary infrastructure will be reused (e.g. libp2p, ssz, pyspec) - Justin Drake
    
- **Can we assume that Beam will use the state from a specific future block as its genesis block and proceed from there?**
    
    > Yes, you can assume that :) Existing clients may want to provide support from the beacon history.
    
- **Would it be reasonable for us to focus on building components of the Beam client that are unlikely to be affected by the spec? Does this align with your vision?**
    
    > Yes, potentially! In Q1 and Q2 I'll be working on a proof-of-concept design for the gossip and aggregation of post-quantum signatures. This may involve moving away from gossipsub and it would be good to have early p2p implementations in Q3 or Q4. I also expect some devs to start tinkering with zkVMs like RISC0 and SP1.
    >
    > A potential way to keep devs engaged in 2025 may be to have monthly study clubs where we go through key beam concepts. Another idea is to organise a beam retreat where researchers and devs spend several days together. There will probably also "beam days" around big conferences like EthCC and Devconnect.
    
- **Looking at the strawman timeline, it seems to me like all are beacon chain-worthy and only the "beam fork" is beam-specific?**
    
    > This is how I see the separation of concerns. The incremental stuff (FOCIL, execution auctions, stake capping, Orbit) is done as part of the beacon chain. The rest is pushed to the beam chain.
    > 
    > ![Consensus Layer Roadmap](./figures/cl-roadmap.jpeg)

- **Winternitz OTS as a post-quantum signature candidate**
    > We're specifically looking at Winternitz right now. They are simple, small, efficient. And for Ethereum attestations it's OK for the signatures to be stateful because the messages being signed are indexed by the slot number. (A validator should not accidentally sign two messages with the same slot number because they would get slashed anyway.)
    >
    > Rust library: https://github.com/AtropineTears/Winternitz-OTS