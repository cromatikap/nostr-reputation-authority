# [draft] nostr reputation authority

Inspired by the [zap/anti-zap](https://nostr.at/nevent1qqsr5yln0f96nmnnnu8lr09pvrdt7mrayu4537q6mhfahlcu3k0qxfgzyr08ang799m2dtdjl7jlfkup5lvp9j9mv6v25qxu78nk4k64alty24m3gjw) post from [Melvin Carvalho](https://nostr.at/npub1melv683fw6n2mvhl5h6dhqd8mqfv3wmxnz4qph83ua4dk4006ezsrt5c24)

## Description

Each **reputation authority** apply their own **policy** and simply emit a **certification score** event for **users**. **User** have a reputation score per **reputation authority** that will most likely be different from an authority to another.

- Clients can listen to **certification score** events from their favorite authority(ies) and apply timeline filtering accordingly (display score, warnings or hide with "see more comments").  
- Relays can do the same and apply moderation strategy accordingly.

### How it works

Alice and Bob are **user**s of the same **reputation authority**. 
1. Alice creates a note  
2. Bob sends a `upvote` event on Alice's note.  
3. The **reputation authority** emits an event with the updated **certification score** of Alice. [See certification score update flow](src/README.md#certification-score-update-flow)
4. Clients listen to the **certification score** from the **reputation authority** of their choice and apply timeline filtering accordingly

---

Definitions:  
- **user**: pubkey (human, machine or whatever)
- [**NIP-XXX**](NIP-XXX.md): binary messaging representing `upvote` and `downvote` events
- [**reputation authority**](src/README.md): a node that listens to **NIP-XXX** events emitted by relays and changes a **user** score according to their **policy**.
- **certification score**: a score given by the **reputation authority**
- **policy**: the rules determined by **reputation authority** to calculate the **certification score**

---

## Proposal

A **user** accounts reputation authority DVM is composed of a *service* and *registration interface*:

The *service*:

**1. listens to events emitted by relay(s)**  
  - relay is decided by DVM operator
  - event is upvote/downvote from **user** on other **user**'s note

**2. changes a pubkey score accordingly**  
  - if author of event is "certified", then his upvote/downvote weight is higher
  - if **user** of note is "certified", the upvote/downvote weight is lower

**3. emits a replaceable event that state the new score (**NIP-XXX**)**  

### Inspirations

- [nostr.directory](https://nostr.directory/) <- registration interface
- [noswot.org](https://noswot.org) <- reputation score

### NIPs of interest

- [NIP-32](https://github.com/nostr-protocol/nips/blob/master/32.md) Labeling
- [NIP-56](https://github.com/nostr-protocol/nips/blob/master/56.md) Reporting
- [NIP-05](https://github.com/nostr-protocol/nips/blob/master/05.md) Mapping Nostr keys to DNS-based internet identifiers
- [NIP-25](https://github.com/nostr-protocol/nips/blob/master/25.md) Reaction
