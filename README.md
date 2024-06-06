# [draft] nostr user accounts reputation authority

Inspired by the [zap/anti-zap](https://nostr.at/nevent1qqsr5yln0f96nmnnnu8lr09pvrdt7mrayu4537q6mhfahlcu3k0qxfgzyr08ang799m2dtdjl7jlfkup5lvp9j9mv6v25qxu78nk4k64alty24m3gjw) post from [Melvin Carvalho](https://nostr.at/npub1melv683fw6n2mvhl5h6dhqd8mqfv3wmxnz4qph83ua4dk4006ezsrt5c24)

## Definitions

- user: pubkey

## Proposal

An user accounts reputation authority DVM is composed of a *service* and *registration interface*:

The *service*:

**1. listens to events emitted by relay(s)**  
  - relay is decided by DVM operator
  - event is upvote/downvote from user on other user's note

**2. changes a pubkey score accordingly**  
  - if author of event is "certified", then his upvote/downvote weight is higher
  - if user of note is "certified", the upvote/downvote weight is lower

**3. emits a replaceable event that state the new score (NIP-XXX)**  
  - apps can listen to events from their favorite authority(ies) and apply timeline filtering accordingly (display score, warnings or hide with "see more comments")
  - relays can listen to events from their favorite authority(ies) and apply moderation strategy accordingly

## Notes

With this design, the authority node doesn't need to keep the entire history.
The database would be used only to store pubkey and external verification proofs that users will make via a registration interface

### Inspirations

- [nostr.directory](https://nostr.directory/) <- registration interface
- [noswot.org](https://noswot.org) <- reputation score

### NIPs of interest

- NIP-05 Verification
- NIP-25 Reaction
