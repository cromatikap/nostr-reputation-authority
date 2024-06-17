# [draft] nostr reputation authority

The role of the reputation authority is to listen to [binary vote events](../NIP-XXX.md) made by the action of upvote or downvote from a user on a note and emit a new **certification score** for the author of the note accordingly.  

## Requirements

- Only one vote per **user** per note

## Certification score update flow

The **reputation authority**:  
1. listens the `upvote` event (see [NIP-XXX](../NIP-XXX.md))
2. calculates the new `score` of Alice
3. emits a `certification score` event for Alice see [NIP-XXX](../NIP-XXX.md)

With this design, the **reputation authority** node doesn't need to keep the entire history of user interactions.
The database would be used only to store pubkey and eventually external verification proofs that **user**s will make via a registration interface

## Certification score calculation

### Definitions

`upvote`: upvote event as described in **NIP-XXX**  
`downvote`: downvote event as described in **NIP-XXX** ([punishment weight](https://github.com/cromatikap/nostr-reputation-authority/issues/1#issue-2340420197))  
`Alice score`: **certification score** of the **user** Alice
`Bob score`: **certification score** of the **user** Bob  
`Bob rating value`: as defined in **NIP-XXX** takes the value `upvote` or `downvote` sent by Bob to Alice's note  

### Examples of implementation

#### 1. Minimum implementation

`upvote` = 1  
`downvote` = -3  
`Alice score` = `Alice score` + `Bob score` * `Bob rating value`

#### 2. Using NIP-320

The **reputation authority** listen to [NIP-320 events](https://github.com/nostr-protocol/nips/pull/604) to get the **user** `rating mass` value.

#### 3. Certification score based on social graph

The **reputation authority** uses the social graph of the **user** to calculate the **certification score** like the major social network platforms do.
