### todo 

1. ether.js ( for connecting to the network  )
2. hardhat ( for contract automated deployment ) 
3. wagmi. ( similar to tanstack query )
4. meta mask detector provider. ( meta mask wallet detector. )

### Step 1: Deploy the Smart Contract

1. **Open Remix IDE**:
    
    - Go to Remix IDE.
2. **Create a New File**:
    
    - Create a new file named `Twitter.sol` and paste your Solidity contract code into it.
3. **Compile the Contract**:
    
    - Click on the "Solidity Compiler" tab.
    - Select the appropriate compiler version (e.g., 0.8.0) and click "Compile Twitter.sol".
4. **Deploy the Contract**:
    
    - Click on the "Deploy & Run Transactions" tab.
    - Set the environment to "Injected Web3" to use MetaMask.
    - Connect your MetaMask wallet.
    - Enter the constructor parameter `_userContractAddress` (an address that implements the `IProfile` interface) and click "Deploy".
    - After deployment, copy the contract address.

### Step 2: Set Up the Web Application

1. **Create a React Project**:
    
    bash
    
    Copy code
    
    `npx create-react-app twitter-dapp cd twitter-dapp`
    
2. **Install Dependencies**:
    
    bash
    
    Copy code
    
    `npm install ethers @metamask/detect-provider`
    

### Step 3: Connect to the Ethereum Network

Create a `src/ethereum.js` file to handle the connection to the Ethereum network:

```ts ethereum.ts
// src/ethereum.ts
import { ethers } from 'ethers';
import detectEthereumProvider from '@metamask/detect-provider';

const getEthereumProvider = async (): Promise<ethers.providers.Web3Provider | void> => {
  const provider = await detectEthereumProvider();
  if (provider) {
    return new ethers.providers.Web3Provider(provider as any);
  } else {
    console.log('Please install MetaMask!');
  }
};

export default getEthereumProvider;

```

### Step 4: Interact with the Smart Contract

Create a `src/contract.js` file to define and interact with your smart contract. Replace the placeholder ABI with your actual contract ABI from Remix.

```ts contract.ts
// src/contract.ts
import { ethers } from 'ethers';
import getEthereumProvider from './ethereum';

// Replace with your contract ABI
const contractABI: any[] = [
  // Add your contract ABI here
];

// Replace with your contract address
const contractAddress: string = '0xYourContractAddress';

const getContract = async (): Promise<ethers.Contract> => {
  const provider = await getEthereumProvider();
  if (!provider) {
    throw new Error('Ethereum provider not available');
  }
  const signer = provider.getSigner();
  const contract = new ethers.Contract(contractAddress, contractABI, signer);
  return contract;
};

export const addTweet = async (tweetContent: string): Promise<void> => {
  const contract = await getContract();
  const transaction = await contract.addtweet(tweetContent);
  await transaction.wait();
};

export const likeTweet = async (id: string, author: string): Promise<void> => {
  const contract = await getContract();
  const transaction = await contract.likeTweet(id, author);
  await transaction.wait();
};

// Add other functions similarly...
```

### Step 5: Create the React Components

Create a simple React component to interact with your contract in `src/App.js`:

```ts
// src/App.tsx
import React, { useState, useEffect } from 'react';
import { addTweet, likeTweet } from './contract';
import getContract from './contract';

interface Tweet {
  id: string;
  content: string;
  author: string;
  likes: number;
}

function App() {
  const [tweetContent, setTweetContent] = useState<string>('');
  const [tweets, setTweets] = useState<Tweet[]>([]);

  const handleAddTweet = async () => {
    await addTweet(tweetContent);
    setTweetContent('');
    fetchTweets(); // Fetch tweets again to update the list
  };

  const handleLikeTweet = async (id: string, author: string) => {
    await likeTweet(id, author);
    fetchTweets(); // Fetch tweets again to update the list
  };

  const fetchTweets = async () => {
    const contract = await getContract();
    const userAddress = await contract.signer.getAddress();
    const userTweets = await contract.getAllTweets(userAddress);
    setTweets(userTweets);
  };

  useEffect(() => {
    fetchTweets();
  }, []);

  return (
    <div>
      <h1>Twitter DApp</h1>
      <input
        type="text"
        value={tweetContent}
        onChange={(e) => setTweetContent(e.target.value)}
      />
      <button onClick={handleAddTweet}>Add Tweet</button>
      <div>
        {tweets.map((tweet, index) => (
          <div key={index}>
            <p>{tweet.content}</p>
            <p>By: {tweet.author}</p>
            <p>Likes: {tweet.likes}</p>
            <button onClick={() => handleLikeTweet(tweet.id, tweet.author)}>Like</button>
          </div>
        ))}
      </div>
    </div>
  );
}

export default App;
```

### Final Steps

1. **Run Your React App**:
    
    bash
    
    Copy code
    
    `npm start`
    
2. **Connect MetaMask**:
    
    - Ensure MetaMask is installed in your browser and connected to the same network where your smart contract is deployed (e.g., Ropsten, Rinkeby).
3. **Test the Functionality**:
    
    - Add and interact with tweets through your web application.

### Contract ABI

Make sure to replace the `contractABI` in `contract.js` with your actual contract ABI, which you can get from the Remix IDE after compiling your contract. Here’s an example ABI snippet:

```json
[
    {
        "inputs": [
            {
                "internalType": "address",
                "name": "_userContractAddress",
                "type": "address"
            }
        ],
        "stateMutability": "nonpayable",
        "type": "constructor"
    },
    {
        "anonymous": false,
        "inputs": [
            {
                "indexed": false,
                "internalType": "uint256",
                "name": "id",
                "type": "uint256"
            },
            {
                "indexed": false,
                "internalType": "address",
                "name": "author",
                "type": "address"
            },
            {
                "indexed": false,
                "internalType": "string",
                "name": "content",
                "type": "string"
            },
            {
                "indexed": false,
                "internalType": "uint256",
                "name": "timestamp",
                "type": "uint256"
            }
        ],
        "name": "TweetCreated",
        "type": "event"
    },
    {
        "anonymous": false,
        "inputs": [
            {
                "indexed": false,
                "internalType": "address",
                "name": "liker",
                "type": "address"
            },
            {
                "indexed": false,
                "internalType": "address",
                "name": "tweetAuthor",
                "type": "address"
            },
            {
                "indexed": false,
                "internalType": "uint256",
                "name": "tweetId",
                "type": "uint256"
            },
            {
                "indexed": false,
                "internalType": "uint256",
                "name": "totalLikeCount",
                "type": "uint256"
            }
        ],
        "name": "TweetLiked",
        "type": "event"
    },
    {
        "anonymous": false,
        "inputs": [
            {
                "indexed": false,
                "internalType": "address",
                "name": "unLiker",
                "type": "address"
            },
            {
                "indexed": false,
                "internalType": "address",
                "name": "tweetAuthor",
                "type": "address"
            },
            {
                "indexed": false,
                "internalType": "uint256",
                "name": "tweetid",
                "type": "uint256"
            },
            {
                "indexed": false,
                "internalType": "uint256",
                "name": "totalLikeCount",
                "type": "uint256"
            }
        ],
        "name": "UnlikeTweet",
        "type": "event"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "_newTwtLength",
                "type": "uint256"
            }
        ],
        "name": "maxTweetLength",
        "outputs": [],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "string",
                "name": "_twt",
                "type": "string"
            }
        ],
        "name": "addtweet",
        "outputs": [],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "id",
                "type": "uint256"
            },
            {
                "internalType": "address",
                "name": "author",
                "type": "address"
            }
        ],
        "name": "likeTweet",
        "outputs": [],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "uint256",
                "name": "id",
                "type": "uint256"
            },
            {
                "internalType": "address",
                "name": "author",
                "type": "address"
            }
        ],
        "name": "unLikeTweet",
        "outputs": [],
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "address",
                "name": "_owner",
                "type": "address"
            },
            {
                "internalType": "uint256",
                "name": "_i",
                "type": "uint256"
            }
        ],
        "name": "getTweet",
        "outputs": [
            {
                "components": [
                    {
                        "internalType": "uint256",
                        "name": "id",
                        "type": "uint256"
                    },
                    {
                        "internalType": "address",
                        "name": "author",
                        "type": "address"
                    },
                    {
                        "internalType": "string",
                        "name": "content",
                        "type": "string"
                    },
                    {
                        "internalType": "uint256",
                        "name": "timestamp",
                        "type": "uint256"
                    },
                    {
                        "internalType": "uint256",
                        "name": "likes",
                        "type": "uint256"
                    }
                ],
                "internalType": "struct Twitter.Tweet",
                "name": "",
                "type": "tuple"
            }
        ],
        "stateMutability": "view",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "address",
                "name": "_owner",
                "type": "address"
            }
        ],
        "name": "getAllTweets",
        "outputs": [
            {
                "components": [
                    {
                        "internalType": "uint256",
                        "name": "id",
                        "type": "uint256"
                    },
                    {
                        "internalType": "address",
                        "name": "author",
                        "type": "address"
                    },
                    {
                        "internalType": "string",
                        "name": "content",
                        "type": "string"
                    },
                    {
                        "internalType": "uint256",
                        "name": "timestamp",
                        "type": "uint256"
                    },
                    {
                        "internalType": "uint256",
                        "name": "likes",
                        "type": "uint256"
                    }
                ],
                "internalType": "struct Twitter.Tweet[]",
                "name": "",
                "type": "tuple[]"
            }
        ],
        "stateMutability": "view",
        "type": "function"
    },
    {
        "inputs": [
            {
                "internalType": "address",
                "name": "_owner",
                "type": "address"
            }
        ],
        "name": "getTotalLikes",
        "outputs": [
            {
                "internalType": "uint256",
                "name": "",
                "type": "uint256"
            }
        ],
        "stateMutability": "view",
        "type": "function"
    }
]

```