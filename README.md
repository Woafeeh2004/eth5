# eth5
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Escrow {
    address public buyer;
    address public seller;
    bool public isFunded;

    constructor(address _seller) {
        buyer = msg.sender;
        seller = _seller;
    }

    function deposit() public payable {
        require(msg.sender == buyer, "Only buyer");
        isFunded = true;
    }

    function release() public {
        require(msg.sender == buyer, "Only buyer");
        require(isFunded, "Not funded");
        payable(seller).transfer(address(this).balance);
    }
}
