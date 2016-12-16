---
title: Diving down the sbot rabbit hole (part 1)
permalink: down-the-sbot-rabbit-hole
date: 2016-12-15 23:31:00
tags: dextech
---

My initial question was:
> how can I spawn a scuttlebot test network?

But then I realized I actually knew nothing of the underlying structures. So instead of just asking my question directly on sbot I started reading the code. Below are notes taken while acquainting myself with some of the modules.

---

### mdmanifest: markdown *manifests* for *muxrpc* apis

  - manifest: dictionary of exposed methods
  - lets you use title ('#'s) in markdown to describe manifests, instead of, say, json.
  - this is great because it allows you to write docs while designing an api, or vice-versa.


### muxrpc: combined *rpc* and *multiplexing*, with *pull-streams*.

  - rpc: call a method on another computer on a shared network
  - multiplexing: when more than one protocol is carried over the same port
  - pull-streams: are to straws what push streams are to pipes
  - takes a manifest of methods in the shape:

  ```
  {
    'method_name': 'type'
  }
  ```
  where type is one of:
  ```
  'async',  // has a callback
  'sync',   // returns a value

  'source'  // returns a source pull-stream (aka, readable)
  'sink',   // returns a sink pull-stream (aka, writable)
  'duplex', // returns a duplex pull-stream
  ```

### chloride: bindings to **libsodium** in nodejs

  - [libsodium][1] : crypto library (c)
  - `crypto_sign_open()`: generate key pairs


### some more pull-streams

  - pull-reader: pulls binary data
  - pull-pushable: kindof a classic stream, but it's still a pull-stream (!)
  - pull-handshake: pull, push, pull, then duplex
  - pull-box-stream: encrypt or decrypt every byte


### secret-handshake: implements a secure key exchange protocol designed with **capability** systems in mind

  - capability: grants to the bearer the right to access a resource
  - mutually authenticates client and server
  - a peer is identified by it's public key
  - [Authenticated Key Exchange as a Capability System][2]

---


*Next up: multiserver & secret-stack*


[1]: https://download.libsodium.org/doc/
[2]: http://dominictarr.github.io/secret-handshake-paper/shs.pdf





