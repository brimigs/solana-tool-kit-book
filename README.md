---
# metadata up here
---

The Solana Toolkit consists of all open sourced tools for smart contract development on the Solana Blockchain.

You can contribute to this book on [GitHub]().

## Installation

To get started, install The Solana toolkit:

```shell
npx solana install
```

This will install the latest versions of the following:

- [Solana CLI / Agave Tool Suite](https://docs.anza.xyz/cli/): A command line tool that allows developers to interact with the Solana blockchain, manage accounts, send transactions, and deploy programs.
- [Rust](https://doc.rust-lang.org/book/): The Programming language that Solana Smart Contracts are written in.
- [Anchor](https://www.anchor-lang.com/): A framework for writing Solana programs that abstracts many complexities to speed up smart contract development.
- [Trident](https://ackee.xyz/trident/docs/latest/): A fuzz tester
- [Zest](https://github.com/LimeChain/zest?tab=readme-ov-file): A code coverage tool

## Getting Started

This section will cover all the toolkit basics to help you get started.

### Keypair generation

For a fresh installation of the [Solana CLI](https://docs.anza.xyz/cli/), you're required to generate a new keypair. 

```shell
solana-keygen new
```

The above command will both:
- print the pubkey generated
- store the your new keypair at the Solana CLI's default path (`~/.config/solana/id.json`) unless you already have a keypair saved there
 
Check the pubkey of your machine's newly generated keypair: 

```shell
solana address
```

### Configuration

Check your current configuration:

```shell
solana config get
```

You can configure your RPC to connect to either mainnet, testnet, devnet, or your localhost.

When using this toolkit, most of the time you'll want to be connected to a local node.

Update your Solana configuration to connect to localhost:

```shell
solana config set --url localhost
```

To test locally, you must also spin up a local node to run on your localhost:

```shell
solana-test-validator
```

To log the network run:

```shell
solana logs
```

For a more information, read this [Solana Test Validator Guide](https://solana.com/developers/guides/getstarted/solana-test-validator).

## Projects

### Creating a New Project

To start a new project with the Solana toolkit, pick which scaffold you want to use. There are scaffolds for:
- [Anchor framework workspaces](#anchor-smart-contract-scaffold)
- [general scaffolds using `create-solana-program`](#general-smart-contract-scaffold)
- [web app workspaces](#web-app-scaffold)
- [mobile app workspaces](#mobile-app-templates)

### Anchor Smart Contract Scaffold

```shell
anchor init <project_name>
```

This initializes a simplistic workspace set up for Anchor smart contract development, with the following structure:

- `Anchor.toml`: Anchor configuration file.
- `Cargo.toml`: Rust workspace configuration file.
- `package.json`: JavaScript dependencies file.
- `programs/`: Directory for Solana program crates.
- `app/`: Directory for your application frontend.
- `tests/`: Directory for JavaScript integration tests.
- `migrations/deploy.js`: Deploy script.

The Anchor framework abstracts away many complexities enabling fast program development.

For more information on the Anchor framework, check out the [Anchor book](https://www.anchor-lang.com/).

To test out this project before making any modifications, just build and test:

```shell
anchor build
```

```shell
anchor test
```

### General Smart Contract Scaffold

```shell
npx create-solana-program
```

This initializes a more complex workspace with everything you need for general Solana smart contract development.

This command gives you the option to choose between Shank and Anchor for the program framework:

- **Shank** creates a vanilla Solana smart contract with Shank macros to generate IDLs. For more information on Shank, check out its [README](https://github.com/metaplex-foundation/shank).

- **Anchor** creates a smart contract using the Anchor framework, which abstracts away many complexities enabling fast program development. For more information on the Anchor framework, check out the [Anchor book](https://www.anchor-lang.com/).

This command also gives the option to choose between a JavaScript client, a Rust Client, or both.

- **JavaScript Client** creates a typescript library compatible with [web3.js](https://solana-labs.github.io/solana-web3.js/).

- **Rust Client** creates a rust crate allowing consumers to interact with the smart contract.

For further workspace customization and additional information, check out the `create-solana-program` [README](https://github.com/solana-program/create-solana-program/tree/main).

### Web App Scaffold

```shell
npx create-solana-dapp
```

This command generates a new project that connects a Solana smart contract to a frontend with a wallet connector.

For additional information, check out its [README](https://github.com/solana-developers/create-solana-dapp).

To test out this project before making any modifications, follow these steps:

1. Build the smart contract:

```shell
npm run anchor-build
```

2. Start the local validator:

```shell
npm run anchor-localnet
```

3. Run tests:

```shell
npm run anchor-test
```

4. Deploy to the local validator:

```shell
npm run anchor deploy --provider.cluster localnet
```

5. Build the web app:

```shell
npm run build
```

6. Run the web app:

```shell
npm run dev
```

### Mobile App Templates

```shell
yarn create expo-app --template @solana-mobile/solana-mobile-expo-template
```

This is initializing a new project using the Expo framework that is specifically designed for creating mobile applications that interact with the Solana blockchain.

Follow their [Running the app](https://docs.solanamobile.com/react-native/expo#running-the-app) guide to launch the template as a custom development build and get it running on your Android emulator. Once you have built the program and are running a dev client with Expo, the emulator will automatically update every time you save your code.

To use this template, you will also need to set up the following:

- [Android Studio and Emulator](https://docs.solanamobile.com/getting-started/development-setup)
- [React Native](https://reactnative.dev/docs/environment-setup?platform=android)
- [EAS CLI and Account](https://docs.expo.dev/build/setup/)

For additional information on Solana Mobile Development: https://docs.solanamobile.com/getting-started/intro

## Smart Contract Layout

Typically Solana smart contract (aka [programs](/docs/core/programs.md)) workspaces will be have the following file structure:

```shell
.
├── app
├── migrations
├── node_modules
├── programs
├── target
└── tests
```

The main smart contract is the `lib.rs` file, which lives insides the `programs` directory, as shown below:

```shell
.
├── app
├── migrations
├── node_modules
├── programs
    ├── src
        ├── lib.rs
├── target
└── tests
```

As the smart contract gets more cumbersome, you'll typically want to separate the logic into multiple files, as shown below:

```shell
├── programs
    ├── src
        ├── state.rs
        ├── instructions
            ├── instruction_1.rs
            ├── instruction_2.rs
            ├── instruction_3.rs
        ├── lib.rs
        ├── constants.rs
        ├── error.rs
        ├── mod.rs
```

## Working on an Existing Project

The Solana toolkit makes developing with existing projects have no overhead.

```shell
npm install
```

```shell
npx solana build
```

```shell
npx solana test
```

```shell
npx solana deploy
```

## Verifiable Programs

## Dependencies??

## Solana Test Suite Overview

Within the Solana toolkit, there are several resources for testing Solana Smart Contracts, including:

- Zest - A fuzzer
- A code coverage tool
- A framework for testing Solana programs in NodeJS that spins up a lightweight `BanksServer` that's like an RPC node but much faster and creates a `BanksClient` to talk to the server.
- A fast and lightweight library for testing Solana programs in Rust, which works by creating an in-process Solana VM optimized for program developers.
- A tool to scan your repo for common security vulnerabilities and provide suggestions for fixes.
- A reference guide of important cheat codes to simplify writing tests.

### Testing Basics

Sync all the program's key. If you're using an Anchor program:

```shell
anchor keys sync
```

Build the smart contract:

```shell
npx solana build
```

Test the smart contract:

```shell
npx solana test
```

Deploy the smart contract:

```shell
npx solana deploy
```

If deploying to localnet, you must first start your local validator:

```shell
solana-test-validator
```

For more information on local validator customization and commands, read the [Solana Test Validator Guide](https://solana.com/developers/guides/getstarted/solana-test-validator).

### Fuzz Tester

Generate fuzz tests:

```shell
npx solana fuzz
```

This command will initialize a Trident workspace and generate a new Fuzz Test Template:

```shell
project-root
├── trident-tests
│   ├── fuzz_tests # fuzz tests folder
│   │   ├── fuzz_0 # particular fuzz test
│   │   │   ├── test_fuzz.rs # the binary target of your fuzz test
│   │   │   └── fuzz_instructions.rs # the definition of your fuzz test
│   │   ├── fuzz_1
│   │   ├── fuzz_X # possible multiple fuzz tests
│   │   ├── fuzzing # compilations and crashes folder
│   │   └── Cargo.toml
├── Trident.toml
└── ...
```

Run fuzz tests:

```shell
npx solana fuzz run
```

The output of the fuzz tests is as follows:

1. Number of Fuzzing Iterations.
2. Feedback Driven Mode = Honggfuzz generates data based on the feedback (i.e. feedback based on Coverage progress).
3. Average Iterations per second.
4. Number of crashes it found (panics or failed invariant checks).

```shell
------------------------[  0 days 00 hrs 00 mins 01 secs ]----------------------
  Iterations : 688 (out of: 1000 [68%]) # -- 1. --
  Mode [3/3] : Feedback Driven Mode # -- 2. --
      Target : trident-tests/fuzz_tests/fuzzing.....wn-linux-gnu/release/fuzz_0
     Threads : 16, CPUs: 32, CPU%: 1262% [39%/CPU]
       Speed : 680/sec [avg: 688] # -- 3. --
     Crashes : 1 [unique: 1, blocklist: 0, verified: 0] # -- 4. --
    Timeouts : 0 [10 sec]
 Corpus Size : 98, max: 1048576 bytes, init: 0 files
  Cov Update : 0 days 00 hrs 00 mins 00 secs ago
    Coverage : edge: 10345/882951 [1%] pc: 163 cmp: 622547
---------------------------------- [ LOGS ] ------------------/ honggfuzz 2.6 /-
```

View the source code [here](https://github.com/Ackee-Blockchain/trident).

### Code Coverage Tool

```shell
npx solana coverage
```

This command will run a code coverage test on all of your Rust tests and then generate report in an HTML page with in depth metrics on where additional code may be needed to improve your current code coverage.

Note: So far, this tool only works on tests written in Rust and is not compatible with a JavaScript test suite.

View the source code [here](https://github.com/LimeChain/zest?tab=readme-ov-file).

### JavaScript Testing Framework

### Rust Testing Library

### Security Vulnerability Scanner

## Solana Cheat Codes

Most of the time, simply testing your smart contract's outputs isn’t enough. To manipulate the state of the blockchain, as well as test for specific reverts and events, you can use the

```Rust
// Example Rust function to adjust account balances in a test environment
use solana_program::account_info::{AccountInfo};
use solana_program::program_error::ProgramError;
use std::{str::FromStr};

fn adjust_account_balance(account: &AccountInfo, amount: u64) -> Result<(), ProgramError> {
    let mut data = account.try_borrow_mut_data()?;
    let mut balance = u64::from_le_bytes(data.clone()[0..8].try_into().unwrap());
    balance += amount;
    data[0..8].copy_from_slice(&balance.to_le_bytes());
    Ok(())
}

// This function would be part of a larger testing utility library that could be invoked during tests
```

## Running a local network

The Solana test validator is a local emulator for the Solana blockchain, designed to provide developers with a private and controlled environment for building and testing Solana programs without the need to connect to a public testnet or mainnet. If you have the Solana CLI tool suite already installed, you can run the test validator with the following command:

```shell
solana-test-validator
```

Advantages #

- Ability to reset the blockchain state at any moment
- Ability to simulate different network conditions
- No RPC rate-limits
- No airdrop limits
- Direct on-chain program deployment
- Ability to clone accounts from a public cluster
- Ability to load accounts from files
- Configurable transaction history retention
- Configurable epoch length
- Installation #

Since the `solana-test-validator` is part of the Solana CLI tool suite, ensure you have Solana's command-line tools installed. You can install the entire Solana toolkit (which includes the Solana CLI) using the following command:

```shell
npx solana install
```

Or install just the Solana CLI with:

```shell
sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"
```

You can replace `stable` with the release tag matching the software version of your desired release (i.e. `v1.18.12`), or use one of the three symbolic channel names: `stable`, `beta`, or `edge`.

### Starting the Test Validator

To start your local validator, simply run:

```shell
solana-test-validator
```

This command initializes a new ledger and starts the validator.

### Interacting with a Running Test Validator

Once you have the `solana-test-validator` up and running, you can interact with it using various Solana CLI commands. These commands let you deploy programs, manage accounts, send transactions, and much more. Here's a detailed guide on the key commands you will use.


Check your current CLI configuration to see which network you are selected too:

```shell
solana config get
```

If needed update your Solana configuration to connect to your test validator running on localhost:

```shell
solana config set --url localhost
```

### Checking the Status of the Test Validator

Before interacting with the test validator, it's useful to confirm its status and ensure it is running correctly.

```shell
solana ping
```

This command pings the local test validator and returns the current blockhash and latency, verifying that it is active.

### Account Management

View the pubkey of your configured CLI keypair:

```shell
solana address
```

View the current balance of your keypair:

```shell
solana balance
```

To add SOL to your CLI keypair, request an airdrop:

```shell
solana airdrop 10
```

To retrieve details about any account, such as its balance and owner:

```shell
solana account <ACCOUNT_ADDRESS>
```

You must first add SOL to an account for it to exist. This airdrop command requests 2 SOL to the specified account address:

```shell
solana airdrop 2 <ACCOUNT_ADDRESS>
```

Aside from "wallet accounts" that only hold SOL, accounts are normally created by smart contracts (aka programs) so they can store the `data` desired by that program.

### Deploying and Managing Programs

To deploy a compiled program (BPF) to the test validator:

```shell
solana program deploy <PROGRAM_FILE_PATH>
```

This uploads and deploys a program to the blockchain.

To check the details of a deployed program:

```shell
solana program show <ACCOUNT_ADDRESS>
```

### Sending Transactions

To transfer SOL from one account to another:

```shell
solana transfer --from /path/to/keypair.json <RECIPIENT_ADDRESS> <AMOUNT>
```

This sends `AMOUNT` of SOL from the source account to the `RECIPIENT_ADDRESS`.

### Simulating and Confirming Transactions

Before actually sending a transaction, you can simulate it to see if it would likely succeed:

```shell
solana transfer --from /path/to/keypair.json --simulate <RECIPIENT_ADDRESS> <AMOUNT>
```

To confirm the details and status of a transaction:

```shell
solana confirm <TRANSACTION_SIGNATURE>
```

### Viewing Recent Block Production

To see information about recent block production, which can be useful for debugging performance issues:

```shell
solana block-production
```

### Creating Token Accounts

### Adjusting Logs

For debugging, you might want more detailed logs:

```shell
solana logs
```

This streams log messages from the validator.

### Tips for Logging

- Increase log verbosity with the `-v` flag if you need more detailed output for debugging.
- Use the `--rpc-port` and `--rpc-bind-address` options to customize the RPC server settings.
- Adjust the number of CPU cores used by the validator with the `--gossip-host` option to simulate network conditions more realistically.

### Configuration

Check CLI Tool Suite configuration:

```shell
solana genesis-hash
```

View all the configuration options available for the Solana test validator:

```shell
solana-test-validator --help
```

### Local Ledger

By default, the ledger data is stored in a directory named `test-ledger` in your current working directory.

### Specifying Ledger Location

When starting the test validator, you can specify a different directory for the ledger data using the `--ledger` option:

```shell
solana-test-validator --ledger /path/to/custom/ledger
```

### Resetting the Ledger

By default the validator will resume an existing ledger, if one is found. To reset the ledger, you can either manually delete the ledger directory or restart the validator with the `--reset` flag:

```shell
solana-test-validator --reset
```

If the ledger exists, this command will reset the ledger to genesis, which resets the state by deleting all existing accounts and starting fresh.

### Cloning Programs

To add existing onchain programs to your local environment, you can clone the program with a new ledger. This is useful for testing interactions with other programs that already exist on any other cluster.

To clone an account from another cluster:

```shell
solana-test-validator --clone PROGRAM_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO
```

To clone an upgradeable program and its executable data from another cluster:

```shell
solana-test-validator --clone-upgradeable-program PROGRAM_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO
```

> If a ledger already exists in your working directory, you must reset the ledger to be able to clone a program.

### Cloning Accounts

To add existing onchain accounts to your local environment, you can clone the account with a new ledger from any other network cluster.

To clone an account from the cluster when a ledger already exists:

```shell
solana-test-validator --clone ACCOUNT_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO --reset
```

### Reset to Specific Account Data

To reset the state of specific accounts every time you start the validator, you can use a combination of account snapshots and the `--account` flag.

First, save the desired state of an account as a JSON file:

```shell
solana account ACCOUNT_ADDRESS --output json > account_state.json
```

Then load this state each time you reset the validator:

```shell
solana-test-validator --reset --account ACCOUNT_ADDRESS account_state.json
```

### Runtime Features

Solana has a feature set mechanism that allows you to enable or disable certain blockchain features when running the test validator. By default, the test validator runs with all runtime features activated.

To see all the runtime features available and their statuses:

```shell
solana feature status
```

To query a specific runtime feature's status:

```shell
solana feature status <ADDRESS>
```

To activate a specific feature:

```shell
solana feature activate <FEATURE_KEYPAIR> <CLUSTER>
```

- `FEATURE_KEYPAIR` is the signer for the feature to activate
- `CLUSTER` is the cluster to activate the feature on

To deactivate specific features in genesis:

```shell
solana-test-validator --deactivate-feature <FEATURE_PUBKEY> --reset
```

This must be done on a fresh ledger, so if a ledger already exists in your working directory you must add the `--reset` flag to reset to genesis.

### Changing Versions

To check your current `solana-test-validator` version:

```shell
solana-test-validator --version
```

Your test validator runs on the same version as the Solana CLI installed and configured for use.

To test your programs against different versions of the Solana runtime, you can install multiple versions of the Solana CLI and switch between them using the following command:

```shell
solana-install init <VERSION>
```

Make sure to reset your Solana test validator's ledger after changing versions to ensure it runs a valid ledger without corruption.

## Solana.toml file configs

## Compute and Fees Section

you dont need to track gas but you can optimize compute.

// link to jonas's compute docs -> advanced section

Solana CLI Commands #
To view all CLI commands and see other ways to interact with the test validator:

solana --help

This command list all flags, options, and subcommands available.

Example Use Case #
Create a USDC Token Account on your localnet

Clone the USDC mint address to your local validator
solana-test-validator --clone EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v --url mainnet-beta --reset

Create a token account
spl-token create-account EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v --url localhost

// FIXME: Add in how to connect to test validator from the front end