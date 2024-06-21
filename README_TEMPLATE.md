# VotingDApp

## Overview

VotingDApp is a simple decentralized application (dApp) built on the Ethereum blockchain that facilitates a secure and transparent voting process. The contract allows an administrator to register candidates and authorize voters, while voters can cast their votes for their preferred candidates. The results of the election are recorded and can be concluded by the administrator, ensuring that the voting process is both fair and verifiable.

## Table of Contents

- [Features](#features)
- [Contract Details](#contract-details)
  - [Structs](#structs)
  - [State Variables](#state-variables)
  - [Events](#events)
  - [Modifiers](#modifiers)
- [Functions](#functions)
- [Error Handling](#error-handling)
- [Usage](#usage)
- [Development](#development)
  - [Setting Up](#setting-up)

## Features

- **Admin Functions**: 
  - Register new candidates.
  - Authorize voters.
  - Conclude the election.

- **Voter Functions**: 
  - Cast a vote for a registered candidate.
  
- **Security**:
  - Ensure only authorized voters can vote.
  - Prevent voters from voting more than once.
  - Validate candidate IDs before voting.

## Contract Details

### Structs

- **Candidate**: 
  - `id`: Unique identifier for the candidate.
  - `name`: Name of the candidate.
  - `voteCount`: Number of votes received.

- **Voter**: 
  - `isAuthorized`: Whether the voter is authorized to vote.
  - `hasVoted`: Whether the voter has already voted.
  - `candidateIdVotedFor`: The ID of the candidate the voter voted for.

### State Variables

- **electionAdmin**: Address of the contract deployer (election administrator).
- **electionTitle**: Title of the election.
- **voterRegistry**: Mapping of voter addresses to their Voter structs.
- **candidateList**: Array of candidates.
- **voteCount**: Total number of votes cast.

### Events

- **VoteReceived**: Emitted when a vote is cast, logging the candidate's name and their updated vote count.
- **ElectionConcluded**: Emitted at the end of the election, logging each candidate's name and their final vote count.

### Modifiers

- **onlyAdmin**: Ensures that only the administrator can call certain functions.

## Functions

- **registerCandidate**: 
  - Adds a new candidate to the election.
  - Can only be called by the administrator.

- **authorizeVoter**: 
  - Authorizes a voter to participate in the election.
  - Can only be called by the administrator.

- **castVote**: 
  - Allows an authorized voter to cast their vote for a candidate.
  - Validates the voter's authorization, vote status, and candidate ID before allowing the vote.

- **concludeElection**: 
  - Ends the election and emits the results.
  - Ensures the integrity of the vote count using an `assert` statement.
  - Resets vote counts for future elections.

## Error Handling

- **revert**: Used to handle specific error conditions with custom error messages, such as:
  - Voter is already authorized.
  - Voter is not authorized to vote.
  - Voter has already voted.
  - Invalid candidate ID.

- **require**: Ensures that certain conditions are met before executing functions, primarily used to restrict access to administrator-only functions.

- **assert**: Used to validate internal errors and invariants, ensuring that the total votes counted match the sum of individual candidate votes.

## Usage

1. **Deploy the Contract**: The contract is deployed by the election administrator who initializes the election with a title.
2. **Register Candidates**: The administrator registers candidates using the `registerCandidate` function.
3. **Authorize Voters**: The administrator authorizes voters using the `authorizeVoter` function.
4. **Cast Votes**: Authorized voters cast their votes using the `castVote` function.
5. **Conclude Election**: The administrator concludes the election using the `concludeElection` function, which emits the results and resets the vote counts for future elections.

## Development

To develop and test the VotingDApp, you can do it in Remix IDE or will need the following tools:

- Solidity: Programming language for writing smart contracts.
- Ethereum: Blockchain platform to deploy the contract.
- Truffle: Development framework for Ethereum.
- Ganache: Personal blockchain for Ethereum development.
- MetaMask: Browser extension for interacting with Ethereum.
