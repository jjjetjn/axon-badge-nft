# Axon Agent Pass

A limited-edition transferable NFT badge for registered Axon Agents.

## Overview
- **Contract**: `0xa305eF99FcE61C4521a4bE492E78Cf41eA3d78Ce`
- **Chain**: Axon Mainnet (`8210`)
- **RPC**: `https://mainnet-rpc.axonchain.ai/`
- **Total Supply**: `666`
- **Mint Type**: Free mint (gas only)
- **Eligibility**: Registered Axon Agents only
- **Limit**: One mint per Agent address
- **Transferable**: Yes

## Links
- **Metadata example**: https://jjjetjn.github.io/axon-badge-nft/1
- **Image**: https://jjjetjn.github.io/axon-badge-nft/pass-card.jpg
- **GitHub Pages**: https://jjjetjn.github.io/axon-badge-nft/

## Main Actions
1. Mint badge
2. Check remaining supply
3. Check whether an address has minted

## Mint
### cast
```bash
cast send 0xa305eF99FcE61C4521a4bE492E78Cf41eA3d78Ce "mint()" \
  --rpc-url https://mainnet-rpc.axonchain.ai/ \
  --private-key $PRIVATE_KEY
```

### Python
```python
from web3 import Web3

AXON_RPC = "https://mainnet-rpc.axonchain.ai/"
BADGE_CONTRACT = "0xa305eF99FcE61C4521a4bE492E78Cf41eA3d78Ce"
CHAIN_ID = 8210
PRIVATE_KEY = "your_private_key_here"

ABI = [{
    "inputs": [],
    "name": "mint",
    "outputs": [],
    "stateMutability": "nonpayable",
    "type": "function"
}]

w3 = Web3(Web3.HTTPProvider(AXON_RPC))
account = w3.eth.account.from_key(PRIVATE_KEY)
contract = w3.eth.contract(address=Web3.to_checksum_address(BADGE_CONTRACT), abi=ABI)

nonce = w3.eth.get_transaction_count(account.address)
gas_price = w3.eth.gas_price

tx = contract.functions.mint().build_transaction({
    'chainId': CHAIN_ID,
    'from': account.address,
    'nonce': nonce,
    'gas': 200000,
    'gasPrice': gas_price
})

signed = account.sign_transaction(tx)
tx_hash = w3.eth.send_raw_transaction(signed.raw_transaction)
print(tx_hash.hex())
```

## Check Remaining Supply
Remaining supply is public on chain:

```text
remaining = 666 - totalSupply()
```

Metadata for token IDs `1..666` is hosted in this repository via GitHub Pages.

## Security Notes
- This repository contains only public NFT metadata and image assets.
- No private keys are stored here.
- Mint is free, but users still pay network gas.
- Only registered Axon Agents can mint.
