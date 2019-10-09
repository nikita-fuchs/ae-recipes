
// everything in setup will be rendered as list of instructions. Other 1st-level topics will be generated to code, text will be comments.
# Setup

## [Install NodeJS](https://nodejs.org/en/download/)

## Install SDK
Install using npm / yarn / pnpm

```
npm i @aeternity/aepp-sdk
``` 

// whenever a topic has a member that starts with "options", display them as carousel, labeled with the options name.

### Options for operating systems:
Note : If you experience errors during the installation, you might need to install build tools for your OS.

#### Windows
Windows Build Tools
```
npm install -g windows-build-tools
```

//whenever there is a ```**SOME_VAR**``` placeholder in the code, take ```SOME_VAR```, define a variable with this name in the header of the generated code and assign them the corresponding values. TODO: Agree on naming for e.g. ```THE_CONTRACT_CODE```, ```THE_PARAMS```, ```THE_FUNCTION_NAME```

#### Ubuntu / Debian: Build Essential
```
sudo apt-get update
sudo apt-get install build-essential
```
#### Mac: 
Download Xcode from AppStore, then run

```
xcode-select --install
```

# Configuration of the SDK

Define an account you will use for transactions:

```
const acc1 = MemoryAccount({ keypair: { secretKey: 'bb9f0b01c8c9553cfbaf7ef81a50f977b1326801ebf7294d1c2cbccdedf27476e9bbf604e611b5460a3b3999e9771b6f60417d73ce7c5519e12f7e127a1225ca', publicKey: 'ak_2mwRmUeYmfuW93ti9HMSUJzCk1EYcQEfikVSzgo6k2VghsWhgU' } });
```
Setup the SDK instance and connect to the network through a node:

```

// account that will be used for the transactions 
// do NOT use this one on mainnet, you will lose your funds!

      

    const node1 = await Node({ url: 'https://sdk-testnet.aepps.com', internalUrl: 'https://sdk-testnet.aepps.com' })
        // const node2 = ...
      
    var Chain = await Ae({
       // This two params deprecated and will be remove in next major release
        url: 'https://sdk-testnet.aepps.com',
        internalUrl: 'https://sdk-testnet.aepps.com',
            // instead use
        nodes: [
              { name: 'someNode', instance: node1 },
              // node2, node3...
            ],
        compilerUrl: 'https://compiler.aepps.com',
            // \`keypair\` param deprecated and will be removed in next major release
           
        accounts: [
              acc1,
              // acc2
            ],
        address: 'ak_2mwRmUeYmfuW93ti9HMSUJzCk1EYcQEfikVSzgo6k2VghsWhgU'
        })
        const height = await Chain.height()
        console.log('Connected to Testned Node! Current Block:', height)
```

# Deploy a Contract



## contract code

// Contract code has to be explicitly written out and not be replaced by a placeholder, for the sake of readability of the doc. the heading that indicates upcomming contract code must read exactly: "contract code" and may at max contain one paragraph of text, followed by the contract code and nothing else - this is for the code generator's parsing, replacing the contract code here. //

First we define our contract code (watch out for the indentations ! Comments and other things will be stripped automatically further below)

```
var code = `
contract CryptoHamster =

    record state = {
        index : int, 
        map_hamsters : map(string, hamster), 
        testvalue: int}

    record hamster = {
        id : int,
        name : string,
        dna : int}

    stateful entrypoint init() = 
        { index = 1,
            map_hamsters = {},
            testvalue = 42}
    
    public entrypoint read_test_value() : int =
        state.testvalue
    
    public entrypoint return_caller() : address =
        Call.caller
`
```

## deployment
First we clean up the code to make sure escapes and comments are gone - all this will be done automatically by the SDK soon.
```
let formattedCode = code;

// replace " => \"
    formattedCode = formattedCode.replace(new RegExp('"', 'g'), '\"');
          


// remove comments
    formattedCode = formattedCode.replace(new RegExp('\\/\\/.*', 'g'), '');
    formattedCode = formattedCode.replace(new RegExp('\\/\\*.*[\s\S]*\\*\\/', 'g'), '');
```

# Call a function 
