// SPDX-License-Identifier: Unlicensed
pragma solidity ^0.6.0;

contract MyBank {
    mapping(address => uint256) private _balances;
    address public owner;
    event LogDepositeMade(address accountHolder, uint256 amount);

    constructor() public {
        owner = msg.sender; // owner: who builds the contract and deploys that contract
        emit LogDepositeMade(msg.sender, 1000);
    }

    // deposit function
    function deposite() public payable returns (uint256) {
        require(
            (_balances[msg.sender] + msg.value) > _balances[msg.sender] &&
                msg.sender != address(0)
        );
        _balances[msg.sender] += msg.value;
        emit LogDepositeMade(msg.sender, msg.value);
        return _balances[msg.sender];
    }

    // withdraw function
    function withdraw(uint256 withdrawAmount) public returns (uint256) {
        require(_balances[msg.sender] >= withdrawAmount);
        require(msg.sender != address(0));
        require(_balances[msg.sender] > 0);
        _balances[msg.sender] -= withdrawAmount;
        msg.sender.transfer(withdrawAmount);
        emit LogDepositeMade(msg.sender, withdrawAmount);
        return _balances[msg.sender];
    }

    // view balance
    function viewBalance() public view returns (uint256) {
        return _balances[msg.sender];
    }
}
