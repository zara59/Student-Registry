# Enroll

Student records on-chain. React and Vite frontend for a Student Registry smart contract, built with `ethers` v6 and MetaMask.

React + Vite frontend for a Student Registry smart contract, built with `ethers` v6 and MetaMask.

## Contract interface

```solidity
function getStudent(address _student) view returns (string name, uint256 age, string course);
function register(string _name, uint256 _age, string _course);
function registered(address) view returns (bool);
```

Paste the deployed contract address into the app. It is saved in `localStorage`, so the same
frontend works against any deployment.

## Run

```bash
npm install
npm run dev
```

Also available: `npm run build` for a production bundle and `npm run lint` for ESLint.

## Features

- Connect an injected EVM wallet (MetaMask) with `eth_requestAccounts`, plus a silent
  `eth_accounts` session restore on page load
- Live account, network, chain ID and balance, kept in sync by the `accountsChanged` and
  `chainChanged` listeners
- Disconnect button that clears the dapp session
- Supported chain list (Sepolia 11155111, Base Sepolia 84532) with one-click network switching
- Unsupported network error followed by a prompt to switch back to a supported chain
- Refresh balance button showing the time of the last update
- Reads `registered(address)` and `getStudent(address)` for the connected account
- Writes `register(name, age, course)` with waiting-for-signature, mining and confirmed states

## Structure

| Path | Purpose |
| --- | --- |
| `src/App.jsx` | Page layout and header actions |
| `src/hooks/useWallet.js` | Connection state, wallet listeners, balance fetching, chain switching |
| `src/components/StudentRegistry.jsx` | Contract reads and the register form |
| `src/components/AccountDetails.jsx` | Account, network and balance panel |
| `src/components/ChainList.jsx` | Supported chain list |
| `src/components/UnsupportedChainBanner.jsx` | Unsupported network error and switch-back prompt |
| `src/constants.js` | Supported networks and contract ABI |
| `src/utils/format.js` | Address, balance and date formatting |

## Deployment

`.github/workflows/pages.yml` builds the app and publishes it to GitHub Pages. Enable it once under
**Settings → Pages → Build and deployment → Source: GitHub Actions**.

## Requirements

MetaMask on a testnet account. Testnet ETH can be requested from a Sepolia faucet.
