## Purpose
The `challenged_proposal.gate` monitor is designed to ensure the liveness of the fault proof system. It detects situations where the Challenger (`honestChallenger`), assumed to be operating honestly, challenges a state output root proposed by the Proposer (`honestProposer`), who is also assumed to be honest.

Such an event indicates a critical issue—potentially a bug in the fault proof smart contracts or offchain components—that could compromise the system's ability to progress. Detecting this scenario promptly is essential to maintain the integrity and reliability of the network.

## Technical Overview

### How It Works

- **Monitoring Dispute Games**: The monitor observes active dispute games involving state output roots proposed by the `honestProposer`.

- **Identifying Claims**:
  - **Root Claim**: The initial claim in a dispute game made by the `honestProposer`.
  - **Subsequent Moves**: Claims made by participants in response to the root claim.

- **Analyzing Challenges**:
  - **Parent Index**: In the dispute game, each claim has a `parentIndex` indicating its relationship to previous claims.
    - **Even `parentIndex`**: Represents an attack against the parent claim.
    - **Odd `parentIndex`**: Represents a defense of the parent claim.

  The monitor checks if the `honestChallenger` has made an attack (even `parentIndex`) against the root claim proposed by the `honestProposer`.

- **Triggering Alerts**:
  - If such an attack is detected, it implies that the `honestChallenger` is challenging a correct proposal from the `honestProposer`.
  - This situation indicates a potential issue affecting the system's liveness.
  - The monitor raises an alert for immediate investigation.

## Importance of the Monitor

- **Ensuring Liveness**: The fault proof system relies on honest actors progressing the dispute games correctly. An honest challenger attacking an honest proposer disrupts this process.
- **Detecting Bugs Early**: Such behavior may result from bugs in the fault proof smart contracts or offchain components.
- **Maintaining Network Integrity**: Ensures that the network operates smoothly without disruptions due to internal conflicts.

## Parameters

- `honestChallenger`: Address of the Challenger.
- `honestProposer` : Address of the Proposer.
- `disputeGame`: Address of the dispute game contract being monitored.
