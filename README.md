# SolidityCONTRACTinsideAcontract
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.18;

contract Skipperman { 
    uint256 myFavoriteNumber;

    struct Person {
        uint256 favoriteNumber;
        string name;
    }

    // Dynamic array of Person structs
    Person[] public listOfPeople;

    mapping(string => uint256) public nameToFavoriteNumber; 

    Person public Skip = Person({favoriteNumber: 27, name: "Skip"});
    Person public Nas = Person({favoriteNumber: 2, name: "Nas"});
    Person public Cookie = Person({favoriteNumber: 1, name: "Cookie"});

    function store(uint256 _favoriteNumber) public {
        myFavoriteNumber = _favoriteNumber;
    }

    //view, pure
    function retrieve() public view returns(uint256) {
        return myFavoriteNumber;
    }

    // calldata, memory, storage
    function addPerson(string memory name, uint256 _favoriteNumber) public {
        listOfPeople.push( Person({favoriteNumber: _favoriteNumber, name: name}) );
        nameToFavoriteNumber[name] = _favoriteNumber; 
    }
}


contract StorageFactory {

    //uint256 public favoriteNumber
    //type visibility name
    SimpleStorage public simpleStorage; 

    address[] public contracts;

    function createSimpleStorageContract() public  {
        address newContract = address(new Skipperman());
        contracts.push(newContract);
    }
    
    function getContracts() public view returns(address[] memory){
        return contracts;
    }
}
