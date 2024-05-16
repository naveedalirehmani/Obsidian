
**Blockchain development.**

**Hashing.**
Hashing is a fundamental concept in computer science and cryptography. It refers to the process of taking an input (or data) of any size and applying a specific mathematical algorithm to generate a fixed-size output, which is usually a sequence of characters or numbers. This fixed-size output is known as the hash value, hash code, or simply the hash.

The primary purpose of hashing is to create a digital fingerprint or unique identifier for the input data.

**Characteristics.**

- **Deterministic:** For the same input, the hash function will always produce the same hash value.
- **Quick Computation:** The hash function should be fast and efficient, allowing for rapid generation of hash values.
- **Preimage Resistance:** Given the hash value, it should be computationally infeasible to determine the original input data.
- Small Changes in Input Produce Significant Changes in Hash: Even a minor modification in the input data should result in a completely different hash value.
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
