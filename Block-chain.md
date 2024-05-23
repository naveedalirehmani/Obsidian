
**Blockchain development.**

**Hashing.**
Hashing is a fundamental concept in computer science and cryptography. It refers to the process of taking an input (or data) of any size and applying a specific mathematical algorithm to generate a fixed-size output, which is usually a sequence of characters or numbers. This fixed-size output is known as the hash value, hash code, or simply the hash.

The primary purpose of hashing is to create a digital fingerprint or unique identifier for the input data.

**Characteristics.**

- **Deterministic:** For the same input, the hash function will always produce the same hash value.
- **Quick Computation:** The hash function should be fast and efficient, allowing for rapid generation of hash values.
- **Preimage Resistance:** Given the hash value, it should be computationally infeasible to determine the original input data.
- **Small Changes in Input Produce Significant Changes in Hash:** Even a minor modification in the input data should result in a completely different hash value.
- **Collision Resistance:** It should be highly improbable for two different inputs to produce the same hash value.

**Some of the hash functions and their characteristics are.**

- **MD5 (Message Digest Algorithm 5)**: 128-bit hash value. However, MD5 is now considered to be weak for cryptographic purposes due to vulnerabilities and collision attacks discovered over the years.
- **SHA-1 (Secure Hash Algorithm 1)**: 160-bit hash value. Similar to MD5, SHA-1 is considered weak for security applications due to vulnerabilities. It is no longer recommended for cryptographic purposes.
- **SHA-2 (Secure Hash Algorithm 2)**: SHA-2 is a family of cryptographic hash functions that includes SHA-224, SHA-256, SHA-384, and SHA-512. These functions produce hash values of different lengths: 224, 256, 384, and 512 bits, respectively. SHA-2 is widely used and considered secure for various cryptographic applications.
- **SHA-3 (Secure Hash Algorithm 3)**: SHA-3 is a family of cryptographic hash functions standardized by NIST (National Institute of Standards and Technology). It offers improved security and resistance against certain types of attacks compared to SHA-2. The SHA-3 family includes hash functions such as SHA3-224, SHA3-256, SHA3-384, and SHA3-512, providing hash values of different lengths.
- **RIPEMD-160 (RACE Integrity Primitives Evaluation Message Digest 160)**: RIPEMD-160 is a cryptographic hash function that produces a fixed-size, 160-bit hash value. It is commonly used in various applications such as digital signatures and certificate authorities.
- **bcrypt**: bcrypt is a password hashing function commonly used for securely storing passwords. Unlike regular hash functions, bcrypt is intentionally slow, which makes it more resistant to brute-force attacks.
- **BLAKE2**: BLAKE2 is a cryptographic hash function that offers high performance and security. It is an improved version of the earlier BLAKE hash function and provides hash values of different lengths. BLAKE2 is designed to be fast and secure, suitable for various cryptographic applications such as message authentication, digital signatures, and key derivation.

---

**Transactions.**
Transactions in the context of blockchain refer to the transfer or exchange of digital assets or data between participants on the blockchain network. These transactions represent the fundamental units of activity recorded on a blockchain.

- Sender and Receiver
- Digital Assets or Data: Cryptocurrencies, tokens and smart contracts.
- Amount or Quantity
- Validation and Verification: ensuring that the assets are not double-spent or fraudulent, and confirming that the transaction adheres to the network's rules and protocols.
- Transaction ID
- Inclusion in Blocks.
- Transaction Fees.

---  

**_ONL-BTC_**

**Mining.**
mining is indeed the process of verifying transactions in a blockchain network. When a transaction is initiated, it needs to be validated by miners before it can be included in a block and added to the blockchain.

Miners earn money through two primary mechanisms: mining rewards and transaction fees.

- **Mining Rewards:** When a miner successfully mines a new block and adds it to the blockchain, they are rewarded with a specific amount of cryptocurrency. In Bitcoin, for instance, the current block reward is 6.25 bitcoins (as of September 2021), but this value is halved approximately every four years through a process known as the "Bitcoin halving." Initially, the block reward was 50 bitcoins, and it has gone through several halvings over time. Other blockchain networks may have different reward structures.
- **Transaction Fees:** In addition to mining rewards, miners also earn transaction fees associated with the transactions included in the blocks they mine. When a user initiates a transaction, they have the option to attach a transaction fee to incentivize miners to prioritize and include their transaction in the next block. Miners, therefore, have an incentive to include transactions with higher fees to maximize their earnings. Transaction fees serve as an additional incentive for miners and contribute to the security and sustainability of the blockchain network.

**Proof Of Work and consensus mechanism.**
block chain is a distributed ledger. this means that each node in a block-chain network has a copy of this ledger. this gives the power to all nodes to verify if a ledger coming from a single node has been mutated or not, through a mechanism called consensus mechanism. there are 2 ways consensus mechanism can work. POW and POS. Here I will be explaining proof of work.

all of the transactions are added to a block and the miners to proof that they are actually contributing to the network have to compete in finding a specific hash fingerprint (not exactly the same fingerprint because that can not be decided in advance as new transaction are still coming in, so we just find a hash fingerprint that in decimal has value less then a specific number. The smaller the number is the harder it is to find the fingerprint. The difficulty of the the block is decided based on the previous history of how long did it took the miners to actually mine the previous block if it was fairly easy the difficulty for the upcoming block is set high if it was hard meaning that it took more time then expected, the difficulty is set low in this case). 

![[Pasted image 20240508123841.png]]

The input for this fingerprint consist of 4 things the transaction history of the block + the nounce of the block which miners can change to find a specific match + hash fingerprint of the previous block + the header for the block. once a specific miner succeeds in finding this specific fingerprint he gets to mint a new block, for which he gets rewarded in 2 ways, the mining reward + the transaction fee.

so this was how a block is minted. now moving onto how this ledger is verified in the network and what makes mutating the ledger very hard and the block-chain data save from the hands of those who want to curupt the system by double spending the currency.

firstly, each block in the block-chain contains the hashprint for the previous block ( expect the genesis block ) this means that if we mutate the transaction history of a single block we would not just need to re mint this block but also every block after.

secondly, every one in the network has the copy to the ledger. this means even if we succeed in mining every block in the block-chain after mutation it will still not be the same for others in the network because, others ledger history + blockhash will not match with ours, which then would cause the network to reject our ledger.  
  
One thing to remember here is that as long as the majority of the nodes in the network are honest. Block-chain is safe.

---

**_ONL-BTC_**

**Mining pool.**
Mining pools are collaborative groups of cryptocurrency miners who combine their computing power to increase their chances of successfully mining 

blocks and earning rewards.

- **Pooling Computing Power**: In a mining pool, individual miners contribute their computing power by connecting their mining hardware or software to the pool's mining server. This pooling of resources allows the pool to have a higher overall hash rate, increasing the chances of finding valid blocks.
- **Block Validation and Rewards**: When a mining pool successfully mines a block, the reward is distributed among the pool members based on their contributions. The pool calculates each member's share of the work by considering factors such as the number of shares submitted, hash rate, or other contribution metrics. The more work a miner contributes, the larger their share of the reward.
- **Share Submission and Difficulty**: Instead of mining for full blocks, miners in a pool work on finding "shares," which are partial solutions to the mining problem. These shares are easier to find and validate compared to full blocks. Each share represents a miner's contribution to the pool's overall mining effort.

**Mining Pool Benefits**:

- Increased Chances of Earning Rewards
- Steady and Predictable Income
- Reduced Variability and Risk
  
**Recording Contributions**

- **Shares**: The primary mechanism for tracking contributions is through shares. When a miner discovers a share, they submit it to the pool. The pool keeps track of each miner's submitted shares and uses them to determine their proportional contribution.

	1. Miners in the pool attempt to find a specific target value or "fingerprint," such as a hash with 20 leading zeros, by iterating through different inputs.
	2. When a miner discovers a partial solution (a share) that meets a certain difficulty level set by the pool, they submit that share to the pool's server.
	3. The pool keeps track of the number of shares submitted by each miner over a certain period, such as a specific time frame or a number of solved shares.
	4. The pool calculates each miner's hash rate based on the number of shares submitted within the defined period. The hash rate represents the miner's computational power relative to the total pool hash rate.
	5. Rewards are distributed to miners based on their proportional contribution to the pool's overall computational power, not solely based on the number of shares submitted. The exact method for calculating rewards may vary depending on the pool's specific rules and reward distribution model.


- **Mining Difficulty**: The mining pool adjusts the difficulty level for share submissions based on the pool's overall hash rate. This adjustment ensures that each miner's contribution is weighted fairly, regardless of their individual hardware capabilities.
- **Stratum Protocol**: Mining pools often use the Stratum protocol, which provides a communication framework between miners and the pool's server. This protocol enables efficient share submission, real-time statistics, and transparent tracking of contributions.
- **Authentication and Worker IDs**: Each miner connecting to a mining pool has a unique worker ID associated with their mining software or hardware. The pool tracks the worker IDs and associates shares and contributions with the respective miners.

---

**Anonymity and pseudonymity on blockchain.**
Anonymity and pseudonymity are two related but distinct concepts related to identity and privacy. Here's an explanation of each term

- **Anonymity:** Anonymity refers to the condition of being unknown or unidentifiable. When someone is anonymous, their true identity is completely concealed and cannot be traced back to them. 
- **Pseudonymity:** Pseudonymity involves the use of a pseudonym or a fictitious name or identifier that represents an individual. In this case, a person may choose to operate under a different name or username to interact or transact within a system or community.

**Unlink ability**
Unlinkability in blockchain refers to the property of ensuring that transactions or activities conducted by participants on the blockchain cannot be easily linked or associated with their real-world identities or other transactions they have performed.

**To hide you identity on blockchain.**

**What not to do.**

- Address association: If a user publicly associates their blockchain address with their real-world identity, either through online profiles, public statements, or transactions.
- On-chain analysis: Sophisticated analysis techniques can be used to analyze the blockchain's transaction history, network patterns, and metadata to try to uncover the real-world identity behind specific addresses.

**What to do.**

- Use multiple addresses.
- Utilize privacy-focused cryptocurrencies: Consider using privacy-focused cryptocurrencies like Monero or Zcash that incorporate privacy-enhancing features by default, such as obfuscated transaction amounts or shielded addresses.
- Employ additional privacy techniques: Combine blockchain usage with privacy-enhancing technologies like VPNs or the Tor network to obfuscate IP addresses.

**Anonymity set**
an anonymity set refers to a group of participants or addresses within a cryptocurrency network that share similar transactional characteristics, making it difficult to determine the true origin or destination of a specific transaction. It is a measure of the privacy or anonymity provided by a particular blockchain protocol.

**Anonymity set in mixing pools**
In the context of mixing pools or transaction mixing techniques, the anonymity set refers to the number of participants or transactions that are combined or mixed together.

---

**Deterministic**
Deterministic refers to a process or system that produces the same output or result when given the same inputs or starting conditions. In other words, in a deterministic system, there is a one-to-one correspondence between the inputs and the outputs, and there is no randomness or uncertainty involved.

---

**Consensus mechanism** 
In a decentralized system or blockchain network, the consensus mechanism ensures that participants collectively agree on the validity and integrity of the data. To achieve this, every participant typically verifies the data to ensure that it has not been altered or tampered with.

#### POW VS POS.

**Proof of Work (PoW):**
In PoW, miners compete to solve complex mathematical puzzles in order to add new blocks to the blockchain and receive rewards. The puzzles require substantial computational power and energy consumption. The miner who successfully solves the puzzle first gets the right to add the next block and is rewarded with newly minted cryptocurrency. Miners investing their time and computational power is POW here.

**Proof of Stake (PoS):**
In PoS, validators are chosen to create new blocks based on the number of cryptocurrency tokens they hold and "stake" as collateral. Validators lock up a certain amount of tokens in their wallets as a security deposit, providing proof of their stake in the network. This was miners proof that in case the try to manipulate the network they have their tokens at stack to loss, which proof their intention to stay honest.

- Some PoS systems select validators randomly, where the probability of selection is proportional to the number of tokens staked. Validators with a larger stake have a higher chance of being chosen.
- Other PoS systems may also consider factors such as the length of time the tokens have been staked. Validators who have staked their tokens for a longer duration may have a higher probability of being selected.

---  

**Forking**:  
Forking in blockchain refers to the creation of a new branch or version of a blockchain. It occurs when there is a divergence in the consensus rules or protocols followed by different participants in the blockchain network.

**Hard Fork**: 
A hard fork is a type of fork that introduces a significant change to the blockchain protocol, making the new version incompatible with the previous version. When a hard fork happens, the blockchain splits into two separate chains, each following its own set of rules.

**Soft Fork**: 
A soft fork is a type of fork that introduces a backward-compatible change to the blockchain protocol. The new rules added in a soft fork are still compatible with the previous version, allowing both upgraded and non-upgraded nodes to continue operating on the same blockchain.

---

**_ONL-ETH_**

**Smart contract:**
smart contracts are contracts on the ethereum blockchain that have the terms and condition of the contract written into the code. This means that everyone on the ethereum blockchain can view the terms and condition of the contract and verify if transactions are occurring according to the terms of the contract. Let’s say you want buy 1ETH on ethereum blockchain you send 1K$ to someone who is selling after receiving the money he refuses to obey by the agreement. Smart contracts can prevent such scam, it is an automated block of code that executes when the terms of contract are fulfilled. This means it acts as an escrow. You deposit the money, the seller deposits the ETH this means that the terms are meet. So the contract automatically sends you the ETH and him the dollars.

another use of this is to buy real estate, lets say there is this NFT on the blockchain that holds the ownership to a house,
instead of buying this NFT from a node directly you can use to perform this transaction through a smart contract.

- There are also some problems with smart contract, for example in the above mentioned scenario what if someone claims the owner ship of your house and does not care about the NFT you own, well in this case government does not abide by the agreements made on blockchain.

- There is also very high Gas fee and people purposely leave errors and loophools in the smart contracts to steal peoples money.
- People also use smart contract to bet on real world data, such as betting own you favorite team. But how does the s-contract get this real world data? We use oracles for this. Oracles can be configured with s-contracts and provide real world data to them.

- In simple words think of smart contracts as account managed by code and as a developer you can write this code and automate how this account behaves. If you want it to be a shopkeeper, it behaves as shopkeeper, that buys or sells EHT for US dollars.

  

**Liquidity pools.**

**Flash loans.**

Flash loans loans are loans that require no collateral tral and need to be paid back instantly. 

- Transaction in crypto can have multiple steps in them unlike real worlds transactions.

For example in one transaction you can take a flash loans from Aave in tokens, use these tokens to buy ethereum on sushi-swap, sell these ethereum at a higher price on uni-swap and then finally pay back tokens to Save. If incase you are not able to complete a transaction completely, these transactions are reverted as if it never existed.

- You also need to pay the gas fee. for these transaction.
- Bots are involved in this heavly so chances of making profit this way is fairly low

Where does this money come from? Aave have investors that lend money to aave which lends money to you, takes 0.9 percent as interest and a big portion of this goes back to investors

---  

**_ONL-ETH_**
  
**Gas**

gas is the unit of measure for the computation price on the ethereum EVM, for exam to perform one addition on EVM you need to pay 3 gas and to multiple you need 5, to send ETH you need 2100.  
miners run these EVM’s on their machines which performs blockchain transactions virtually, so when you need to let say send ETH to an account you need to pay 2100 gas for this. Few things to not here.

- Each gas unit has a minimum gas fee/unit, and this changes on each newly block minted this can increase or decrease. This is directly proportional to the number of users using the blockchain. Another factor is also the price of ETH in dollars as directly proportional.
- On each block the total number of gas units that can be consumed by all transactions is 30 miliion.

So when you want to send ETH on ethereum blockchain you contact miners that run these transactions for you on EVM, these transactions consume gas units. One thing to not here is the miners don’t just accept every transaction request. They accept only transaction request that are more beneficial from them. This means that when you want to send ETH you not such pay the base price for gas unit you also pay extra price, this amount is upto you. The more you pay the more chances are that a miner why prioritise your request because miners will not just accept all request they will only accept transaction that have most gas/unit price paid. So that they don’t just reach the limit on a block on less paid transactions.  

- Gas was introduce to reward the miners and stop attackers from running smart contracts that run in a loop.

**How can you pay less**

- One important thing to note here is that there are also application that can run these computations off the EVM and only use EVM to validate the transaction (this I will explain later)
- Chose a timing for transaction when there are less transaction being requested on the blockchain, such as in the weekends between 12 am t0 4 am. (NOTE this is not in PST)

**Gas Limit**

There are two gas limits one I have discussed earlier that is the gas limit on each block. Another is one that is set by the user, this limit is simple the maximum amount of gas units that I am willing to pay for one my transactions as a user, this is to prevent situations such as the transaction consuming more gas units then my predicted value. So that I don’t pay way more than I intend to. All this because we cannot exactly tell the amount of gas units each transaction will take we can only predict.  
  
three factors that make it hard to exactly tell how much each transaction will take are.

- Complexity of the computation.
- Amount of data that will be precessed.
- State of the blockchain.

---

  

  

  

  

  

  

  

  

  

            Gas 

liquidity pools

flash loans 

EVM,  

turing machine. 

UTXO’s

creating a metamask wallet and understanding the 12 phrases.

  
Blockchain

Cryptocurrency

Consensus Mechanism

Smart Contracts

Decentralization

Immutable Ledger

Public vs. Private Blockchain

Tokenization

DApps (Decentralized Applications)

Interoperability

Fork

Permissioned vs. Permissionless

Scalability

Privacy and Confidentiality

Blockchain Intermediaries

Oracles

Token Standards

Governance

Sidechains

Off-Chain Scaling Solutions

  

  

To Read -

  

- Dedicated mixes.

- Mixing fee

- Mixing pool

- Reliability  issues in mixing pools

- Use uniforms transactions

- Why mixing pools failed.

- Decentralising the mixings pools

- Coin join

  

Best practicies for anonymity in mixing pools

Certainly! Here are some best practices for transaction mixing, client channel attacks, client-side automation, and privacy-friendly techniques:

1. Transaction Mixing Best Practices:

    * Choose a reputable mixing service: Select a mixing service or protocol that has a good reputation for privacy and security.

    * Use a large anonymity set: Opt for mixing pools or services that have a large number of participants to increase the anonymity set and make it harder to trace transactions.

    * Mix multiple times: Consider mixing your transactions multiple times to further obfuscate the transactional flow.

    * Randomize transaction amounts: Mix transactions with varying amounts to make it more difficult to link inputs and outputs.

2. Client Channel Attacks:

3. Client channel attacks refer to potential vulnerabilities in the communication channels between the user and the mixing service. To mitigate these attacks:

    * Use encrypted communication: Ensure that the communication between your device and the mixing service is encrypted using protocols such as HTTPS or VPNs.

    * Validate SSL certificates: Verify the authenticity of SSL certificates to prevent man-in-the-middle attacks.

    * Be cautious of phishing attempts: Avoid clicking on suspicious links or providing sensitive information to unknown sources.

4. Client-Side Automation:

5. Automating the client-side process of transaction mixing can improve convenience and reduce user error. Consider the following:

    * Use trusted automation tools: Utilize reputable software or tools that automate the transaction mixing process, but ensure they come from trusted sources.

    * Verify the integrity of automation tools: Check the authenticity and integrity of the automation tools before using them to avoid potential malware or compromise.

6. Privacy-Friendly Techniques:

    * Use privacy-focused cryptocurrencies: Consider using privacy-centric cryptocurrencies like Monero or Zcash, which offer enhanced privacy features by default.

    * Utilize stealth addresses: Stealth addresses enable the receiver to generate a unique address for each transaction, making it harder to track the recipient's identity.

    * Zero-knowledge proofs: Explore protocols that utilize zero-knowledge proofs, such as zk-SNARKs (Zero-Knowledge Succinct Non-Interactive Argument of Knowledge), which allow for the verification of transactions without revealing sensitive information.

    * Employ VPNs and Tor: Utilize privacy-enhancing technologies like Virtual Private Networks (VPNs) or the Tor network to obfuscate your IP address and online activities.

It's important to note that while these practices can enhance privacy, they do not provide foolproof anonymity. Careful consideration of the specific tools, protocols, and potential risks is essential when adopting these techniques.

  

  

Terminologies.