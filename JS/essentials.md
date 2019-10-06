
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

# Deploy Contract

# Call a function 
