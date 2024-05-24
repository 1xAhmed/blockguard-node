# Blockguard Node Instructions

Follow this guide to Prepare a local relay chain
Prepare a local relay chain
[Prepare a local relay chain](https://docs.substrate.io/tutorials/build-a-parachain/prepare-a-local-relay-chain)

This command will not work
`git clone --branch release-v1.0.0 https://github.com/paritytech/polkadot-sdk.git`

Download from github directly
[Download Polkadot v1.0.0](https://github.com/paritytech/polkadot/archive/refs/tags/v1.0.0.zip)


The rest is pretty straightforward

After running local relay chain, Run Blockguard node by following these steps


## Step 1: Clone the repo and switch to blockguard-v0.0.1 branch
Blockguard Node Repo

## Step 2 Build the node by this command
```bash
cargo build --release
```

## Step 3 Generate the plain text chain specification for the blockguard node by running the following command:
```bash
./target/release/blockguard-node build-spec --disable-default-bootnode > plain-blockguard-chainspec.json
```

## Step 4 Generate a raw chain specification file from the modified chain specification file by running the following command:

```bash
./target/release/blockguard-node build-spec --chain plain-blockguard-chainspec.json --disable-default-bootnode --raw > raw-blockguard-chainspec.json
```

## Step 5 Export the WebAssembly runtime for the parachain.

```bash
./target/release/blockguard-node export-genesis-wasm --chain raw-blockguard-chainspec.json para-2000-wasm
```

## Step 6 Generate a parachain genesis state.

```bash
./target/release/blockguard-node export-genesis-state --chain raw-blockguard-chainspec.json para-2000-genesis-state
```

## Step 7 Start a collator node with a command similar to the following:

```bash
./target/release/blockguard-node \
--alice \
--collator \
--force-authoring \
--chain raw-blockguard-chainspec.json \
--base-path /tmp/parachain/alice \
--port 40333 \
--rpc-port 8844 \
-- \
--execution wasm \
--chain ../path/to/polkadots/raw-local-chainspec.json \
--port 30343 \
--rpc-port 9977
```

Now if your local relay chain is running, blockguard should be able to connect to it and successfully run.

Follow the next steps in this guide



[Substrate Node Template](https://github.com/substrate-developer-hub/substrate-node-template)
