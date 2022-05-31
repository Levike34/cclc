<div align="center">

  <h1><code>substrate-stencil</code></h1>

  <strong>A template for kick starting a Rust and Blockchain project using <a href="https://github.com/paritytech/substrate">Substrate</a>.</strong>

  <h3>
    <a href="https://substrate.io/">Docs</a>
    <span> | </span>
    <a href="https://matrix.to/#/!HzySYSaIhtyWrwiwEV:matrix.org?via=matrix.parity.io&via=matrix.org&via=web3.foundation">Chat</a>
  </h3>

</div>

## Features

This template includes the minimum required components to start a PoS testnet, inspired by [substrate-node-template](https://github.com/substrate-developer-hub/substrate-node-template).

* Consensus related pallets: Babe & GRANDPA
* Staking related pallets: staking, session, authorship, im-online, offences, utility
* Governance related pallets: collective, membership, elections-phragmen, democracy, treasure

**Notes:** The code is un-audited and not production ready, use it at your own risk.

## Getting Started

Follow the steps below to get started.

### Rust Setup

First, complete the [Dev Docs Installation](https://docs.substrate.io/v3/getting-started/installation/).

### Build and Run

Use the following command to build the node and run it after build successfully:

```sh
cargo build --release
./target/release/substrate-stencil --dev
```

## Run public testnet

* Modify the genesis config in chain_spec.rs
* Build spec, `./target/release/substrate-stencil build-spec --chain staging > stencil-staging.json`
* Change original spec to encoded raw spec, `./target/release/substrate-stencil build-spec --chain=stencil-staging.json --raw > stencil-staging-raw.json`
* Start your bootnodes, node key can be generate with command `./target/release/substrate-stencil key generate-node-key`.
  ```shell
  ./target/release/substrate-stencil \
       --node-key a9772c23421bdc2b2b953d91d7d41eec180448d268c534c1250dd80a93ab3adf \
       --base-path /tmp/bootnode1 \
       --chain stencil-staging-raw.json \
       --name bootnode1
  ```
* Start your initial validators,
  ```shell
  ./target/release/substrate-stencil \
      --base-path  /tmp/validator1 \
      --chain   stencil-staging-raw.json \
      --bootnodes  /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWJdgAVLxCA5M7EB2CHJApGEfdW5Tdr23JnMgZaJBFPiEE\
	    --port 30336 \
	    --ws-port 9947 \
	    --rpc-port 9936 \
      --name  validator1 \
      --validator
  ```
* [Insert session keys](https://substrate.dev/docs/en/tutorials/start-a-private-network/customchain#add-keys-to-keystore)
* Attract enough validators from community in waiting
* Call force_new_era in staking pallet with sudo, rotate to PoS validators
* Enable governance, and remove sudo
* Enable transfer and other functions

./target/release/substrate-stencil key insert --base-path /tmp/validator1 \
--chain stencil-staging-raw.json  \
--scheme Sr25519 \
--suri "owner word vocal dose decline sunset battle example forget excite gentle waste//1//stash" \
--password pass \
--key-type aura

./target/release/substrate-stencil key insert --base-path /tmp/validator1 \
--chain stencil-staging-raw.json  \
--scheme Sr25519 \
--suri "owner word vocal dose decline sunset battle example forget excite gentle waste//1//controller" \
--password pass \
--key-type aura


  Secret Key URI `owner word vocal dose decline sunset battle example forget excite gentle waste//1//stash` is account:
    Network ID/version: substrate
    Secret seed:        0x4e73cec7a4023d8dbccbd54cba395883480a8f7228179e3de55d7fc067fe86cf
    Public key (hex):   0xd41e0bf1d76de368bdb91896b0d02d758950969ea795b1e7154343ee210de649
    Account ID:         0xd41e0bf1d76de368bdb91896b0d02d758950969ea795b1e7154343ee210de649
    SS58 Address:       5Grpw9i5vNyF6pbbvw7vA8pC5Vo8GMUbG8zraLMmAn32kTNH
  Secret Key URI `owner word vocal dose decline sunset battle example forget excite gentle waste//1//controller` is account:
    Network ID/version: substrate
    Secret seed:        0x013f446b2911f86518a65528e833f59dce641878b1719de7bfa0934520ff6193
    Public key (hex):   0x382bd29103cf3af5f7c032bbedccfb3144fe672ca2c606147974bc2984ca2b14
    Account ID:         0x382bd29103cf3af5f7c032bbedccfb3144fe672ca2c606147974bc2984ca2b14
    SS58 Address:       5DLMZF33f61KvPDbJU5c2dPNQZ3jJyptsacpvsDhwNS1wUuU
  Secret Key URI `owner word vocal dose decline sunset battle example forget excite gentle waste//2//stash` is account:
    Network ID/version: substrate
    Secret seed:        0x35610dd371805384bf2064fe7df2876847bceded13035374018c5b10189a1a05
    Public key (hex):   0x08050f1b6bcd4651004df427c884073652bafd54e5ca25cea69169532db2910b
    Account ID:         0x08050f1b6bcd4651004df427c884073652bafd54e5ca25cea69169532db2910b
    SS58 Address:       5CFDk3yCSgQ2goiaksMfRMFRS7ZU28BZqPQDeAsgZUa6FRzt
  Secret Key URI `owner word vocal dose decline sunset battle example forget excite gentle waste//2//controller` is account:
    Network ID/version: substrate
    Secret seed:        0x7b17d79aaa416814f058b206654891e104d8b8b8dd34d86a6c8664863ee3224a
    Public key (hex):   0x8275157f2a1d8373106cb00078a73a92a3303f3bf6eb72c3a67413bd943b020b
    Account ID:         0x8275157f2a1d8373106cb00078a73a92a3303f3bf6eb72c3a67413bd943b020b
    SS58 Address:       5F1ks2enazaPktQa3HURLK8GywzNZaGirovPtFvvbv91TLhJ
