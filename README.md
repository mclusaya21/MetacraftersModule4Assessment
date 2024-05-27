# MetacraftersModule4Assessment
This project demonstrate a ERC20 contract with mint, burn, transfer, redeem, and check balance functions

# Description
The Ethereum blockchain standard known as Ethereum Request for Comment 20 (ERC20) stipulates two events and specific scripting operations that must be employed when generating a fungible token inside of a smart contract.

# Getting Started
To run this code go https://remix.ethereum.org/ create new file (example DegenToken.sol) and paste the code below.
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

//ERC20 contract with mint, burn, transfer, redeem, and check balance
contract DegenToken is ERC20, Ownable {
    mapping(uint256 => uint256) public itemPrices;

    constructor() ERC20("Degen", "DGN") Ownable(msg.sender) {
          _mint(msg.sender, 1000000 * 10 ** uint(decimals()));
    }
        
    function mint(address account, uint256 amount) public {
        require(msg.sender == owner(), "Only owner can mint new tokens");
        _mint(account, amount);
    }
    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }
     function transfer(address to, uint256 amount) public override returns (bool) {
        require(to != address(0), "ERC20: transfer to the zero address");
        return super.transfer(to, amount);
    }   
    function redeemItems(uint256 itemId, uint256 price) external onlyOwner {
        itemPrices[itemId] = price;
    }

    function redeem(uint256 itemId) public {
        uint256 price = itemPrices[itemId];
        require(price > 0, "Item not available for redemption");
        require(balanceOf(msg.sender) >= price, "Insufficient balance");
        _burn(msg.sender, price);
    }
    function balanceOf(address account) public view virtual override returns (uint256) {
        return super.balanceOf(account);
    }
}

# Author
Lusaya, Maria Carmela J.
Email: 8210131@ntc.edu.ph
