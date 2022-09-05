# Welcome to DevPath - Walks through the Docs

## Episode 1 - Getting Started with Scrypto!

What is Scrypto?

"Scrypto is the open source smart contract language of the Radix Network." They say it pretty clearly themselves right here at the top of the docs https://docs.radixdlt.com/main/scrypto/introduction.html

What will you learn?

How to:

1. Install Scrypto
2. Set up your development environment
3. Set up and run the Radix Engine Simulator `resim`
4. Build and deploy a hello world blueprint package
5. Instantiate a Component from the blueprint
6. Interact with it via the `resim` CLI tool

## Quick Start -> Install Scrypto - STEP 1

Follow the install instructions steps 1-3 for your operating system.

> **_NOTE!_** `We will cover step 4 below after IDE setup.`

https://docs.radixdlt.com/main/scrypto/getting-started/install-scrypto.html

### Setting Up VS Code as your IDE - STEP 2

There are detailed instructions in the link below.

- Install [VSCode](https://code.visualstudio.com/)
- Install `rust-analyzer` vscode extension
- Install `Radix Transaction Manifest Support` vscode extension
  https://docs.radixdlt.com/main/scrypto/getting-started/setting-up-vscode.html

### Setting up Radix Engine Simulator `resim` - STEP 3

The first command clones the git repository which contains the simulator along with example blueprints and more. All we really need right now is the simulator which the third command is installing with **Cargo** which is the **Rust Package Manager**

```
git clone https://github.com/radixdlt/radixdlt-scrypto.git
cd radixdlt-scrypto
cargo install --path ./simulator
```

### Build and Deploy a Blueprint Package - STEP 4

Either open an new terminal at the project root or `cd ..` to navigate back out of radixdlt-scrypto from step 3.

> #### Step 4.1 - Create a New Bluprint Package
>
> First we will use the Scrypto CLI tool to generate a basic project to get started by running

`scrypto new-package tutorial`

This will create a new directory names tutorial with a Hello blueprint package. You can open tutorial>src>lib.rs to inspect your new blueprint!

> #### Step 4.2 - Create a new Account
>
> Now that we have a bluprint package we need an account that we can use to deploy it. We Can create a new account using the resim CLI tool by running.

`resim new-account`

You should get a success message containing an Account Component Address, Public Key, and Private Key that looks something like this:

```
A new account has been created!
Account component address: account_sim1q0r85g5hyuudv57jeyqrts2u5py6mkr8tzccc8vm0hsq6pkemt
Public key: 0217161655220fa4f68fb78584b87cc8fda2c2332a5eb25ce65b21cbc2fc6b529a
Private key: f7d6ff476d2da934343b24def7ef64e7b70c61c9199c9d43ced7bd486703d748
No configuration found on system. will use the above account as default.
```

To make interacting with our bluprint from the simulator easier we can store these account credentials in a local variable by running

```
export account=account_sim1q0r85g5hyuudv57jeyqrts2u5py6mkr8tzccc8vm0hsq6pkemt
export pubkey=0217161655220fa4f68fb78584b87cc8fda2c2332a5eb25ce65b21cbc2fc6b529a
export privkey=f7d6ff476d2da934343b24def7ef64e7b70c61c9199c9d43ced7bd486703d748
```

or

```
# Using the PowerShell
$account="account_sim1q0r85g5hyuudv57jeyqrts2u5py6mkr8tzccc8vm0hsq6pkemt"
$pubkey="0217161655220fa4f68fb78584b87cc8fda2c2332a5eb25ce65b21cbc2fc6b529a"
$privkey="f7d6ff476d2da934343b24def7ef64e7b70c61c9199c9d43ced7bd486703d748"
```

> **_NOTE!_** Be sure to replace the values with the values from your new-account success message

> #### Step 4.3 View Account and Deploy Blueprint Package

Now we can view our account data in the simulator by running

`resim show $account`

> **_NOTE!_** If you did not store the account varible, replace `$account` with the acount address.

### **Time to deploy!**

Make sure that you are in the tutorial directory and run

`resim publish .`

Once again let's store the package address in a variable

`export package=<package_address_returned_by_resim_publish>`

### Instantiate a Component from the blueprint - STEP 5

We can instantiate our Hello component using the simulator to call the instantiate_hello function from our blueprint.

`resim call-function $package Hello instantiate_hello`

As you can see we use resim pass it the "call-function" command with the $package address Blueprint Name and then function name that we wish to run

This should output some information about creation including our new component address

```
Transaction Status: SUCCESS
Transaction Fee: 1.004125 XRD burned, 0.05020625 XRD tipped to validators
Cost Units: 10000000 limit, 1004125 consumed, 0.000001 XRD per cost unit
Execution Time: 67 ms
Instructions:
├─ CallMethod { component_address: component_sim1qgqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqpqgyhcl2, method_name: "lock_fee", call_data: Struct(Decimal("10")) }
├─ CallFunction { package_address: package_sim1qxsh3hmhus47jwnva2wzndc706j3pygdv06cd2rqydeq0grjgh, blueprint_name: "Hello", method_name: "instantiate_hello", arg: Struct() }
└─ CallMethodWithAllResources { component_address: account_sim1q0r85g5hyuudv57jeyqrts2u5py6mkr8tzccc8vm0hsq6pkemt, method: "deposit_batch" }
Instruction Outputs:
├─ ()
├─ ComponentAddress("component_sim1qf2f2xe2rl3zy4cvl9pt90aj94ca8tz84w3sqfkzrsks9thtea")
└─ ()
Logs: 0
New Entities: 2
└─ Component: component_sim1qf2f2xe2rl3zy4cvl9pt90aj94ca8tz84w3sqfkzrsks9thtea
└─ Resource: resource_sim1qqc3ux4mxuh8y8a5whfsqfmfcpxmun63msrdgvkhpqdqkqv76m
```

Once again let's save out component address to a variable

`export component=<component_address_returned_by_resim_call_function>`

### Grand Finally Let's get our free Hello Token - STEP 6

We are now going to use the simulator to call our free_token method which will pull 1 token from the vault and put it into our user account

We can inspect any address with the command

`resim show <address>`

This will show us the data attached to that addess be it a user account, component etc.

to call our free token method run

`resim call-method $component free_token`

This should remove 1 token from the component vault and place it in the caller account.

#### The official docs Section for this step -> [here](https://docs.radixdlt.com/main/scrypto/getting-started/run-first-project.html)

There are additional details and explanations available in the official docs [here](https://docs.radixdlt.com/main/scrypto/getting-started/run-first-project.html)

###

### CLI Cheat Sheet

https://docs.radixdlt.com/main/scrypto/toolchain/cheat-sheet.html

#### Quick Start CLI Commands Reference

- Create a new account ` resim new-account`

- Show address info `resim show <address> `

- Change simulator default account `resim set-default-account <account_address> <account_private_key>`

- Publish blueprint package `resim publish <path_to_package_dir>`

- Call a function `resim call-function <package_address> <blueprint_name> <function> <args>`

- Call a method `resim call-method <component_address> <method> <args>`

- Reset the Simulator `resim reset`

## Additional Resources

### Main Radix Website

https://www.radixdlt.com/

### Radix Docs

https://docs.radixdlt.com/main/index.html

### Rust

https://www.rust-lang.org/tools/install

### DevPath

https://devpath.tech
