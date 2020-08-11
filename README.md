# Beam Roadmap Draft

## Overview

From its launch on January 3rd 2019, Beam hasd released four major versions, each bringing a different set of features and improvements. 

The recent release of Eager Electron 5.0 marks a beginning of a new era in Beam development. What started as a best in class confidential and scalable cryptocurrency a little over two years ago, is now expanding to new and exciting product paths, a combination of both product and technology. We chose to call it Confidential DeFi and it will be an integral part of Beam Roadmap for the next year or more. In this article we will outline the rough draft of our Roadmap. Our goal is to discuss it both internally and with the community during the coming weeks and then release an official update. 

The roadmap can be roughly divided into three tracks: the Wallet track, the DeFi track and the Infrastructure track. On a timeline, it will span two major versions: Eager Electron 5.0, the current version and the Fierce Fermion 6.0, next major version that will require a hard fork to introduce new capabilities into the Beam node. 

## Wallet Track

### [5.1 (July - August, 2020)](https://github.com/BeamMW/roadmap/projects/1)

Eager Electron major version has started with the release of the 5.0 and the subsequent hard fork on July 28th 2020 that has activated Lelantus MW and Confidential Asset support in Beam nodes. It also changed the mining algorithm to BeamHash III, the last of the two planned PoW updates that Beam has announced at launch. As usual, each major version is followed by several minor ones, each delivering a set of features and enhancements that do not require a consensus change.

Work on the 5.1 version has started immediately after the release of 5.0. It is already in the testing phase and scheduled to be released in the upcoming weeks. This version includes several important features and improvements. 

#### [Max privacy](https://github.com/BeamMW/roadmap/issues/1)

Max Privacy transactions utilize the new Lelantus MW infrastructure that was added in the recent hard fork and the related 5.0 version. Each such transaction contains two parts. First, the Sender submits UTXOs into the shielded pool with a max anonymity set of 64K. Then, Receiver extracts a completely new set of UTXOs that are completely unlinked from the previous history from the pool and can use it for further transactions. The time between these two parts is important as it allows for a sufficient number of other UTXOs to accumulate in the pool and provide the required anonymity set. Beam CLI wallets allow users to perform these operations separately for maximum control. In UI wallets, this operation is seamless and is built into standard Send and Receive operations.

The specific window within which the anonymity set is maximal depends on the rate of Max Privacy transactions, the more they are used, the faster maximum anonymity is reached. This information is monitored and displayed by the wallet, so that  at any time the user can know the exact anonymity set of each UTXO. The manual control, however, is not required since the wallet automatically selects the best UTXOs for each transaction, including the ability to send LelantusMW and Mimblewimble UTXOs in a single transaction. 


#### [Offline payments](https://github.com/BeamMW/roadmap/issues/3)

Since Mimblewimble is inherently an interactive protocol, both the sender and the receiver need to participate in creation of the transaction. This introduces a very different user interface from what we are used to in other crypto currencies. However, using the LelantusMW technology, Beam has built an ability for senders to send funds non interactively even when the receiver is not online. We called this feature offline payments and it comes in two different flavors: using vouchers and using the offline address. 

First option, which will be released in 5.1, allows the user to embed a set of special keys called vouchers into an address created in the receive screen. By default, 20 vouchers are created. Since each voucher is about 100 symbols in length this number was chosen to allow the resulting address to be sent through most messengers without breaking into several messages. Each voucher is good for one transaction and when they expire, the wallet will either automatically request a new set from the receiver if it comes online, or prompt the user to ask for a new address with more tokens. The advantage of this, rather complicated, method is due to two properties. Each transaction uses a unique voucher, hence making it impossible to trace the user by trying to monitor which vouchers are used. Also, the sender can not track when funds that were sent using the voucher are spent, i.e extracted from the pool. Thus vouchers provide the maximum anonymity. 

The second option, that is currently planned for 5.2 version, uses a single ‘offline’ address, which allows to send any amount of offline transactions to the same address. Due to details of how LelantusMW pool works, there can only be a very limited (and definitely capped) number of such addresses created for each wallet since each new address would require the wallet to rescan the pool for UTXOs sent to it. This option is less secure since it allows deanonymization by comparing offline addresses sent out to different senders and also the sender can see when the funds are extracted from the pool. It is however much simpler for the user and more consistent with how most other crypto currencies work, which is why we recommend it for specific user cases like donations and non-interactive pool payouts, rather than general confidential transactions.



#### [Atomic Swap improvements](https://github.com/BeamMW/roadmap/issues/4)

Atomic Swaps are a great and completely confidential decentralized way to securely exchange Beams for BTC, LTC and QTUM without any third party. In this version this feature becomes even better with **replacing intermediate outputs and inputs with SegWit**, lowering the fees for the swap significantly. We also provide optimal fee rate recommendations directly from the respective blockchains thus removing the necessity to obtain them manually. 

#### [Redesigned settings](https://github.com/BeamMW/roadmap/issues/2)

As more features are added into the wallet the settings page gets more crowded, so we have decided to redesign it and create logical groups to simplify finding and accessing the relevant settings. 



### [5.2 (September - November, 2020)](https://github.com/BeamMW/roadmap/projects/2)


#### [Beam Vault and Secure Sync](https://github.com/BeamMW/roadmap/issues/5) 

Beam SBBS is a great decentralized encrypted messaging system that allows wallet to interactively create MW transactions. It is however limited by design to only hold the message for 12 hours after which the message will expire and is no longer available for the recipients. Beam Vault is a centralized but trustless service that can store SBBS messages for longer periods of time. It can also be used to synchronize Beam Wallet that uses the same seed across multiple devices, something that was previously problematic and hence discouraged. As SBBS will gain more function with addition of DeFi functionality this service will be even more useful as a complementary and backup option for the SBBS system.

#### [Address Book improvement](https://github.com/BeamMW/roadmap/issues/6)

The Address Book feature is not new. It appeared in all wallet versions from the very beginning. It was, however, hardly used as most transactions used ad hoc SBBS addresses and hence writing them down was irrelevant. In few cases where permanent addresses were used, they are usually related to either exchanges or pools. However, with the addition of offline payments and Confidential Assets, the address book takes on new roles and needs to be improved and updated.

#### [Trezor T support](https://github.com/BeamMW/roadmap/issues/7)

We are planning to roll out a custom firmware for Trezor T that supports Beam with integration into Beam Desktop Wallet. Ledger X development is more difficult and still in progress.

#### [Swaps with BSV, BCH, Dash and more](https://github.com/BeamMW/roadmap/issues/8)

More coins will be added to our Atomic Swap support, mostly BTC forks. These will include BCH, DASH and BSV. We are also looking at RVN and probably a few others.

#### [Beam Blockchain Explorer improvements](https://github.com/BeamMW/roadmap/issues/9)

Following the introduction of new features we need to reflect their state in the blockchain explorer and related APIs. These should include statistics for Atomic Swaps offered and accepted, The current state of the LelantusMW pool including estimated hold duration for achieving maximum anonymity set.

#### [Wallet UI for Confidential Assets](https://github.com/BeamMW/roadmap/issues/10)

Beam UI Wallets should be able to transact using any existing Confidential Asset, in addition to native Beam coins. Since CAs inherit all properties of Beam coins, it is possible to seamlessly mix different asset types within the same transaction. The challenge is to integrate this functionality into Beam UI in a way that would not negatively impact its usability, while still being able to support all relevant use cases for power users.

#### [Beam Web Wallet and Wallet Service Mainnet release](https://github.com/BeamMW/roadmap/issues/11) 

We have recently released the Testnet version of Beam Web Wallet and Wallet Service, which is a centralized but trustless backend component able to relay SBBS messages and handle the connectivity layer for multiple wallet processes. Both components still require a lot of work to be ready for production including extensive security and stability testing, which is why their release is most likely to take place towards the end of the 5.2 time frame.


## Confidential DeFi Track

This section describes the Beam roadmap for Confidential DeFi infrastructure and applications. We plan to combine two different architectural approaches, Scriptless Scripts and Beam Contracts. 

Scriptless Scripts were introduced back in 2017 shortly after the invention of the MW protocol and they describe an idea of replicating Smart Contract like functionality by running most of the calculation off chain and then validating the results using cryptographical concepts such as  Schnorr Adaptor Signatures. Combined with Beam SBBS subsystem this will allow implementation of decentralized and confidential, multiparty trading applications, such as for example Perpetual Swaps described below.

Beam Contracts technology is yet another amazing extension of Mimblewimble protocol for implementing Smart Contracts with built in scripting. It utilizes MW transaction kernels to consume input UTXOs while at the same time updating state variables inside the node. Those variables are then packed into Beam Contracts controlled by Beam Script (which is yet to be designed) thus allowing on chain calculations and emitting new UTXOs as their results. 

Scriptless Scripts and Beam Contracts together provide a powerful infrastructure able to support any existing DeFi application use case including Confidential Stable Coins, lending, and trading, all confidential and decentralized.

Since most of the DeFi tasks require a lot of research and prototyping  we will first release a series of POC and Testnet versions before deciding what is ready to be integrated into the mainnet wallets. Here is a breakdown of the planned milestones for Beam DeFi Track, roughly aligned with wallet release schedule.

### [5.2 timeframe (September - November 2020)](https://github.com/BeamMW/roadmap/projects/3)

#### [Beam Contract architecture POC](https://github.com/BeamMW/roadmap/issues/12)

First POC of the Beam Contract technology should include ability to create contracts with basic scripting capabilities and define clear APIs to use them. Most of this work is already in early design and research stages. 

#### [Oracles](https://github.com/BeamMW/roadmap/issues/13)

In order to enable DeFi applications, we need to use oracles that provide reference price points for the traded assets. There are several possibilities to implement oracles either onchain to be used by Beam Contracts or using SBBS infrastructure to provide signed and verifiable information directly to wallets to be used in the process of negotiation and creating P2P trading contracts between the users. We are currently researching the possibility of building the oracles as well as integration with existing oracle providers.

#### [Perpetual swaps app](https://github.com/BeamMW/roadmap/issues/14)

One of the first applications we are considering are Perpetual Swaps, which are a specific implementation of the futures contracts without a definite expiration date. The application will utilize SBBS for creating contracts and Laser Beam payment channels for locking collateral, handling funding transactions and settlement. More details on the implementation of the application will be provided in a future article.

### 5.3 timeframe (December 2020 - January 2021)

#### [Side chains POC](https://github.com/BeamMW/roadmap/issues/15)

As we move forward it becomes clear that not all of the features could be natively supported on the mainnet while at the same time maintaining its stability and integrity. However, we also do not want to ever stop innovating and taking Beam and its underlying protocols to new extremes. The way to combine these two opposing desires is by introducing side chains.

Beam Side Chain, is basically another independent Beam chain with few key differences and modifications that would make it incompatible with the main chain. Such modifications may include for example as different consensus mechanisms such as GhostDAG or Proof of Stake, or even addition of Smart Contracts. Despite being a separate blockchain, side chains are designed to maintain two side peg to Beam at all times, making it possible to reliably move value from Beam Mainnet to Side chain and back.

Depending on their purpose, side chains can be either created empty or use their own native token. In the first case it and only uses token moved from the Beam main chain. Instead if it uses a native token, it can be either co-mined  or emitted independently using a separate mining algorithm. In any case, new assets created directly on the side chain could never be moved onto Beam and interfere with it's consistency. They can, however, be exchanged for Beam or any other Confidential Asset on Beam network using Atomic Swaps.

### Infrastructure Track

### 5.1 (July - August, 2020)

#### [Bridges to Ethereum](https://github.com/BeamMW/roadmap/issues/16)

Despite providing a lot of value within the Beam chain, it is clear that having the ability to represent wrapped tokens from other networks would provide enormous benefits and possibilities for expansion and adoption. Ethereum as a leading DeFi platform today is clearly the top candidate for such integration. We can think of two possible architectures for Beam <> Eth bridges: federated and decentralized. 

In case of a federated bridge, issuance of the asset is controlled by a multisig wallet which should be trusted to monitor and balance amounts locked and distributed on each chain. This solution is relatively straightforward, however does require the trust in the federation that operates it.

Decentralized bridges depend on the ability of all Beam nodes to monitor the state of specific contracts on Ethereum chain and are much more difficult to implement. One way to approach this is to create a two way SPV clients utilizing Beam Fly Client implementation to be able to get proofs from each chain.

Already in 5.1 we are starting to research and  implement the second, decentralized solution, which is expected to span the 5.2 timeframe.

#### GhostDAG

GhostDAG is a novel consensus algorithm that replaces the blockchain with a k branching directed acyclic graph, which means that at any time there can be between one and k valid branches. This means that blocks can be created faster resulting in higher network throughput. It also provides better miner decentralization and reward distribution as more blocks are created.

We have started working on GhostDAG and it will continue 

## Fierce Fermion 6.x Era

Next major version will come with a fork that will not change the PoW algorithm but rather introduce crucial consensus breaking features to support Confidential DeFi infrastructure. 



## Additional topics 

The following is a list of topics that were raised but not prioritized

Atomic Swaps with Eth
Multisig wallets requiring several signatures to sign the transaction
Audit system that can monitor multiple wallets
Add Dandelion protocol to SBBS messages

Multisig
Audit wallet 
TOR/i2p integration 
mixNet integreaiono 
SBBS over dandelion 

