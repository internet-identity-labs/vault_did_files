# vault_did_files
This repo hosts the required .did files to view information on deployed NFID Vaults.

## What is NFID Vaults?
NFID Vaults (https://nfidvaults.com) is an omni-chain smart wallet protocol for protecting personal and shared digital assets from any form of loss. Each NFID Vault is a canister that controls itself (so that it can be upgraded by you as the core team deploys new wasm upgrades, or as community members build their own versions).

## How can I verify the amount NFID Vault wallets store?

### Get a list of all vault canisters from the NFID Vault protocol canister
1. Navigate to the [candid UI explorer](https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/)
2. Enter the NFID Vault protocol canister ID (`z2cpg-maaaa-aaaal-adx2q-cai`) and `vault_manager.did` from this repo
3. Query the `get_all_canisters` function to get all canister_id principals

### Query wallet addresses from each vault canister
1. Navigate to the [candid UI explorer](https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/)
2. Enter the NFID Vault canister ID for the vault you want to query addresses for (from the previous step) and use the `vault.did` from this repo
3. Query the `get_state` function to find the UID for each of the `wallets`
4. Find the account_id for each wallet:
  `let subaccount = Subaccount(to_array(hex::decode(UID).unwrap()));`
  `let account_id = AccountIdentifier::new(canister_id, &subaccount).to_hex();`
5. Lookup the account_id on any block explorer (i.e. [Internet Computer Dashboard](https://dashboard.internetcomputer.org/))

## Dev FAQ
### Will vaults support other wallets?
Yes. We are working on completing the wallet standards in the wallet working group and releasing a package we've named [Identity Kit](https://docs.nfid.one/blog/standardizing-icp-wallet-and-identity-interaction-overview) that we intend to use in vaults. Any ICP wallet that conforms to ICP wallet standards and adds itself as a connector to the package will automatically be supported across the ICP ecosystem.
### Can I edit the controllers of my NFID Vault canister?
Yes.
### How do I top up my NFID Vault?
Check our [Knowledge base](https://learn.nfidvaults.com/top-up-smart-contract-canister) for the answer to this and other topics.
