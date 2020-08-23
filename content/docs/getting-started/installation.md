+++
title = "Installation"
weight = 2
template = "docs-page.html"
+++

## Bitcoin Development Kit

This library combines rust-bitcoin, murmel, and rust-wallet libraries to provide basic functionality for interacting with the 
bitcoin network. The library can be used in an android mobile app by including the optional jni module.

<br />

## Setup and Build

### 1. Install Rustup
[Install Link](https://www.rust-lang.org/learn/get-started)  
<br />

### 2. Install rust targets (if not already installed)
   
Android 
```sh
rustup target add x86_64-apple-darwin x86_64-unknown-linux-gnu x86_64-linux-android aarch64-linux-android armv7-linux-androideabi i686-linux-android
```

iOS
```sh
rustup target add aarch64-apple-ios armv7-apple-ios armv7s-apple-ios x86_64-apple-ios i386-apple-ios
```
<br />

### 3. Install cargo-ndk cargo extension

[cargo-ndk](https://docs.rs/crate/cargo-ndk/0.6.1)
   
#### Android
```sh
cargo install cargo-ndk
```

#### iOS
```sh
cargo install cargo-lipo
cargo install cbindgen
```
<br />

### 4. Install Android Studio and NDK
 
Open Android Studio -> Tools -> SDK Manager -> SDK Tools -> install "NDK (Side by side)"
<br />

### 5. Set environment variables

If not already set, set environment variables needed to build rust based library files and to run local unit tests. Better yet, add these to your `.bash_profile`.

#### Android (OSX)

```sh
export ANDROID_HOME=$HOME/Library/Android/sdk
export ANDROID_NDK_HOME=$ANDROID_HOME/ndk/<ndk version, eg. 21.0.6113669>
```

#### Android (Linux)

```sh
export ANDROID_HOME=$HOME/Android/Sdk
export ANDROID_NDK_HOME=$ANDROID_HOME/ndk/<ndk version, eg. 21.0.6113669>
```

#### iOS (OSX)

```sh
## if this fails:
xcrun -k --sdk iphoneos --show-sdk-path
## run this:
sudo xcode-select --switch /Applications/Xcode.app
```
<br />

### 6. Set environment variables needed to build Bitcoin C++ library files

This will be unnecessary after [fix](https://github.com/bbqsrc/cargo-ndk/pull/7) to [cargo-ndk](https://docs.rs/crate/cargo-ndk/0.6.1).

#### Android (OSX) 
```sh
export CXX_x86_64_linux_android=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/darwin-x86_64/bin/x86_64-linux-android30-clang++
export CXX_aarch64_linux_android=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/darwin-x86_64/bin/aarch64-linux-android30-clang++
export CXX_armv7_linux_androideabi=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/darwin-x86_64/bin/armv7a-linux-androideabi30-clang++
export CXX_i686_linux_android=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/darwin-x86_64/bin/i686-linux-android30-clang++
```

#### Android (Linux)
```sh
export CXX_x86_64_linux_android=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/linux-x86_64/bin/x86_64-linux-android30-clang++
export CXX_aarch64_linux_android=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android30-clang++
export CXX_armv7_linux_androideabi=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/linux-x86_64/bin/armv7a-linux-androideabi30-clang++
export CXX_i686_linux_android=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/linux-x86_64/bin/i686-linux-android30-clang++
```
<br />

### 7. Build Rust library files for all target platform OS architectures:

```sh
./build-lib.sh
```

<br />

## REGTEST Testing

The 🍣 [Nigiri CLI](https://github.com/vulpemventures/nigiri) tool can be used to spin-up a complete `regtest` 
development environment that includes a `bitcoin` node, a Blockstream `electrs` explorer and the 
[`esplora`](https://github.com/blockstream/esplora) web-app to visualize blocks and transactions in the browser.

First install [Docker-Desktop](https://www.docker.com/products/docker-desktop) on your machine. Then see the 
[Nigiri CLI README.md](https://github.com/vulpemventures/nigiri/blob/master/README.md) file to install via prebuilt binaries or from the 
 project source.
