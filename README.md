# Deploying On Our Own Avalanche Subnet

This project contains Solidity smart contracts for an ERC20 token and a Vault contract that allows users to deposit ERC20 tokens in exchange for shares and withdraw them by redeeming their shares. 

## Contracts

### ERC20 Interface

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

**Internal Functions:**

- **`_mint(address _to, uint _shares)`**: Mints new shares and assigns them to the specified address.
- **`_burn(address _from, uint _shares)`**: Burns shares from the specified address.

## How It Works

1. **Deposit Tokens:**
   - Users can deposit a specified amount of ERC20 tokens into the vault.
   - In return, they receive shares representing their ownership of the vault's token pool.
   - If the vault is empty, the number of shares equals the amount deposited.
   - If the vault already contains tokens, the number of shares is calculated based on the proportion of the deposit to the existing balance.

2. **Withdraw Tokens:**
   - Users can redeem their shares for the underlying ERC20 tokens.
   - The amount of tokens received is proportional to the number of shares being redeemed.

3. **Approve and Transfer Mechanism:**
   - The `deposit` function attempts to approve the vault contract to transfer the user's tokens, which is unconventional. Users typically need to approve the vault contract to transfer tokens on their behalf before calling `deposit`.

## Example Use Cases

- **Liquidity Pools**: The Vault contract can be used as a basic liquidity pool where users deposit ERC20 tokens and receive shares representing their contribution.
- **Token Staking**: The contract can be adapted for staking scenarios where users deposit tokens in exchange for rewards, represented by shares.

## Prerequisites

- Solidity ^0.8.17
- An ERC20-compliant token contract

## Deployment

1. Deploy the ERC20 token contract (if not already deployed).
2. Deploy the Vault contract with the address of the ERC20 token contract.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
