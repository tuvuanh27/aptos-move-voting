# Voting Module

## Overview
The `Voting` module is a Move smart contract that facilitates a simple voting system. This module allows for the initialization of candidates, voting by multiple accounts, and declaring a winner based on the votes received. The module also includes several safety checks to ensure the integrity of the voting process.

## Structures

### CandidateList
Stores the list of candidates, their respective vote counts, and the declared winner.
- `candidate_list: SimpleMap<address, u64>`: A map of candidate addresses to their vote counts.
- `c_list: vector<address>`: A vector of candidate addresses.
- `winner: address`: The address of the winning candidate.

### VotingList
Stores the list of voters.
- `voters: SimpleMap<address, u64>`: A map of voter addresses to a flag indicating if they have voted.

## Error Codes
- `E_NOT_OWNER (0)`: The caller is not the owner.
- `E_IS_NOT_INITIALIZED (1)`: The voting system is not initialized.
- `E_DOES_NOT_CONTAIN_KEY (2)`: The map does not contain the specified key.
- `E_IS_INITIALIZED (3)`: The voting system is already initialized.
- `E_IS_INITIALIZED_WITH_CANDIDATE (4)`: The candidate is already initialized.
- `E_WINNER_DECLARED (5)`: The winner has already been declared.
- `E_HAS_VOTED (6)`: The voter has already voted.

## Public Functions

### `assert_is_owner`
Ensures that the caller is the owner of the module.
- `addr: address`: The address to check.

### `assert_is_initialized`
Ensures that the voting system is initialized.
- `addr: address`: The address to check.

### `assert_uninitialized`
Ensures that the voting system is not initialized.
- `addr: address`: The address to check.

### `assert_contains_key`
Ensures that the specified key exists in the map.
- `map: &SimpleMap<address, u64>`: The map to check.
- `addr: &address`: The key to check.

### `assert_not_contains_key`
Ensures that the specified key does not exist in the map.
- `map: &SimpleMap<address, u64>`: The map to check.
- `addr: &address`: The key to check.

### `initialize_with_candidate`
Initializes the voting system with a candidate.
- `acc: &signer`: The signer account.
- `c_addr: address`: The candidate address.

### `add_candidate`
Adds a candidate to the voting system.
- `acc: &signer`: The signer account.
- `c_addr: address`: The candidate address.

### `vote`
Allows a voter to vote for a candidate.
- `acc: &signer`: The voter account.
- `c_addr: address`: The candidate address.
- `store_addr: address`: The address of the voting store.

### `declare_winner`
Declares the candidate with the highest votes as the winner.
- `acc: &signer`: The signer account.

## Testing

### `test_flow`
Tests the overall flow of the voting system.
- `admin: signer`: The admin account.

### `test_declare_winner`
Tests declaring the winner.
- `admin: signer`: The admin account.

### `test_initialize_with_candidate_not_owner`
Tests initialization by a non-owner.
- `admin: signer`: The admin account.

### `test_initialize_with_same_candidate`
Tests initializing the voting system with the same candidate twice.
- `admin: signer`: The admin account.

### `test_vote_twice`
Tests voting twice by the same voter.
- `admin: signer`: The admin account.

### `test_vote_not_initialized`
Tests voting before the system is initialized.
- `admin: signer`: The admin account.

### `test_add_candidate_after_winner_declared`
Tests adding a candidate after the winner is declared.
- `admin: signer`: The admin account.

## Usage
To use this module, follow these steps:
1. Initialize the voting system with an initial candidate using `initialize_with_candidate`.
2. Add additional candidates using `add_candidate`.
3. Allow users to vote for their preferred candidate using `vote`.
4. Declare the winner using `declare_winner`.

Ensure that all safety checks and assertions are satisfied to maintain the integrity of the voting process.
