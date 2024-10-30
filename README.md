# VoteChain: A Decentralized Voting System

**VoteChain** is a decentralized voting system designed to provide a secure, transparent, and democratic approach to decision-making on the blockchain. Built with Clarity, VoteChain enables users to create proposals and vote in an immutable, tamper-proof manner. Key features include proposal creation, voting, and administrative control over proposal lifetimes.

## Features

1. **Proposal Creation**: Users can create new proposals, specifying a title, description, and voting duration.
2. **Voting**: Any user can cast a "yes" or "no" vote on open proposals.
3. **Vote Tracking**: Ensures that users cannot vote multiple times on the same proposal.
4. **Voting Closure**: Only the contract owner can close voting on proposals once the voting duration has ended.
5. **Proposal and Voting Validation**: Prevents unauthorized actions and enforces proposal title, description length, and duration validity.

## Smart Contract Overview

The VoteChain contract is divided into constants, data maps, read-only functions, private functions, and public functions, ensuring clear separation of functionalities and efficient validation.

### Constants
- **CONTRACT_OWNER**: Specifies the contract owner (initially `tx-sender`).
- **Error Codes**: Defines errors for unauthorized actions, duplicate votes, invalid proposal details, and closed voting.

### Data Structures
- **Proposals Map**: Stores proposal details, including title, description, creator, yes/no votes, and end block.
- **Votes Map**: Tracks each voter's choice on specific proposals to prevent duplicate voting.

### Public Functions

- **create-proposal**: Enables users to create a proposal with specified title, description, and voting duration.
- **vote**: Allows users to vote on proposals with "yes" or "no". Checks if voting is open and ensures one vote per user per proposal.
- **close-voting**: Grants the contract owner authority to close voting for a proposal once its duration has expired.

### Read-only Functions
- **get-proposal**: Retrieves the details of a specific proposal.
- **get-vote**: Fetches the vote cast by a specific user on a proposal.
- **is-voting-open**: Checks if a proposal's voting duration is still open.

### Private Functions
- **validate-string-length**: Ensures that titles and descriptions meet specified length constraints.

## Usage

### Prerequisites
- Familiarity with Clarity smart contracts and Stacks blockchain.
- Access to a Clarity-compatible development environment like Clarinet.

### Deployment
1. Clone the repository and navigate to the project folder.
2. Deploy the contract using Clarinet or another Clarity environment.
3. Interact with the contract through the Clarity REPL or a Stacks-compatible front-end.

### Example

1. **Create a Proposal**:
   ```clarity
   (contract-call? .vote-chain create-proposal "Proposal Title" "Description" u100)
   ```

2. **Vote on a Proposal**:
   ```clarity
   (contract-call? .vote-chain vote u1 true) ;; vote true for "yes"
   ```

3. **Close Voting** (Contract Owner Only):
   ```clarity
   (contract-call? .vote-chain close-voting u1)
   ```

## Error Codes
| Error Code | Description                           |
|------------|---------------------------------------|
| `u100`     | Unauthorized action                   |
| `u101`     | Duplicate vote attempt                |
| `u102`     | Proposal not found                    |
| `u103`     | Voting period has ended               |
| `u104`     | Invalid title length                  |
| `u105`     | Invalid description length            |
| `u106`     | Invalid voting duration               |

## Contributing

Feel free to contribute to the VoteChain project by submitting issues or pull requests. Ensure contributions follow the code style and include tests for new features.

## License

This project is licensed under the MIT License.

---