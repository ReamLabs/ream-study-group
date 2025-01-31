# ream-study-group

A collection of learning materials on the Beam chain and Ream client.

## Table of Content

- **Meeting notes** - See [Meeting notes](#meeting-notes) below.
- **Beacon chain** - See the [Beacon chain](./beacon-chain.md) page.
- **Beam chain** - See [Beam chain](#beam-chain) section below.
- **Development notes** - See our development notes at [ReamLabs' HackMD](https://hackmd.io/@reamlabs).

## Meeting Notes

| №   | Date                          | Notes                           | Recordings                                |
| --- | ----------------------------- | ------------------------------- | ----------------------------------------- |
| 008 | Jan 27, 2024, 14:30-15:10 UTC | [Notes](./meeting-notes/008.md) | [Recording](https://youtu.be/BuUxOhd9VbI) |
| 007 | Jan 13, 2024, 14:30-15:10 UTC | [Notes](./meeting-notes/007.md) | [Recording](https://youtu.be/AeGFI3vWWOE) |
| 006 | Jan 6,  2024, 14:30-15:30 UTC | [Notes](./meeting-notes/006.md) |                                           |
| 005 | Dec 23, 2024, 14:30-15:30 UTC | [Notes](./meeting-notes/005.md) | [Recording](https://youtu.be/JblYpv-SAJo) |
| 004 | Dec 17, 2024, 14:30-15:30 UTC | [Notes](./meeting-notes/004.md) | [Recording](https://youtu.be/JYYKFzppQrQ) |
| 003 | Dec 10, 2024, 14:30-15:30 UTC | [Notes](./meeting-notes/003.md) | [Recording](https://youtu.be/2I8SVWsfQkY) |
| 002 | Dec 2, 2024, 14:30-16:00 UTC  | [Notes](./meeting-notes/002.md) | Not available                             |
| 001 | Late November, 2024           | Not available                   | Not available                             |

## Beam chain

### Beam chain proposals

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
- [**Beam chain tldr**](https://www.youtube.com/watch?v=63w7kHh737w) - Devcon SEA Community-Led Session: Ethereum Magicians Infinite Endgames - Ethereum Execution
    - "It's about doing a merge again / replacing the consensus layer, redesign everything with inclusion lists, make everything quantum secure, a fresh start. Get rid of Beacon Chain and replace with everything we learned from Beacon." - Guillaume
    - "Continual improvement is really a governance question and a decentralized governance problem. As an ecosystem we've gotten more conservative, need a big change, and Beam has the potential to be a significant change." - Guillaume
    - "ZK is a big part of the beam change and increased dependency on EL to have zk. The Beam change is about ZK. Also single slot and faster finality" - Alexi
    - "faster finality would be nice to have, this is a great usability change, francesco (EF) doing lots of work on this" - Guillaume
    - "This is probably my number 1 concern. There are two classes of big projects: things we know how to do but are difficult given the legacy environment and things we don't know how to do yet. Beam chain contains both of these. There are things we can change but are very difficult to do while the airplane is in the air. Need full confidence before we can ship." - lightclient
- [**Future of Ethereum: Beam Chain**](https://medium.com/@organmo/future-of-ethereum-1-beam-chain-52492e39af62) - Seungmin Jeon (Jan 2025)
  - Semi-technical elaborations on the Beam Chain objectives:
    - Shorter/Single-Slot Finality with Orbit SSF
    - Shortening block time to 4 seconds
    - Preconfirmations
    - Chain Snarkification
    - Quantum-Resistant Signatures

### Related specifications

- [Hardware and Bandwidth Requirements for Full Nodes and Validators](https://github.com/ethereum/EIPs/pull/9270)
  - Original document for hardware requirements: https://hackmd.io/G3MvgV2_RpKxbufsZO8VVg?view
  - Original document for bandwidth requirements: https://hackmd.io/DsDcxDAVShSSLLwHWdfynQ?view

### Concerns about the Beam chain

- [**Bundling too many things, however, has problematic characteristics…**](https://x.com/peter_szilagyi/status/1856353010349400398) - Péter Szilágyi (Nov 2024)

### Discussions

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