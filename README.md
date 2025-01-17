# Token vesting contract

### Setup

Clone this repository: <br>
`git clone https://github.com/talentvesting/talenvesting_token`

Install dependencies: <br>
`cd token-vesting-contract && npm install`

### Tests

Run unit tests: <br>
`npx hardhat test`

### Deploy

Before running deployment you need to write out setup variables. Run `cp .env.example .env` and write down all params of `.env` file.
Then go to `./scripts/deploy.js` and write down **token**, **beneficiary**, **start**, **cliff**, **release period**, **releases count** variables.<br>
- `token`: Address of token, which beneficiary should receive
- `beneficiary`: Address of beneficiary, who should receive vested tokens
- `start`: Time when vesting start (_should be UNIX timestamp of the certain date_)
- `cliff`: Additional time in seconds which will added to `start`. During the cliff releases is not available (_can be setted as 0 if no cliff_)
- `releasePeriod`: Time in seconds for releases (_e.g. 3 months should be as 7776000_)
- `releaseCount`: Total amount of upcoming releases

All popular networks are supported, for deploy run: <br>
`npx hardhat run scripts/deploy.js --network [NETWORK]`

### Verification on Etherscan

For Etherscan verification after deployment run this commands:<br>

`npx hardhat verify --network [NETWORK_NAME] [FACTORY_CONTRACT] "BENEFICIARY" "START" "CLIFF" "RELEASE_PERIOD" "RELEASE_COUNT"` <br>

### How it works

After deploying the **Vesting contract**, it should receive tokens for future vesting logic. Owner can simply transfer required amount of tokens to the contract address. There are multiply releases with the same delay. When time will be reached release tokens will be available for claiming.
