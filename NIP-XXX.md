# [draft] NIP-XXX: upvote/downvote and certification score

Definitions:  
**user**: pubkey (human, machine or whatever)

## Description

A simple messaging protocol to send/receive binary values representing `upvote` and `downvote` of a note by a **user**.

### binary vote event (upvote/downvote signals)

```
{
  "kind": ???,
  "pubkey": <32-bytes lowercase hex-encoded public key of the event creator>,
  "tags": [
    ["vote", <1 or 0 if it is upvote or downvote>],
  ],
  "content": <OPTIONAL reason>,
}
```

### certification score update event

```
{
  "kind": ???,
  "pubkey": <32-bytes lowercase hex-encoded public key of the event creator>,
  "tags": [
    ["reputation", <new reputation score>],
  ],
}
```