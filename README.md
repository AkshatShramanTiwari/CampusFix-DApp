# CampusFix — Decentralized Campus Maintenance DApp

CampusFix lets campus users submit maintenance issues to an Ethereum-compatible blockchain and transparently track status updates. The contract owner (administrator) can move requests between **Open**, **In Progress**, and **Resolved**.

## Features
- Solidity smart contract with input validation and sequential request IDs.
- MetaMask wallet connection using ethers.js v6.
- On-chain request creation and request-history reads.
- Status filtering and request summary counters.
- Owner-only status updates enforced by the smart contract.
- Events for request creation and status changes.

## Project files
- `CampusFix.sol` — smart contract.
- `index.html`, `style.css`, `app.js` — browser interface.
- `SUBMISSION_REPORT.md` — report template and test checklist.
- `screenshots/README.md` — evidence screenshot checklist.

## Deploy and run
1. Open [Remix](https://remix.ethereum.org/) and create `CampusFix.sol`.
2. Paste the contract source, select Solidity compiler version **0.8.20 or compatible 0.8.x**, and compile.
3. Deploy using Remix VM for local testing, or connect MetaMask to the instructor-approved test network. Keep the deploying wallet as the contract owner for administrator controls.
4. Copy the deployed contract address.
5. In `app.js`, replace `PASTE_DEPLOYED_CONTRACT_ADDRESS_HERE` with that address.
6. Serve this directory over HTTP (for example, VS Code Live Server or `python -m http.server 8000`). Open the local HTTP URL in a browser with MetaMask available. Opening `index.html` directly with `file://` may prevent wallet access.
7. Set MetaMask to the same network used for deployment, connect the wallet, and approve transactions when prompted.

The page loads ethers.js v6 from jsDelivr, so an internet connection is required for that CDN dependency.

## Contract rules
- Title: non-empty, at most 80 UTF-8 bytes.
- Description: non-empty, at most 500 UTF-8 bytes.
- Only the deployer/owner may call `updateStatus`.
- Request ID must be within the existing range.
- A request cannot be assigned its current status again.

## Suggested tests
1. Compile and deploy successfully.
2. Submit a valid request and verify the transaction and request list.
3. Attempt empty title/description and over-limit values.
4. Update a request status from the owner account.
5. Switch to a different account and confirm status update is rejected.
6. Query an invalid request ID and try updating an invalid ID.
7. Attempt to set a request to its current status.

Record observed results and attach real screenshots in the report. Do not claim a test passed until you have run it. Never commit wallet seed phrases, private keys, or other secrets. Request descriptions are public on-chain; do not submit personal or confidential information.