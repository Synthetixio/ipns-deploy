# @synthetixio/ipns-deploy

`ipns-deploy` is a command-line utility for publishing IPFS content identifiers (CIDs) to IPNS keys. It is designed to work in conjunction with `ipfs-deploy`, which uploads files and returns the corresponding CID.

By using `ipns-deploy` together with `ipfs-deploy`, you can publish your uploaded files' CID to an IPNS key, making it easier to manage and share your content on IPFS.

## Install

```sh
npm install -g @synthetixio/ipns-deploy
```

## ENV

Configure the environment variables with your IPFS cluster credentials and settings.

```sh
IPFS_HOST=ipfs.synthetix.io
IPFS_PORT=443
IPFS_PROTOCOL=https
IPFS_USER=
IPFS_PASS=
```

## CLI

Usage and examples

```sh
# Publish a CID to an IPNS key
# Usage: ipns-deploy KEY CID

# Example: Publish the CID obtained from ipfs-deploy to the 'staking.synthetix.eth' IPNS key
ipns-deploy "staking.synthetix.eth" QmAbCdEf1234567890

# Publish a CID obtained from an `ipfs-deploy` execution to the 'staking.synthetix.eth' IPNS key
export IPFS_CID=$(ipfs-deploy ./public)
ipns-deploy "staking.synthetix.eth" "$IPFS_CID"

# DEBUG mode to view additional information
DEBUG=ipns-deploy ipns-deploy "staking.synthetix.eth" QmXyZaBc1234567890
```

## IPNS Keys management

If the IPNS key was not added to the IPFS server it needs to be added first.

_NOTE_: This needs to be executed on the remote IPFS Cluster server

1. Generate new key

   ```sh
   ipfs key gen --type=rsa --size=2048 staking.synthetix.eth
   # This returns the key ID (IPNS name)
   # k2k4r8jvf8qlg4ytq7y3ta749vkjzms0hisd9i92ohk0lsp0yestbhy3
   ```

2. Check all the keys added

   ```sh
   ipfs key list -l
   # ...
   # k2k4r8jvf8qlg4ytq7y3ta749vkjzms0hisd9i92ohk0lsp0yestbhy3       staking.synthetix.eth
   ```

3. Check the IPNS URL can be resolved

   ```sh
   curl http://k2k4r8jvf8qlg4ytq7y3ta749vkjzms0hisd9i92ohk0lsp0yestbhy3.ipns.localhost:8080/
   ```
