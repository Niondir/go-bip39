![The bip39 library for Go](assets/images/banner.png)

[![PkgGoDev](https://pkg.go.dev/badge/tyler-smith/go-bip39)](https://pkg.go.dev/github.com/tyler-smith/go-bip39)
[![Latest release](https://img.shields.io/github/v/tag/tyler-smith/go-bip39?label=release&sort=semver)](https://github.com/tyler-smith/go-bip39/releases)
[![MIT License](https://img.shields.io/github/license/tyler-smith/go-bip39.svg?maxAge=2592000&color=blue)](https://github.com/tyler-smith/go-bip39/blob/master/LICENSE)
[![Contributors](https://img.shields.io/github/contributors/tyler-smith/go-bip39.svg?color=blue)](https://github.com/tyler-smith/go-bip39/graphs/contributors)

[![Build check](https://github.com/tyler-smith/go-bip39/workflows/build-check/badge.svg?branch=master)](https://github.com/tyler-smith/go-bip39/actions?query=workflow%3Abuild-check+branch%3Amaster)
[![Go Report Card](https://goreportcard.com/badge/github.com/tyler-smith/go-bip39)](https://goreportcard.com/report/github.com/tyler-smith/go-bip39)
[![Coverage Status](https://coveralls.io/repos/github/tyler-smith/go-bip39/badge.svg?branch=master)](https://coveralls.io/github/tyler-smith/go-bip39?branch=master)

This fork contains additional encryption methods to encrypt an existing mnemonic with a passwort to get a new encrypted mnemonic that is worthless without the password. But no observer could tell what the real wallet is.

BIP39 standard already allows you to create a seed from a mnemonic plus password. But that means, that you can not protect a mnemonic from an existing wallet (e.g. a mnemonic without password from a Trezor) with plausibel deniability.

## Example

```go
package main

import (
  "fmt"
  "github.com/tyler-smith/go-bip39"
  "github.com/tyler-smith/go-bip32"
)

func main(){
  // Generate a mnemonic for memorization or user-friendly seeds
  entropy, _ := bip39.NewEntropy(256)
  mnemonic, _ := bip39.NewMnemonic(entropy)

  // Generate a Bip32 HD wallet for the mnemonic and a user supplied password
  seed := bip39.NewSeed(mnemonic, "Secret Passphrase")

  masterKey, _ := bip32.NewMasterKey(seed)
  publicKey := masterKey.PublicKey()

  // Display mnemonic and keys
  fmt.Println("Mnemonic: ", mnemonic)
  fmt.Println("Master private key: ", masterKey)
  fmt.Println("Master public key: ", publicKey)
}
```
