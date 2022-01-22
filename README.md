# Rust-Counter-Smart-Contract

A simple smart contract that serves as a Counter, incrementing, decrementing and returning the counter value.

This smart contract is written in the [Rust programming language](https://www.rust-lang.org/).

### Prerequisites

- Install Rust
- Create a NEAR account - for this example we use testnet wallet
- Install `near-cli`

### Notes

Smart contracts from NEAR usually have a primary file that holds the code `./src/lib.rs` - this is the conventional filename for the rust library.

When writing smart contracts, the pattern is to have a `struct` with an associated `impl` where you write the core logic into functions.
"...most functions will end up being inside impl blocks..." - Rust docs.

We use attributes specific to NEAR:
```
#[near_bindgen]
#[derive(Default, BorshDeserialize, BorshSerialize)]
```
These essentially allow the compilation into WebAssembly to be compatible and optimized for the NEAR blockchain.

You can use the context `env` to get useful information including :
- **signer_account_id** - account id that signed the original transaction that led to the execution of the smart contract
- **attached_deposit** - if someone sent tokens along with the call
- **account_balance** - balance attached to the given account

### Deploying the smart contract
step 1 => login with `near-cli` by running the command `near login`

step 2 => deploy the contract to your testnet account .
```
near deploy --wasmFile target/wasm32-unknown-unknown/release/rust_counter_tutorial.wasm --accountId YOUR_ACCOUNT_HERE
```
step 3 => test the contract by running the commands below
```
near call YOUR_ACCOUNT_HERE increment --accountId YOUR_ACCOUNT_HERE

near call YOUR_ACCOUNT_HERE decrement --accountId YOUR_ACCOUNT_HERE


near view YOUR_ACCOUNT_HERE get_num --accountId YOUR_ACCOUNT_HERE
```

