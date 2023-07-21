# Intercoin Wallet
It's a secure wallet -- and you don't have to install it!

## Advantages:

1. 🚀 **Nothing to install.** Users can seamlessly start to use Web3 upon visiting a site.
2. ⛽ **No gas needed.** The wallet can sign meta-transactions, allowing the website operator to pay gas. 
3. 📜 **Standards-compliant.** The wallet is designed to work with with the new Account Abstraction standard ([ERC 4337]([url](https://eips.ethereum.org/EIPS/eip-4337)))
4. 🔍 **Transparency.** The user is shown the contract, method and parameters for a transaction, before approving it ([EIP 712]([url](https://eips.ethereum.org/EIPS/eip-712)) and [EIP 6384]([url](https://ethereum-magicians.org/t/eip-6384-readable-eip-712-signatures/12752/28)))
5. 🔒 **Extra Security.** The wallet maintains a managed whitelist of trusted smart contracts for each website, protecting users in case the site is compromised. It can also require the user to scan a QR code from another device to double-check and approve their transaction.

In addition, the wallet natively integrates a growing number of [applications developed by Intercoin](https://intercoin.org/applications) and audited by third parties, that lets people participate in, and manage, various community activities across websites:
:
1. 🌐 **[Community DAO](https://community.intercoin.app/t/intercoin-defi-communitycontract)** – inviting people, managing roles and permissions. ([GitHub](https://github.com/Intercoin/CommunityContract))
2. 🎨 **[NFTs](https://community.intercoin.app/t/intercoins-nft-smart-contract-released-audited)** -- connect with artists to release your own collection, memberships ([GitHub](https://github.com/Intercoin/NonFungibleTokenContract/tree/main_hardhat))
3. 💱 **[Currencies](https://intercoin.org/communities.pdf)** – issue and manage your own local money supply ([GitHub](https://github.com/Intercoin/UtilityTokenContract))
4. 🔄 **[Subscriptions](https://github.com/Intercoin/SubcriptionContract)** – manages recurring subscriptions to maintain some benefits ([GitHub](https://github.com/Intercoin/SubcriptionContract))
5. 💸 **[Income](https://github.com/Intercoin/IncomeContract)** – managing disbursements, including [Universal Basic Income](https://community.intercoin.app/t/rolling-out-voluntary-basic-income-in-communities) ([GitHub](https://github.com/Intercoin/IncomeContract))
6. 📊 **[Stats](https://github.com/Intercoin/StatsContract)** – understand how money is being spent from consumer price activity ([GitHub](https://github.com/Intercoin/StatsContract))
7. 🏆 **[Contests](https://community.intercoin.app/t/intercoin-defi-contestcontract)** – elect judges and reward teams for solving community problems ([GitHub](https://github.com/Intercoin/ContestContract))
8. 🌱 **[Fundraising](https://community.intercoin.app/t/how-intercoin-helps-to-raise-money-for-your-project)** - raising money with multiple rounds and bonus structures ([GitHub](https://github.com/Intercoin/FundContract))
9. 🔨 **[Auctions](https://github.com/Intercoin/AuctionContract)** - have buyers compete on price for NFTs, roles, reservations, etc. ([GitHub](https://github.com/Intercoin/AuctionContract))
10. 💰 **[Escrow](https://community.intercoin.app/t/intercoin-defi-escrowcontract)** – off-chain transactions and alternatives for reputation and trust ([GitHub](https://github.com/Intercoin/EscrowContract))
11. 🤝 **[Control](https://github.com/Intercoin/ControlContract)** – let multiple parties collectively manage an account and its actions ([GitHub](https://github.com/Intercoin/ControlContract))
12. 🗳️ **[Voting](https://community.intercoin.app/t/intercoin-defi-votingcontract-and-governance)** – secure elections to democratically govern your community ([GitHub](https://github.com/Intercoin/VotingContract))

## Other Crypto Wallets Today

The way crypto wallet browser extensions store the user's private keys is actually by encrypting them at runtime in Javascript (using material derived from the user's password), and storing the encrypted version in the browser's local storage. Then they load the keys into their Javascript execution environment and use it to sign the transactions. Wallets deployed as apps do a similar thing, except the code might not be in a browser extension. 

An exception is the ["Fortmatic/Magic wallet"](https://medium.com/fortmatic/security-infrastructure-at-fortmatic-4a95c3688997) and [related wallets](https://cointelegraph.com/news/new-wallet-uses-amazon-hardware-security-modules-to-eliminate-seed-words) which use [Amazon Key Management Service](https://aws.amazon.com/kms/) so users basically trust Amazon.

## Intercoin Wallet Security Foundations

The Intercoin wallet don't rely on Amazon and won't require a browser extension or an app, but will work inside iframes. It leverages [subresource integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) and [service workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) to ensure that the client-side code hasn't changed, and exactly matches what's been audited by third parties, and doesn't "phone home" any private information to any server.

Authentication in the Intercoin Wallet is done by means of [WebAuthn]([url](https://webauthn.guide/)) (you can see a [demo of how it works]([url](https://webauthn.io/)) in your own browser). The keys are stored inside a [U2F device](https://en.wikipedia.org/wiki/Universal_2nd_Factor) or -- these days very often -- in a [secure enclave](https://en.wikipedia.org/wiki/Trusted_execution_environment) inside the computer or phone on which the browser is running.

The challenge comes from the blockchain, with the material being derived from a [pseudo-random oracle]([url](https://ethereum.stackexchange.com/questions/191/how-can-i-securely-generate-a-random-number-in-my-smart-contract)https://ethereum.stackexchange.com/questions/191/how-can-i-securely-generate-a-random-number-in-my-smart-contract) that is infeasible to predict. The user signs the challenge using either WebAuthn or a [Web Crypto]([url](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto)https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto) using a non-extractable key. For now, most operating systems and hardware modules only support the secp256r1 elliptic curve, instead of the secp256k1 used in Bitcoin and Ethereum.

_(Some prominent people in the crypto space, including Vitalik Buterin, believe that the r1 curve was chosen because it has a weakness that can be exploited by state actors. However, it is used in all major security implementations outside crypto, including TLS, DNSSEC, Apple’s Secure Enclave, Passkeys, Android Keystore, and Yubikey, which can be used in the EVM.)_
