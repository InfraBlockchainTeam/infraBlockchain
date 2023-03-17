# infrablockchain-js

## Account Info

1.) Create a new folder on your computer, I will name mine `infrajs-tutorial`.

2.) Navigate into the `infrajs-tutorial` folder and initialize the npm project with `npm init` . You can enter your information, or simply just press enter for each step. Once done, you should see a `package.json` file within the folder

3.) Inside of this folder install eosjs and node-fetch by entering `npm install infrablockchain-js node-fetch`. Node-fetch will give us the ability to execute HTTP requests from within our script.

4.) Create the entrypoint file for the project either through the command line or by doing it through your IDE / text editor. The file's name should be `getAccount.js`

5.) Inside of `getAccount.js` insert the following code:

```
const fetch = require('node-fetch')
const infrajs = require('infrablockchain-js')
const JsonRpc = infrajs.JsonRpc

const ENDPOINT = `https://someendpoint.io`
const rpc = new JsonRpc(ENDPOINT, { fetch })

const getAccount = async (accountName) => {
  const accountInfo = await rpc.get_account(accountName)
  console.log('account info: ', accountInfo)
}

getAccount('myAccount')
```

Notes have been included in the file explaining how the code works. The script imports two libraries, `fetch` and `infrablockchain-js`, sets an InfraBlockchain network endpoint, defined a `getAccount` routine that takes an account name as an input and executes the `get_account` procedure on the endpoint.

6.) Go ahead and run the script from the terminal with the `node getAccount.js` command. The result in your terminal _should_ look something like the following (note that `captaincrypt` is my account name:

```
account info:  { account_name: 'captaincrypt',
  head_block_num: 28074886,
  head_block_time: '2020-01-26T00:14:45.000',
  ...
  ram_quota: 129399,
  net_weight: 200000,
  cpu_weight: 200000,
  net_limit: { used: 0, available: 110385499, max: 110385499 },
  cpu_limit: { used: 0, available: 20647737, max: 20647737 },
  ram_usage: 3454,
  permissions:
   [ { perm_name: 'active', parent: 'owner', required_auth: [Object] },
     { perm_name: 'owner', parent: '', required_auth: [Object] } ],
  total_resources:
   { owner: 'captaincrypt',
     net_weight: '20.0000 TLOS',
     cpu_weight: '20.0000 TLOS',
     ram_bytes: 127999 },
  self_delegated_bandwidth:
   { from: 'captaincrypt',
     to: 'captaincrypt',
     net_weight: '20.0000 TLOS',
     cpu_weight: '20.0000 TLOS' },
  refund_request: null,
  voter_info:
  ...
```

Congratulations, we have proven that your account has been registered by the network. If your results don't look anything like the above then make sure you have already gone through the account activation process, and that the endpoint you used is really online.

Now that we've established that our account is activated, it's time for us to take a closer look into transactions.

## Transaction Info

Much the same as our RPC method for getting account info, there also exists an endpoint for getting information about transactions.
