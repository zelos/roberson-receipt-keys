# Roberson receipt keys

Roberson is a record of what a person agreed to about their name, image, voice and likeness. It issues a signed receipt when a use is cleared. Roberson is a product of Zelos Inc.

This repository publishes the public keys that check those signatures. It exists so that a key can be checked somewhere other than Roberson's own servers, and so that the history of each key is public. If Roberson changed a key, the commit history here would show it.

## Status

**No key is published yet.** `keys.json` is empty. Receipts issued today use a shared-secret signature that only Roberson can check. Public-key receipts are being built. This page will say when they begin.

## What is here

`keys.json` will hold a list of public keys in JSON Web Key form. Each key has an id (`kid`), and a signed receipt names the key that signed it. Keys are added and never removed, so an old receipt can always be checked.

## How a check will work

A signed receipt has three fields: `keyId`, `payload` and `signature`.

1. Find the entry in `keys.json` whose `kid` equals `keyId`.
2. Build the signed text from `{ "keyId": keyId, "payload": payload }`. Sort object keys at every level, use no whitespace, and drop undefined values.
3. Check `signature` (Ed25519, base64url) against the UTF-8 bytes of that text, using the key's `x` value.

This needs no account and no call to Roberson.

## What a valid signature shows

It shows that Roberson issued exactly that content under that key. It does not show that the underlying agreement is true, that the person who confirmed is who they said, or that the receipt still stands today. It is not legal certification.

## Contact

Chris Williams, chris@zelos.ai
