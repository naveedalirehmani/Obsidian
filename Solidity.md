
### Functions
![[Pasted image 20240508151837.png]]

### Maps
maps are similar to objects in javascript.
![[Pasted image 20240509153514.png]]


### Arrays
![[Pasted image 20240509154753.png]]

### Visibilities

1. **External**: They can be called by other contracts or transactions and cannot be accessed internally
2. **Internal**: they can only be called within the contract that defines them and any derived contracts. They are not accessible by contracts that inherit from them or by external contracts.
3. **Private**: Private functions and state variables are only accessible within the contract that defines them. They are not accessible by derived contracts or external contracts.
4. **Public**: Public functions and state variables can be accessed both internally and externally.
  
| Visibility Specifier | Accessible in Derived Class | Accessible from Outside | Accessible for Another Contract | callable within contract |     |
| -------------------- | --------------------------- | ----------------------- | ------------------------------- | ------------------------ | --- |
| external             | Yes                         | Yes                     | yes                             | No                       |     |
| public               | Yes                         | Yes                     | Yes                             | Yes                      |     |
| private              | No                          | No                      | No                              | Yes                      |     |
| internal             | Yes                         | No                      | No                              | Yes                      |     |
	
### State mutabilities 

1. **Pure**: Functions declared as `pure` do not read or modify the state of the contract. They are used when you want to perform computations based only on the provided parameters and return a value without interacting with the blockchain.
2. **View**: Functions declared as `view` (formerly `constant` before Solidity version 0.4.17) do not modify the state of the contract. They are used to read data from the blockchain without modifying it.
3. **Payable**: Functions declared as `payable` can receive Ether along with the function call. They are used when you want to allow users to send Ether to the contract when calling the function. Payable functions can modify the contract's state.
4. **Nonpayable (default)**: Functions that do not have a state mutability specifier explicitly defined are considered `nonpayable` by default. They can modify the state of the contract but cannot receive Ether.

### is 
use is keyword to extend a drived class.
### abstract
use abstract instead of contract to state that this class is only meant to be inherited from. Not to be used as a stand alone contract.

### classes
```ts
pragma solidity ^0.8.0;

contract Base {
    uint256 private baseValue;

    constructor(uint256 _baseInitialValue) {
        baseValue = _baseInitialValue;
    }

    function getValue() public view virtual returns (uint256) {
        return baseValue;
    }
}

contract Intermediate is Base {
    uint256 private intermediateValue;

    constructor(uint256 _baseInitialValue, uint256 _intermediateInitialValue) Base(_baseInitialValue) {
        intermediateValue = _intermediateInitialValue;
    }

    function getValue() public view virtual override returns (uint256) {
        return intermediateValue;
    }
}

contract Derived is Intermediate {
    uint256 private derivedValue;

    constructor(uint256 _baseInitialValue, uint256 _intermediateInitialValue, uint256 _derivedInitialValue) Intermediate(_baseInitialValue, _intermediateInitialValue) {
        derivedValue = _derivedInitialValue;
    }

    function getValue() public view override returns (uint256) {
        return derivedValue;
    }
}

```

### Contract to contract communication.
two contract can communicate to each other. what are the requirement’s?
1. methods in a contract that are supposed to be called from another should have visibility external.
2. you need to create a interface for the function that will be called.

**code example : user contract**
```ts
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

// 1️⃣ Create a new Player and save it to players mapping with the given data

contract User {
    struct Player {
        address playerAddress;
        string username;
        uint256 score;
    }

    mapping(address => Player) public players;

    function createUser(address userAddress, string memory username) external {
        require(players[userAddress].playerAddress == address(0), "User already exists");

        // Create a new player here 👇
        Player memory newPlayer;
        newPlayer.playerAddress = userAddress;
        newPlayer.username = username;
        newPlayer.score = 0;

        players[userAddress] = newPlayer;
    }
}

```

**game contract**
```ts
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

// 2️⃣ Set up a connection to the User Contract throught IUser in constructor
// 3️⃣ Call the createUser function with the correct inputs

interface IUser {
    function createUser(address userAddress, string memory username) external;
}

contract Game {
    uint public gameCount;
    IUser public userContract;

    constructor(address _userContractAddress) {
        // CODE HERE
        userContract = IUser(_userContractAddress);
    }

    function startGame(string memory username) external {
        // Create a user in the User contract
        gameCount++;
        // CODE HERE
        userContract.createUser(msg.sender, username);
    }
}

```
























