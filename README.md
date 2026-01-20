# TokenVault UUPS Proxy System

Production-grade upgradeable smart contract system implementing the UUPS (Universal Upgradeable Proxy Standard) Pattern with comprehensive state management, access control, and business logic.

## Project Overview

This project demonstrates a complete implementation of an upgradeable smart contract system with three progressive versions:

- **TokenVaultV1**: Basic deposit/withdraw functionality with fee management
- **TokenVaultV2**: Adds yield generation and pause/unpause capabilities
- **TokenVaultV3**: Introduces withdrawal delays and emergency withdrawal mechanisms

## Directory Structure

```
├── contracts/
│   ├── TokenVaultV1.sol
│   ├── TokenVaultV2.sol
│   ├── TokenVaultV3.sol
│   └── mocks/
│       └── MockERC20.sol
├── test/
│   ├── TokenVaultV1.test.js
│   ├── upgrade-v1-to-v2.test.js
│   ├── upgrade-v2-to-v3.test.js
│   └── security.test.js
├── scripts/
│   ├── deploy-v1.js
│   ├── upgrade-to-v2.js
│   └── upgrade-to-v3.js
├── hardhat.config.js
├── package.json
├── submission.yml
└── README.md
```

## Installation

```bash
npm install
```

## Compilation

```bash
npx hardhat compile
```

## Running Tests

```bash
npx hardhat test
```

## Key Features

### Storage Layout Management
- Proper storage gaps to allow future upgrades
- Consistent ordering of state variables across versions
- Prevention of storage collisions

### Security
- Initializer protection using OpenZeppelin's initializer modifier
- Role-based access control with DEFAULT_ADMIN_ROLE, UPGRADER_ROLE, PAUSER_ROLE
- Prevents reinitialization attacks
- Authorized upgrade mechanism only

### Business Logic
- Deposit fees calculated and deducted from user balance
- Yield calculations based on time elapsed and balance
- Withdrawal delay enforcement
- Emergency withdrawal capability

## Contract Functions

### TokenVaultV1
- `initialize(address _token, address _admin, uint256 _depositFee)`
- `deposit(uint256 amount)`
- `withdraw(uint256 amount)`
- `balanceOf(address user) returns (uint256)`
- `totalDeposits() returns (uint256)`
- `getDepositFee() returns (uint256)`
- `getImplementationVersion() returns (string)`

### TokenVaultV2 (Extends V1)
- `setYieldRate(uint256 _yieldRate)`
- `getYieldRate() returns (uint256)`
- `claimYield() returns (uint256)`
- `getUserYield(address user) returns (uint256)`
- `pauseDeposits()`
- `unpauseDeposits()`
- `isDepositsPaused() returns (bool)`

### TokenVaultV3 (Extends V2)
- `emergencyWithdraw() returns (uint256)`
- `setWithdrawalDelay(uint256 _delaySeconds)`
- `getWithdrawalDelay() returns (uint256)`
- `requestWithdrawal(uint256 amount)`
- `executeWithdrawal() returns (uint256)`
- `getWithdrawalRequest(address user) returns (uint256, uint256)`

## Deployment

### Deploy V1
```bash
npx hardhat run scripts/deploy-v1.js
```

### Upgrade to V2
```bash
npx hardhat run scripts/upgrade-to-v2.js
```

### Upgrade to V3
```bash
npx hardhat run scripts/upgrade-to-v3.js
```

## Testing Coverage

Comprehensive test coverage includes:
- Initialization and parameter validation
- Deposit/withdrawal functionality
- Fee calculations
- Yield calculations and claims
- Upgrade state preservation
- Access control enforcement
- Security vulnerability tests
- Edge case handling

## License

MIT
