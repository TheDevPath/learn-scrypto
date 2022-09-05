# Welcome to DevPath - Walks through the Docs

## Episode 1 - Getting Started with Scrypto!

What is Scrypto?

"Scrypto is the open source smart contract language of the Radix Network." They say it pretty clearly themselves right here at the top of the docs https://docs.radixdlt.com/main/scrypto/introduction.html

What will you learn?

How to:

- Install Scrypto
- Set up your development environment
- Set up and run the Radix Engine Simulator `resim`
- Build and deploy a hello world blueprint package
- Instantiate a Component from the blueprint
- Interact with it via the `resim` CLI tool

## Main Radix Website

https://www.radixdlt.com/

## Quick Start -> Install Scrypto - STEP 1

Follow the install instructions for your operating system @
https://docs.radixdlt.com/main/scrypto/getting-started/install-scrypto.html

### Radix Docs

https://docs.radixdlt.com/main/index.html

### Rust

https://www.rust-lang.org/tools/install

### Setting up Radix Engine Simulator `resim`

The first command clones the git repository which contains the simulator along with example blueprints and more. All we really need right now is the simulator which the third command is installing with **Cargo** which is the **Rust Package Manager**

```
git clone https://github.com/radixdlt/radixdlt-scrypto.git
cd radixdlt-scrypto
cargo install --path ./simulator
```

### CLI Cheat Sheet

https://docs.radixdlt.com/main/scrypto/toolchain/cheat-sheet.html

#### Quick Start CLI Commands Reference

- Create a new account ` resim new-account`

- Show address info `resim show <address> `

- Change simulator default account `resim set-default-account <account_address> <account_private_key>`

- Publish blueprint package `resim publish <path_to_package_dir>`

- Call a function `resim call-function <package_address> <blueprint_name> <function> <args>`

- Call a method `resim call-method <component_address> <method> <args>`
