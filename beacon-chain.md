# Beacon chain

Study materials on the Ethereum Beacon chain.

## Beacon chain specs
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

## Beacon chain _annotated_ specs

- [Weak Subjectivity in Eth2.0](https://notes.ethereum.org/@adiasg/weak-subjectvity-eth2) - Aditya Asgaonkar (Sep 2020)
- [Phase 0 for Humans \[v0.10.0\]](https://notes.ethereum.org/@djrtwo/Bkn3zpwxB) - Danny Ryan (Jul 2021)
- [Upgrading Ethereum: A technical handbook on Ethereum's move to proof of stake and beyond](https://eth2book.info/capella/) - Ben Edgington (2023)
- [Engine API: A Visual Guide](https://hackmd.io/@danielrachi/engine_api) - Daniel Ramirez (Feb 2024)

## Beacon chain design rationales

- [Vitalik's annotated eth2 spec with a focus on design rationale](https://github.com/ethereum/annotated-spec) - Vitalik (2020 - current)
- [Serenity Design Rationale](https://notes.ethereum.org/@vbuterin/serenity_design_rationale) - Vitalik (Jan 2022)

## Beacon chain pitfalls, lessons learnt & improvement ideas

- [**Reducing Beacon Chain Bandwidth for Institutional and Home Stakers**](https://www.youtube.com/watch?v=u8JJh-E-VMg) ([slides](https://archive.devcon.org/resources/6/reducing-beacon-chain-bandwidth-for-institutional-and-home-stakers.pdf)) - Adrian Manning, Diva (SigmaPrime/Lighthouse) at Devcon Bogota (Oct 2022)
- [**Beacon chain design mistakes**](https://www.youtube.com/watch?v=10Ym34y3Eoo) ([slides](https://docs.google.com/presentation/d/1LkxHrXjQyRh2i75R13yjndc_aUp9oXTAdAw538XfJhk/edit?usp=sharing)) - Justin Drake at EthStaker's Staking Gathering (Nov 2023)
- [**Staking Incidents**](https://ethstaker.cc/incidents) - EthStakers (2023 - 2024)
- [**Ethereum Node Message Propagation Bandwidth Consumption**](https://ethresear.ch/t/ethereum-node-message-propagation-bandwidth-consumption/19952) - yiannisbot (Jul 2024)
- [**Where’s the home staking bandwidth research?**](https://ethresear.ch/t/wheres-the-home-staking-bandwidth-research/20507) - ryanberckmans (Sep 2024)
- [Bandwidth Availability in Ethereum: Regional Differences and Network Impacts](https://ethresear.ch/t/bandwidth-availability-in-ethereum-regional-differences-and-network-impacts/21138) - cortze and yiannisbot (Dec 2024)

## Beacon chain client-specific analyses

- [**Compare ROI of 3 eth2 Clients**](https://trademotif-46434.medium.com/compare-roi-of-3-eth2-clients-d5862b372c0d) - motif (Oct 2020)
- [**Move from teku to prysm**](https://www.reddit.com/r/ethstaker/comments/ph3h7z/move_from_teku_to_prysm/) - r/ethstaker (Sep 2021)
- [**Which clients are having issues post-merge? Recommendations?**](https://www.reddit.com/r/ethstaker/comments/xmrriw/which_clients_are_having_issues_postmerge/) - r/ethstaker (Sep 2022)
- [**Considering Client Diversity through the lens of Network Performance**](https://ethresear.ch/t/considering-client-diversity-through-the-lens-of-network-performance/18885) - U. Natale and G. Sofia (Mar 2024)