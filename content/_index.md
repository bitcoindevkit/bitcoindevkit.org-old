+++
title = "Home"
template = "landing.html"
+++

## Welcome! below is an overview of the Bitcoin Dev Kit project's objectives, background, planned features and a very rough road map. If you have any questions or would like to get involved please send us a DM on twitter [@bitcoindevkit](https://twitter.com/bitcoindevkit).

### Objective

Create a secure and easy to use mobile cross platform (iOS/Android) Bitcoin wallet dev kit and example wallet app. 
Support integration and use by teams creating mobile bitcoin applications that require a bitcoin wallet such as 
multi-key vaults, mixing services, decentralized exchanges, privacy focused wallets, etc. Provide pluggable modules to 
support different options for accessing blockchain data (ie. BIP-157, Electrum, Core RPC), and for storing block and 
wallet data. As a long term goal also add pluggable modules for services such as coin selection, or alternative 
transports (ie. TOR, mesh wireless) and hardware security support. Ultimately this project should integrate with the 
LDK project to enable seamless on chain and off chain wallet features. 

### Background

This project grew out of a desire to build a mobile multi-sig wallet app. That app was originally based on the bitcoinj 
library but bitcoinj could not be used on iOS and was slow to adopt protocol improvements like Segwit. In searching for 
a suitable replacement we found the [rust-bitcoin](https://github.com/rust-bitcoin) suite of projects and the 
[defiads](https://github.com/defiads/defiads) project which together implement a functional bitcoin wallet. The author 
of defiads, Tamás Blummer, confirmed his vision was to also support a mobile wallet. The BDK project began by extracting 
the wallet related work from Tamás’ defiads project and creating mobile friendly wallet APIs and packaging for it. The 
team also saw a need to help maintain the related rust projects Tamás spearheaded and continue his work.

### Planned Features

1. Tested and signed release builds 
1. Good documentation and community support
1. Up-to-date with latest rust-bitcoin and other dependency versions
1. Feature parity between Android and iOS (hardware permitting)
1. Latest core wallet features ([rust-bitcoin](https://github.com/rust-bitcoin/rust-bitcoin), [rust-wallet](https://github.com/rust-bitcoin/rust-wallet))
   - mnemonic seeds
   - hd key derivation
   - segwit addresses
   - PSBT
   - RBF
1. Mobile cross platform with native language wrapper APIs
   - Android/Kotlin
   - iOS/Swift
1. Pluggable options for block data source and outbound tx peers
   - Light client bitcoin network peer (BIP157/158) ([murmel](https://github.com/rust-bitcoin/murmel))
   - Electrum ([rust-electrum-client](https://github.com/rust-bitcoin/murmel))
   - Local Core RPC ([rust-bitcoincore-rpc](https://github.com/rust-bitcoin/rust-bitcoincore-rpc))
   - Remote Core RPC via Tor ([Quick Connect QR](https://github.com/rust-bitcoin/rust-bitcoincore-rpc))
   - Alternative transports ([Low bandwidth](https://github.com/rust-bitcoin/rust-bitcoincore-rpc), Headers over DNS, etc.)
1. Eclipse mitigation
   - Configurable block data source diversity
   - Configurable outbound peer diversity
   - Configurable stale tip detection, new peer selection
1. Pluggable options for wallet and seed data storage
   - Local SQLite
   - Local Flat file
   - Cloud Encrypted flat file (Backup)
1. Configurable wallet data storage diversity (for backups)
1. Configurable wallet derivation paths
1. Plugable coin selection: manual, branch and bound
1. Miniscript / descriptor support ([magical-bitcoin-wallet](https://github.com/rust-bitcoin/rust-bitcoincore-rpc))
1. Payjoin support
1. Integrated TOR proxy
1. LDK integration ([rust-lightning](https://github.com/rust-bitcoin/rust-lightning))
1. Hardware security support
   - Secure enclave key storage and signing
   - Hardware wallet / HWI 
   - HSM runtime support like the nShield
1. Taproot/Schnorr

### Road map

#### 20.Q2 - Android POC
1. POC bdk-android, Testnet
1. Functional Android/Java API Lib (AAR) and example Android wallet app
1. Simple website and documentation
1. Solicit and onboard community devs

#### 20.Q3 - Android API
1. v0.1.0 bdk-android, Testnet
1. Finalize initial Android/Java APIs
1. Block source: bip157/158 (murmel)
1. Block store: hammersbald (or SQLite?)
1. Wallet store: SQLite
1. Improve test coverage, also on murmel and hammersbald
1. Documentation and community outreach
1. Onboard part-time sponsored dev

#### 20.Q4 - iOS POC + Android Pipeline 
1. v0.2.0 bdk-android, POC iOS, Testnet
1. Fix critical bugs, including in dependency projects 
1. Automate CI pipeline, creating and deploying signed AAR builds
1. Basic iOS example wallet app
1. PSBT and RBF APIs

#### 21.Q1 - iOS API
1. v0.3.0 bdk-android, v0.1.0 bdk-ios, Testnet
1. Finalize initial iOS/Swift APIs
1. Block source: add electrum client
1. Update Android API and example wallet app to support electrum client
1. Documentation and community outreach
1. Onboard part-time sponsored dev
1. HWI APIs

#### 21.Q2 - iOS Pipeline, Coin Selection

#### 21.Q3 - Miniscript, Descriptors

#### 21.Q4 - Payjoin, TOR

#### 22. - Mainnet, Secure Enclave Signing

#### 23. - LDK integration
