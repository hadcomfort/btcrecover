# Basic Password/Passphrase Recoveries

The idea is that, if you are running this tool on Windows, you can directly copy/paste any of these examples. (They all use the same seeds and addresses that are in the automatic tests)

They will all find a result almost straight away.

## Seed Based Recovery Notes
**Notes**
Seedrecover.py has been set up so that the defaults should get a result for the majorty of simple "invalid menmonic" or "invalid seed" type errors. (Eg: Where you have an intact seed backup that has a typo in it)

It will search all account types for the supported cryptocurrencies, on all common derivation paths.

It will automatically run through four search phases that should take a few hours at most.
1. Single typo
2. Two typos, including one where you might have a completely different BIP39 word
3. Three typos, including one where you might have a completely different BIP39 word
4. Two typos that could be completely different words.

**Fully Supported wallets** (For supported cryptocurrencies)

* Hardware Wallets
    * Ledger Nano X and S
    * Trezor One and T
    * Keepkey
    * Safepal
    * Coldcard
    * Bitbox02
    * Keystone
    * Cobo Vault
    * Ellipal
    * CoolWallet S (You will need both convert the seed numbers to BIP39 seed words and to use the --force-p2sh argument for Bitcoin and Litecoin...)
* Software Wallets
    * Electrum - Both V1 and V2 Seeds (This includes forks like Electrum-LTC, Electron-Cash, etc)
    * Coinomi
    * Wasabi
    * Edge Wallet
    * Mycelium
    * Exodus
    * Trust Wallet
    * Metamask (Including clones like Binance Chain Wallet Extension)

**Wallets with Compatibility Issues**(Due to not following derivation standards...)

* Atomic Wallet. (Non-Standard derivation for ETH (And all ERC20 tokens), needs to be used with the `--checksinglexpubaddress`, XRP)
* Abra Wallet. (Non-Standard seed format, first word is Non-BIP39 "at", the last 12 are BIP39 (and checksum) but unable to reproduce derivation)

## Examples
### Basic Bitoin Recoveries
**Note:** Most of the time you can just run seedrecover.py, even simply double click it and follow the graphical interface.

With a Native Segwit Address - One missing word, address generation limit of 5. (So address needs to be in the first 5 addresses in that account)
```
python seedrecover.py --wallet-type bip39 --addrs bc1qv87qf7prhjf2ld8vgm7l0mj59jggm6ae5jdkx2 --mnemonic "element entire sniff tired miracle solve shadow scatter hello never tank side sight isolate sister uniform advice pen praise soap lizard festival connect" --addr-limit 5
```

With a P2SH Segwit Address - One missing word, address generation limit of 5. (So address needs to be in the first 5 addresses in that account)
```
python seedrecover.py --wallet-type bip39 --addrs 3NiRFNztVLMZF21gx6eE1nL3Q57GMGuunG --mnemonic "element entire sniff tired miracle solve shadow scatter hello never tank side sight isolate sister uniform advice pen praise soap lizard festival connect" --addr-limit 5
```
### Basic Cardano Recoveries
For Cardano recovers, [see the notes here as well.](bip39-accounts-and-altcoins.md) You can use any Shelley-Era base or stake addresses. (Byron-Era not supported)

Seed from a Ledger Nano, missing one word, using a standard base address. (Address generation limit isn't appliable in Cardano)
```
python seedrecover.py --wallet-type cardano --addrs addr1qyr2c43g33hgwzyufdd6fztpvn5uq5lwc74j0kuqr7gdrq5dgrztddqtl8qhw93ay8r3g8kw67xs097u6gdspyfcrx5qfv739l --mnemonic "wood blame garbage one federal jaguar slogan movie thunder seed apology trigger spoon basket fine culture boil render special enforce dish middle antique"
```

Seed from a Trezor, missing one word, using a standard base address. (Address generation limit isn't appliable in Cardano)
```
python seedrecover.py --wallet-type cardano --addrs addr1q8k0u70k6sxkcl6x539k84ntldh32de47ac8tn4us9q7hufv7g4xxwuezu9q6xqnx7mr3ejhg0jdlczkyv3fs6p477fqxwz930 --mnemonic "ocean kidney famous rich season gloom husband spring convince attitude boy"
```

Seed from Yoroi, Adalite or Daedalus (Working as a software wallet), using a standard stake address
```
python seedrecover.py --wallet-type cardano --addrs stake1uxztdzzm4ljw9a0qmgregc8efgg56p2h3kj75kc6vmhfj2cyg0jmy --mnemonic "cave table seven there limit fat decorate middle gold ten battle trigger luggage demand"
```

### Basic Ethereum Validator Recoveries
Recovery for Ethereum Validator seeds is the same as a standard seed recovery, but uses the validators public key (Also known as Signing Key) in the place of an address.

Example command for a seed with one missing word
```
python seedrecover.py --mnemonic "spatial evolve range inform burst screen session kind clap goat force x" --addrs 869241e2743379b6aa5e01138d410851fb2e2f3923ccc19ca78e8b14b01d861f67f95e2e6b3be71a11b251680b42dd81 --wallet-type ethereumvalidator --addr-limit 1
```

### Basic Helium Recoveries
One missing word
```
python seedrecover.py --wallet-type helium --addrs 13hP2Vb1XVcMYrVNdwUW4pF3ZDj8CnET92zzUHqYp7DxxzVASbB --mnemonic "arm hundred female steel describe tip physical weapon peace write advice"
```

### Basic Polkadot(Substrate) Recoveries
One missing word, blank secret derivation path
```
python seedrecover.py --wallet-type polkadotsubstrate --addrs 13SsWBQSN6Se72PCaMa6huPXEosRNUXN3316yAycS6rpy3tK --mnemonic "toilet assume drama keen dust warrior stick quote palace imitate music disease"
```

One missing word, secret derivation path of "//hard/soft///btcr-test-password" The soft/hard derivation path is passed to the program via the --substrate-path argument and the password is treated the same as a passphrase (Without the leading ///)
```
python seedrecover.py --wallet-type polkadotsubstrate --addrs 12uMBgecqfkHTYZE4GFRx847CwR7sfs2bTdPbPLpzeMDGFwC --mnemonic "toilet assume drama keen dust warrior stick quote palace imitate music disease" --passphrase-arg btcr-test-password --substrate-path //hard/soft
```

### Basic Stacks Recoveries
One missing word, address generation limit of 10. (So will check the first 10 "accounts" for a given seed)
```
python seedrecover.py --wallet-type stacks --addrs SP11KHP08F4KQ06MWESBY48VMXRBK5NB0FSCRP779 --mnemonic "hidden kidney famous rich season gloom husband spring convince attitude boy" --addr-limit 10
```

### Basic Tron Recoveries
One missing word, address generation limit of 1. (So address needs to be in the first account)
```
python seedrecover.py --wallet-type tron --addrs TLxkYzNpMCEz5KThVuZzoyjde1UfsJKof6 --mnemonic "have hint welcome skate cinnamon rabbit cable payment gift uncover column duck scissors wedding decorate under marine hurry scrub rapid change roast print arch" --addr-limit 1
```

### Basic Elrond Recoveries
One missing word, address generation limit of 2. (So address needs to be in the first account)
```
python seedrecover.py --wallet-type elrond --addrs erd16jn439kmwgqj9j0xjnwk2swg0p7j2jrnvpp4p7htc7wypnx27ttqe9l98m --mnemonic "agree process hard hello artefact govern obtain wedding become robust fish bar alcohol about speak unveil mind bike shift latin pole base ugly artefact" --addr-limit 2
```

### Basic Electrum Legacy Recoveries
One wrong word, address generation limit of 2. (So address needs to be in the first account)
```
python seedrecover.py --wallet-type electrum1 --addrs 1Pw1yjF5smzg6eWbE2LbFm7fr1zq7WUYc7 --mnemonic "milk hungry group sound Lift Connect throw rabbit gift leg new lady pie government swear flat dove imagination sometime prepare lot trembl alone bus" --addr-limit 2
```

### Basic Stellar(XLM) Recoveries
One wrong word, address generation limit of two.
```
python seedrecover.py --mnemonic "doctor giant eternal huge improve suit service poem logic dynamic crane summer exhibit describe later suit dignity ahead unknown fall syrup mirror nurse" --addrs GAV7E2PHIPDS3PM3BWN6DIHC623ONTZUDGXPJ7TT3EREYJRLTMENCK6Z --addr-limit 2 --no-eta --wallet-type xlm
```

## SLIP39 Share Recovery
`seedrecover.py` can also help fix a damaged SLIP39 share. Supply your best guess of the share and allow the tool to search for close matches.

```
python seedrecover.py --slip39 --mnemonic "hearing echo academic acid deny bracelet playoff exact fancy various evidence standard adjust muscle parcel sled crucial amazing mansion losing" --typos 2
```

The tool can also recover shares with missing words. For example, omitting the last
word of the same share still succeeds:

```
python seedrecover.py --slip39 --mnemonic "hearing echo academic acid deny bracelet playoff exact fancy various evidence standard adjust muscle parcel sled crucial amazing mansion" --big-typos 2
```

If the share is longer than twenty-eight words, `seedrecover.py` assumes it is a
thirty-three word share. You can override this by supplying
`--share-length WORDS`.