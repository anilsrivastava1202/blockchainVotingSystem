# Build your First Decentralized Application (DApp) Tutorial

A quick tutorial to get your first DApp up and running without any frameworks!

By Anil Kumar <br/>
Created: 18-AUG-2018 <br/>

Install Dependencies:
1. ganache-cli ```npm install ganache-cli web3@0.20.2```
2. solc ```npm install solc```

Directions:
1. Git Clone this repository
2. Run ganache-cli ```node_modules/.bin/ganace-cli```
3. Open up Nodejs console ```node```
4. Compile the contract
  ```
  code = fs.readFileSync('Voting.sol').toString()
  solc = require('solc')
  compiledCode = solc.compile(code)
  ```

5. Deploy the contract
  ```
  abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface)
  VotingContract = web3.eth.contract(abiDefinition)
  byteCode = compiledCode.contracts[':voting'].bytecode
  deployedContract = VotingContract.new(['Ankur','Gaurav','Hemant'],{data: byteCode, from: web3.eth.accounts[0], gas: 4700000})
  contractInstance = VotingContract.at(deployedContract.address)
  ```



Interacting with contract through nodejs console
```
> contractInstance.totalVotesFor.call('Ankur')
Output: { [String: '0'] s: 1, e: 0, c: [ 0 ] }

> contractInstance.voteForCandidate('Ankur', {from: web3.eth.accounts[0]})
Output: '0x5aad33103dc8099925f707dd9b58613cff8e54de13fe445ec610ae3aa5be88ff'

> contractInstance.voteForCandidate('Gaurav', {from: web3.eth.accounts[0]})
Output: '0x04a281f8a61621ac8ad5b5d3ee185c189e20304c39323d61bca4fa98419ef292'

> contractInstance.voteForCandidate('Hemant', {from: web3.eth.accounts[0]})
Output:  '0xcbbd77573fac176fe4f2dcadbfa27f5df6556bd3603a98aa687316fe452e0c7a'

> contractInstance.totalVotesFor.call('Ankur').toLocaleString()
Output: '1'
```

Interacting with contract via front GUI
1. Update the contract instance address in index.js
  * Can run command ```contractInstance.address``` to find address
2. Open index.html in your browser
