# How to communication the Ledger Nano S in Mac OS
This tutorial contains how to communicate with Ledger  Nano S. I use Ledger Nano S hardware on Firmware version 1.55, Python / PIP to communicate Ledger Nano S in a Virtual Environment in your native environment (not a Docker image).

## Steps Configuring the Ledger SDK and Toolchain
1. Make folder project
```bash
$ mkdir /Users/"YourUsername"/ledger-nano-s
```
2. Set an environmental variable BOLOS_ENV
```bash
$ cd ledger-nano-s/
$ pwd                   # /Users/"YourUsername"/ledger-nano-s
$ export BOLOS_ENV="/Users/YourUsername/ledger-nano-s"
```
3. Download a prebuilt gcc for Mac OS [here](https://launchpad.net/gcc-arm-embedded/5.0/5-2016-q1-update/+download/gcc-arm-none-eabi-5_3-2016q1-20160330-mac.tar.bz2) and unpack this into the /ledger-nano-s/ folder using the command
```bash
$ tar –xjf ~/Donwloads/gcc-arm-none-eabi-5_3–2016q1–20160330-mac.tar.bz2 /Users/"YourUsername"/ledger-nano-s
```
4. Download a prebuild clang for Mac OS [here](http://releases.llvm.org/download.html#4.0.0) and unpack it using
```bash
$ tar –xf ~/Downloads/clang+llvm-4.0.0-x86_64-apple-darwin.tar.xz /Users/"YourUsername"/ledger-nano-s
```
5. Rename the directory "clang+llvm-4.0.0-x86_64-apple-darwin" that was inside to "clang-arm-fropi"
```bash
$ mv clang+llvm-4.0.0-x86_64-apple-darwin clang-arm-fropi
```
6. Navigate to /Users/"YourUsername"/ledger-nano-s
```bash
$ cd /Users/"YourUsername"/ledger-nano-s
```
7. Clone the Nano S SDK
```bash
$ git clone https://github.com/LedgerHQ/nanos-secure-sdk
```
8. Ensure you have the correct version for your Ledger Firmware Checked out. I use Firmware version 1.55, but we can check using
```bash
$ git tag –l
```
9. And then making sure we’re on the correct tag by using
```bash
$ git checkout nanos-1553
```
10. Add another environmental variable "BOLOS_SDK" that links to this folder
```bash
$ export BOLOS_SDK="$BOLOS_ENV/nanos-secure-sdk"
```

## Steps Configuring the Python Loader (blue-loader-python)
1. Clone the repository into the /Users/"YourUsername"/ledger-nano-s folder
```bash
$ git clone https://github.com/LedgerHQ/blue-loader-python.git
```
2. I will assume you do not have virtualenv installed, so at this point use the command
```bash
$ pip3 install virtualenv
```
3. And follow any prompts necessary to install this. Then we will run
```bash
$ virtualenv ledger
$ source ledger/bin/activate
$ pip install ledgerblue
```

This will configure a one-time virtual environment in python for loading to the ledger.

## How to use
- Delete App
```bash
$ python -m ledgerblue.deleteApp — targetId <TARGET_ID> — appName <APP_NAME>
```
- Install App
```bash
$ python -m ledgerblue.loadApp --targetId <TARGET_ID> — appName <APP_NAME>
```

## Target ID
- 0x31100002 on Nano S with firmware <= 1.3.1
- 0x31100003 on Nano S with firmware 1.4.x
- 0x31100004 on Nano S with firmware 1.5.x
- 0x31000002 on Blue with firmware <= 2.0
- 0x31000004 on Blue with firmware 2.1.x
- 0x31010004 on Blue v2 with firmware 2.1.x
- 0x33000004 on Nano X with firmware 1.x
