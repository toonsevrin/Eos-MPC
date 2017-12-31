# Eos-MPC
The goal for this repo is to find a way to encode a secret in the blockchain that can be read publically after a condition is met.


## Motivation
Let's say I want to sent someone a private message over the blockchain, but he should only be able to read it after some conditions are met. Is there a way to do this in a decentralised manner?

## Proposal
Suppose Bob wants to send a secret to Alice, which she can only see after a timestamp has passed. 
1. Some secret keepers publish a public encryption key to the contract, along with some tokens as a "deposit" to ensure they will cooperate
2. Alice publishes her public encryption key as well, no deposit.
3. Bob encrypts his secret with Alice's key
4. Bob divides the encrypted secret into n chunks.
5. Bob re-encrypts each chunk with a public key of a secret keeper
6. Bob publishes the encryped chunks, a hash of the original chunk, the timestamp, and some tokens as incentive for the keepers
7. The keepers accept this offer (they could reject it if the incentive is too small or if the hash is wrong)
8. The keepers publish their decrypted chunks once the timestamp is reached (if they publish it too soon, too late, or not matching the hash, the deposit is taken away)
9. Alice reveals the secret by combining the chunks and decrypting them

Replication could be used to decrease the chance of a party failing to decrypt the data.

## Attack vectors

### Cooperation
#### Cooperation between secret keepers and secret receiver
The secret receiver can pay the secret keepers off-chain to reveil their information. Though this cooperation is not trivial, there is incentive to do it (and the keepers will still receive their deposit back).
