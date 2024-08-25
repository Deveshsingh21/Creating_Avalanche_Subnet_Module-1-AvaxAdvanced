# Deploying On Our Own Avalanche Subnet

This project contains Solidity smart contracts for an ERC20 token and a Vault contract that allows users to deposit ERC20 tokens in exchange for shares and withdraw them by redeeming their shares. 

# Video Explanation
https://www.loom.com/share/31abf5986a5b4493880ffa235c4cadac

## Contracts

### ERC20 Contract

The `ERC20` interface defines the essential functions and events that any ERC20 token should implement. This interface ensures that the token will be interoperable with other contracts, wallets, and applications that expect these functions to be present.

**Functions:**

- **`totalSupply()`**: Returns the total supply of tokens in existence.
- **`balanceOf(address account)`**: Returns the number of tokens owned by the specified `account`.
- **`transfer(address recipient, uint amount)`**: Transfers `amount` of tokens from the caller's account to the `recipient`.
- **`allowance(address owner, address spender)`**: Returns the remaining number of tokens that `spender` is allowed to spend on behalf of `owner`.
- **`approve(address owner, address spender, uint amount)`**: Sets the `amount` of tokens that `spender` is allowed to withdraw from the `owner`'s account.
- **`transferFrom(address sender, address recipient, uint amount)`**: Transfers `amount` of tokens from `sender` to `recipient` using the allowance mechanism.

**Events:**

- **`Transfer(address indexed from, address indexed to, uint value)`**: Emitted when `value` tokens are transferred from one account to another.
- **`Approval(address indexed owner, address indexed spender, uint value)`**: Emitted when `owner` approves `spender` to spend `value` tokens on their behalf.

### Vault Contract

The `Vault` contract allows users to deposit ERC20 tokens in exchange for shares and withdraw tokens by redeeming their shares. The vault manages a pool of ERC20 tokens and calculates shares based on the value of the tokens in the vault.

**Functions:**

- **`constructor(address _token)`**: Initializes the vault with the ERC20 token contract address.
- **`return_contract_address()`**: Returns the address of the vault contract.
- **`deposit(uint _amount)`**: Allows users to deposit ERC20 tokens into the vault. The user receives shares proportional to the amount deposited.
- **`withdraw(uint _shares)`**: Allows users to withdraw ERC20 tokens from the vault by redeeming their shares.



## How It Works

1. **Install Avalanche CLI**
   - Install avalanche-cli on your UNIX system.
   - Copy ERC20.sol and Vault.sol from this repository.
   - Create you custom subnet on Ubuntu Terminal.
   - In a terminal, run: ```avalanche subnet create <any-subnet-name>```
   - Select the desired options , go with defaults if new.
   - Create chain ID (any positve digits).
   - Deploy you subnet using the command ```avalanche subnet deploy <your-subnet-name>```.
   - Details such as RPC URL , Funded address ,Network name, Chain ID ,Currency Symbol,private key will appear . Use these information to add a new network on Metamask .
   - Switch to the newly created network and import new account using the private key dispalyed in the network information box.

2. **Deploy Contract:**
   - In Remix IDE, select "Injected Web3" as the environment.
   - Deploy ```ERC20.sol``` first.
   - Then deploy ```Vault.sol```, using the deployed address of ```erc20.sol``` as the constructor parameter.

3. **Mint and Deposit Tokens:**
   - Mint some tokens to your address using the mint function in ```ERC20.sol```.
   - Deposit some tokens and receive shares in return using ```Vault.sol```.

## Author
Deveshsingh21 Metacrafters
deveshsingh503@gmail.com
## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
