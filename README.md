# The Toolkit Book

# Introduction

The Solana Toolkit consists of all open sourced tools for smart contract development on the Solana Blockchain.

You can contribute to this book on [GitHub]().

## Installation

To get started, install The Solana Toolkit.

```shell
npx solana install
```

This will install the latest versions of the following:

- [Solana CLI/ Agave Tool Suite](https://docs.solanalabs.com/cli/): A command line tool that allows developers to interact with the Solana blockchain, manage accounts, send transactions, and deploy programs.
- [Rust](https://doc.rust-lang.org/book/): The Programming language that Solana Smart Contracts are written in.
- [Anchor](https://www.anchor-lang.com/): A framework for writing solana programs that abstracts many complexities to speed up smart contract development.
- [Trident](): A fuzz tester
- [Zest](): A code coverage tool

## Getting Started

This section will cover all the toolkit basics to help you get started.

### Keypair generation

For a fresh installation of the [Solana CLI](https://docs.solanalabs.com/cli/), you're required to generate a new keypair.

```shell
solana-keygen new
```

Set the keypair path:

```shell
solana config set --keypair <path_to_keypair>
```

Check the pubkey of your machines newly generated keypair:

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

For a more information, read the [Solana Test Validator Guide](https://solana.com/developers/guides/getstarted/solana-test-validator).

# Projects

## Creating a New Project

To start a new project with the solana toolkit, pick a which scaffold you want to use. There are scaffolds for stand alone smart contract workspaces, web app workspaces, or mobile app workspaces.

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

The anchor framework abstracts away many complexities enabling fast program development.

For more information on the anchor framework, check out the [anchor book](https://www.anchor-lang.com/).

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

This command gives you the option to choose between Shank and Anchor for the program framework.

- **Shank** creates a vanilla Solana smart contract with Shank macros to generate IDLs

For more information on Shank, check out the [README](https://github.com/metaplex-foundation/shank).

- **Anchor** creates a smart contract using the anchor framework, which abstracts away many complexities enabling fast program development.

For more information on the anchor framework, check out the [anchor book](https://www.anchor-lang.com/).

This command also gives the option to choose between a JS client, a Rust Client, or both.

- **JavaScript Client** creates a typescript library compatible with web3.js.

- **Rust Client** creates a rust crate allowing consumers to interact with the smart contract.

For further workspace customization and additional information, check out the [README](https://github.com/solana-program/create-solana-program/tree/main).

### Web App Scaffold

```shell
npx create-solana-dapp
```

This command generates a new project that connects a solana smart contract to a front end with a wallet connector.

For additional information, check out the [README](https://github.com/solana-developers/create-solana-dapp).

To test out this project before making any modifications, follow these steps.

Build the smart contract:

```shell
npm run anchor-build
```

Start the local validator:

```shell
npm run anchor-localnet
```

Run tests:

```shell
npm run anchor-test
```

Deploy to the local validator:

```shell
npm run anchor deploy --provider.cluster localnet
```

Build Web App:

```shell
pnpm build
```

Run Web App:

```shell
pnpm dev
```

### Mobile App Templates

```shell
yarn create expo-app --template @solana-mobile/solana-mobile-expo-template
```

This is initializing a new project using the Expo framework that is specifically designed for creating mobile applications that interact with the Solana blockchain.

Follow the [Running the app](https://docs.solanamobile.com/react-native/expo#running-the-app) guide to launch the template as a custom development build and get it running on your Android emulator. Once you have built the program and are running a dev client with expo, the emulator will automatically update every time you save your code.

To use this, you will also need to set up the following:

- [Android Studio and Emulator](https://docs.solanamobile.com/getting-started/development-setup)
- [React Native](https://reactnative.dev/docs/environment-setup?platform=android)
- [EAS CLI and Account](https://docs.expo.dev/build/setup/)

For additional information on Solana Mobile Development: https://docs.solanamobile.com/getting-started/intro

## Smart Contract Layout

Typically Solana smart contract workspaces will be have the following file structure:

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

The Solana Tool Kit makes developing with existing projects have no overhead.

```shell
npm install
```

```shell
solana build
```

```shell
solana test
```

```shell
solana deploy --provider.cluster <localnet || devnet || mainnet || testnet>
```

## Verifiable Programs

## Dependencies??

# Solana Test Suite Overview

Within the toolkit, there are several resources for testing Solana Smart Contracts, including:

- A fuzzer
- A code coverage tool
- A step debugger????
- A framework for testing Solana programs in NodeJS that spins up a lightweight `BanksServer` that's like an RPC node but much faster and creates a `BanksClient` to talk to the server.
- A fast and lightweight library for testing Solana programs in Rust, which works by creating an in-process Solana VM optimized for program developers.
- A tool to scan your repo for common security vulnerabilities and provide suggestions for fixes.
- A reference guide of important cheat codes to simplify writing tests.

## Testing Basics

Sync all the program's key, if you're using an anchor program:

```shell
anchor keys sync
```

Build the smart contract:

```shell
solana build
```

Test the smart contract:

```shell
solana test
```

Deploy the smart contract:

```shell
solana deploy --provider.cluster <localnet || devnet || testnet || mainnet>
```

If deploying to mainnet, you must first start your local validator:

```shell
solana-test-validator
```

For more information on local validator customization and commands, read the [Solana Test Validator Guide](https://solana.com/developers/guides/getstarted/solana-test-validator).

## Fuzz Tester

Generate fuzz tests:

```shell
solana fuzz
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
solan fuzz run
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

## Code Coverage Tool

```shell
solana coverage
```

This command will run a code coverage test on all of your Rust tests and then generate report in an HTML page with in depth metrics on where additional code may be needed to improve your current code coverage.

Note: So far, this tool only works on tests written in Rust and is not compatible with a JS test suite.

View the source code [here](https://github.com/LimeChain/zest?tab=readme-ov-file).

## Step Debugger

## JS testing Framework

## Rust Testing Library

## Security Vulnerability Scanner

## Solana Cheat Codes

Most of the time, simply testing your smart contracts outputs isn’t enough. To manipulate the state of the blockchain, as well as test for specific reverts and events, you can use the

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

solana-test-validator

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

Since the solana-test-validator is part of the Solana CLI tool suite, ensure you have Solana's command-line tools installed. You can install them using the following command:

```shell
sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"
```

You can replace stable with the release tag matching the software version of your desired release (i.e. v1.18.12), or use one of the three symbolic channel names: stable, beta, or edge.

### Starting the Test Validator

To start your local validator, simply run:

```shell
solana-test-validator
```

This command initializes a new ledger and starts the validator.

### Interacting with a Running Test Validator

Once you have the solana-test-validator up and running, you can interact with it using various Solana CLI (Command Line Interface) commands. These commands let you deploy programs, manage accounts, send transactions, and much more. Here's a detailed guide on the key commands you will use.

### Checking the Status of the Test Validator

Before interacting with the test validator, it's useful to confirm its status and ensure it is running correctly.

```shell
solana ping
```

This command pings the local test validator and returns the current blockhash and latency, verifying that it is active.

### Account Management

To create a new keypair (account), use:

```shell
solana-keygen new
```

This command creates a new keypair and saves it to the specified file.

To add SOL to your account:

```shell
solana airdrop 10 <ACCOUNT_ADDRESS>
```

To retrieve details about an account, such as its balance and owner:

```shell
solana account <ACCOUNT_ADDRESS>
```

You must first airdrop funds to the account for the account to exist.

This command sends 10 SOL to the specified account address.

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

This sends AMOUNT of SOL from the source account to the RECIPIENT_ADDRESS.

### Simulating and Confirming Transactions

Before actually sending a transaction, you can simulate it to see if it would succeed:

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

### Useful Tips Logging:

Increase log verbosity with the -v flag if you need more detailed output for debugging.
Use the --rpc-port and --rpc-bind-address options to customize the RPC server settings.
Adjust the number of CPU cores used by the validator with the --gossip-host option to simulate network conditions more realistically.

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

By default, the ledger data is stored in a directory named test-ledger in your current working directory.

### Specifying Ledger Location

When starting the test validator, you can specify a different directory for the ledger data using the --ledger option:

```shell
solana-test-validator --ledger /path/to/custom/ledger
```

### Resetting the Ledger

By default the validator will resume an existing ledger. To reset the ledger, you can either manually delete the ledger directory or restart the validator with the --reset flag:

solana-test-validator --reset

If the ledger exists, this command will reset the ledger to genesis, which resets the state by deleting all existing data and starting fresh.

Runtime Features #
Solana has a feature set mechanism that allows you to enable or disable certain blockchain features when running the test validator. By default, the test validator runs with all runtime features activated.

To query the runtime feature status:

solana feature status <ADDRESS>

ADDRESS is the feature status to query [default: all known features]
To activate a specific feature:

solana feature activate <FEATURE_KEYPAIR> <CLUSTER>

FEATURE_KEYPAIR is the signer for the feature to activate
CLUSTER is the cluster to activate the feature on
To deactivate specific features in genesis:

solana-test-validator --deactivate-feature <FEATURE_PUBKEY> --reset

This must be done on a fresh ledger, so if a ledger already exists in your working directory you must add the --reset flag to reset to genesis.

Changing Versions #
To check your current solana-test-validator version:

solana-test-validator --version

Your solana-test-validator runs on the same version as the Solana CLI version.

To test your programs against different versions of the Solana runtime, you can install multiple versions of the Solana CLI and switch between them using the solana-install set command:

solana-install init <VERSION>

VERSION is the desired CLI version to install
Make sure to restart your Solana test validator after changing versions to ensure it runs the correct version.

Cloning Programs #
To add existing onchain programs to your local environment, you can clone the program with a new ledger.

To clone an account from the cluster:

solana-test-validator --clone PROGRAM_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO

This is useful for testing interactions with standard programs.

If a ledger already exists in your working directory, you must reset the ledger to be able to clone a program.

To clone an account from the cluster when a ledger already exists:

solana-test-validator --clone PROGRAM_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO --reset

To clone an upgradeable program and its executable data from the cluster:

solana-test-validator --clone-upgradeable-program PROGRAM_ADDRESS --url CLUSTER_PROGRAM_IS_DEPLOYED_TO

Resetting State on Accounts at Startup #
By default the validator will resume an existing ledger (if present). But during startup, you can reset the ledger either to genesis or to specific account state that you provide.

Reset to Genesis #
To reset the ledger to the genesis state:

solana-test-validator --reset

Reset to Specific Accounts #
To reset the state of specific accounts every time you start the validator, you can use a combination of account snapshots and the --account flag.

First, save the desired state of an account as a JSON file:

solana account PROGRAM_ADDRESS --output json > account_state.json

Then load this state each time you reset the validator:

solana-test-validator --reset --account PROGRAM_ADDRESS account_state.json

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

## Solana.toml file configs

## Compute and Fees Section

you dont need to track gas but you can optimize compute.

// link to jonas's compute docs -> advanced section
