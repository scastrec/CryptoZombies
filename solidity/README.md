# CryptoZombies - Solidify

## Notes about Solidify
* You write contract like you write Java class
* Similar to Java
* `struct` for custom variables
* Functions visibilities:
1. public: can be called by outside the class
2. private: can't be called from outside the class
3. external: Can be called only by outside the class
4. internal: can be called by inside inherited class (like protected in Java)
* Functions pure/views can be run without gas fee because there is no interaction with blockchain
* Functions returns
1. One one more values
2. mutiple values `returns(uint a, uint b, uint c)` and get it
```
  uint a;
  uint b;
  uint c;
  (a, b, c) = multipleReturns();
```
* To comparate string, compare keccak256 hash `if (keccak256(string1) = keccak256("MyZombie"))`
* `address` type is a to recognize ethereum user. You can get user address with `msg.sender`
* `event` function are used to send messages to client (JS)
* If you need to check conditions to run a function use `require`
* contract can inherit from another contract with the keyword _is_ `BabyDog is Dog`
* If you want to receive **Ether**, you function has to use `payable` keyword
* you can import other solidity files with `import "path/file.sol"`
* Storage with solidity in blockchain
1. `storage` keywoard use to store in blockchain `Zombie storage myZombie = ...`
* call other contracts:
1. Create an interface of the wanted contract. It contains all the methods that you want to call but without implémentation`{}` but endig with ';`
2. you call id with `MyExtrernalContract(contractAddress).myFunction()`

## Deploying DApps with Truffle
Truffle is a blockchain development framework
* Smart contract compilation
* Automated ABI Generation
* Smart contract testing (mocha/chai)
* Multiple networks

1. Install Truffle
`npm install truffle -g`
`npm install truffle-hdwallet-provider`
2. Init Truffle
`truffle init`
It creates folders and files :
* contracts/myContract.sol : contract to deploy
* migrations/1_initial_migration.js : How to deploy contract
* test/ : where you store your tests
* truffle-config.js & truffle.js to configure network
3. Compile contract `truffle compile`
It generates bytecode, ABIs and some Truffle files
4. Test the generated contract with Ganache which run a local Ethereum Network (or check [testing with truffle](https://cryptozombies.io/en/lesson/10))
5. Deployments are based on migration file and is really simple
```
var CryptoZombies = artifacts.require("./CryptoZombies.sol");
module.exports = function(deployer) {
  deployer.deploy(CryptoZombies);
};
```
6. Truffle config files
truffle.js contains networks to deploy DApps. For each network alias, you supply a provider using truffle-hdwallet-provider with a token (should be secret) and the address and a network id.
7. Finally, let's deploy
`truffle migrate --network [you_network_alias]`

On the Ethereum mainet, you pay gas fee for each access. To avoid that, you can deploy on Loom which is a multichain interoperability platform.

