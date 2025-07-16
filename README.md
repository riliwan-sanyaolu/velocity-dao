# VelocityDAO - Community-Driven Investment Protocol

[![Stacks](https://img.shields.io/badge/Stacks-Blockchain-orange)](https://stacks.co)
[![Clarity](https://img.shields.io/badge/Language-Clarity-blue)](https://clarity-lang.org)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

## Overview

VelocityDAO is a sophisticated decentralized autonomous organization built on the Stacks blockchain that empowers communities to collectively manage investment funds through transparent governance mechanisms, time-locked deposits, and democratic proposal execution.

The protocol revolutionizes collective investment by providing a trustless framework where community members can pool resources, participate in governance, and execute investment strategies through democratic consensus. Each participant gains voting power proportional to their contribution, ensuring fair representation while maintaining robust protection against malicious actors.

## Key Features

- **🏛️ Democratic Governance**: Weighted voting system based on stake contribution
- **🔒 Time-locked Deposits**: Security through mandatory lock periods
- **💼 Investment Proposals**: Community-driven investment decision making
- **🎯 Multi-stage Lifecycle**: Comprehensive proposal validation and execution
- **⚖️ Fair Representation**: Voting power proportional to stake
- **🛡️ Security Measures**: Protection against malicious actors and double voting

## System Architecture

### Core Components

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Governance    │    │   Deposit       │    │   Proposal      │
│   System        │    │   Management    │    │   Lifecycle     │
│                 │    │                 │    │                 │
│ • Weighted Vote │    │ • STX Deposits  │    │ • Create        │
│ • Token Balance │    │ • Token Minting │    │ • Vote          │
│ • Voting Power  │    │ • Lock Periods  │    │ • Execute       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                        │                        │
         └────────────────────────┼────────────────────────┘
                                  │
                        ┌─────────▼─────────┐
                        │  VelocityDAO      │
                        │  Smart Contract   │
                        │                   │
                        │ • Error Handling  │
                        │ • Access Control  │
                        │ • State Management│
                        └───────────────────┘
```

### Contract Architecture

The VelocityDAO contract is structured around four main functional areas:

#### 1. **Governance Layer**

- **Token-based Voting**: Users receive governance tokens equal to their STX deposits
- **Weighted Decisions**: Voting power scales with token holdings
- **Anti-manipulation**: Prevents double voting and unauthorized participation

#### 2. **Asset Management**

- **Deposit System**: STX deposits are locked for security periods
- **Token Economics**: 1:1 ratio between deposited STX and governance tokens
- **Withdrawal Protection**: Time-locked withdrawals prevent rapid exit attacks

#### 3. **Proposal System**

- **Creation Requirements**: Only token holders can create proposals
- **Validation Framework**: Comprehensive input validation and duration limits
- **Execution Logic**: Automated execution for approved proposals

#### 4. **Security Framework**

- **Access Control**: Owner-only initialization and administrative functions
- **Input Validation**: Extensive error checking and parameter validation
- **State Protection**: Immutable execution states and vote recording

## Data Flow

### Deposit Flow

```
User STX → Contract Validation → STX Transfer → Token Minting → Lock Period Set
```

### Proposal Flow

```
Create Proposal → Validation → Voting Period → Vote Counting → Execution (if approved)
```

### Governance Flow

```
Token Balance → Voting Power Calculation → Weighted Vote → Proposal Decision
```

## Contract Interface

### Public Functions

#### Core Operations

- `initialize()` - Initialize the DAO contract (owner only)
- `deposit(amount: uint)` - Deposit STX and receive governance tokens
- `withdraw(amount: uint)` - Withdraw STX after lock period expires

#### Governance Functions

- `create-proposal(description, amount, target, duration)` - Create new investment proposal
- `vote(proposal-id, vote-for)` - Vote on active proposals with weighted voting
- `execute-proposal(proposal-id)` - Execute approved proposals

#### Read-Only Functions

- `get-balance(account)` - Get user's governance token balance
- `get-total-supply()` - Get total supply of governance tokens
- `get-proposal(proposal-id)` - Get proposal details by ID
- `get-deposit-info(account)` - Get user's deposit information
- `get-vote(proposal-id, voter)` - Get user's vote on specific proposal

## Protocol Parameters

| Parameter | Value | Description |
|-----------|--------|-------------|
| Minimum Deposit | 1,000,000 μSTX | Minimum required deposit amount |
| Lock Period | 1,440 blocks (~10 days) | Mandatory lock period for deposits |
| Minimum Duration | 144 blocks (~1 day) | Minimum proposal voting period |
| Maximum Duration | 20,160 blocks (~14 days) | Maximum proposal voting period |

## Error Codes

| Code | Error | Description |
|------|-------|-------------|
| u100 | `err-owner-only` | Function restricted to contract owner |
| u101 | `err-not-initialized` | Contract not initialized |
| u102 | `err-already-initialized` | Contract already initialized |
| u103 | `err-insufficient-balance` | Insufficient token balance |
| u104 | `err-invalid-amount` | Invalid amount provided |
| u105 | `err-unauthorized` | Unauthorized access attempt |
| u106 | `err-proposal-not-found` | Proposal does not exist |
| u107 | `err-proposal-expired` | Proposal voting period expired |
| u108 | `err-already-voted` | User already voted on proposal |
| u109 | `err-below-minimum` | Amount below minimum requirement |
| u110 | `err-locked-period` | Funds still in lock period |

## Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) - Stacks development tool
- [Node.js](https://nodejs.org/) (v16 or higher)
- [Stacks Wallet](https://wallet.hiro.so/) for interaction

### Installation

1. Clone the repository:

```bash
git clone https://github.com/riliwan-sanyaolu/velocity-dao.git
cd velocity-dao
```

2. Install dependencies:

```bash
npm install
```

3. Check contract syntax:

```bash
clarinet check
```

4. Run tests:

```bash
npm test
```

### Development

The project uses Clarinet for smart contract development and testing:

- **Contract Code**: `contracts/velocity-dao.clar`
- **Tests**: `tests/velocity-dao.test.ts`
- **Configuration**: `Clarinet.toml`

### Testing

Run the test suite to verify contract functionality:

```bash
# Check contract syntax
clarinet check

# Run unit tests
npm test

# Run specific test file
npm test velocity-dao.test.ts
```

## Usage Examples

### Depositing STX

```clarity
;; Deposit 5 STX to the DAO
(contract-call? .velocity-dao deposit u5000000)
```

### Creating a Proposal

```clarity
;; Create investment proposal
(contract-call? .velocity-dao create-proposal 
  "Invest in DeFi protocol" 
  u2000000 
  'SP2...' 
  u1440)
```

### Voting on Proposals

```clarity
;; Vote yes on proposal #1
(contract-call? .velocity-dao vote u1 true)
```

## Security Considerations

### Implemented Protections

- **Time-locked Deposits**: Prevents rapid exit attacks
- **Weighted Voting**: Proportional representation based on stake
- **Double Vote Prevention**: Users cannot vote multiple times on same proposal
- **Input Validation**: Comprehensive parameter checking
- **Access Control**: Restricted administrative functions

### Best Practices

- Always verify proposal details before voting
- Understand lock periods before depositing
- Monitor proposal execution status
- Participate actively in governance decisions

## Contributing

We welcome contributions to VelocityDAO! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow Clarity best practices
- Add comprehensive tests for new features
- Update documentation for any interface changes
- Ensure all tests pass before submitting PR

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

- **Project Maintainer**: [Riliwan Sanyaolu](https://github.com/riliwan-sanyaolu)
- **Issues**: [GitHub Issues](https://github.com/riliwan-sanyaolu/velocity-dao/issues)
- **Discussions**: [GitHub Discussions](https://github.com/riliwan-sanyaolu/velocity-dao/discussions)

## Acknowledgments

- Built on [Stacks](https://stacks.co) blockchain
- Powered by [Clarity](https://clarity-lang.org) smart contract language
- Development tools by [Hiro](https://hiro.so)
