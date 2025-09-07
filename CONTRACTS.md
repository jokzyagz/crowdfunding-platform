# Smart Contract Documentation

## Overview

This repository contains two primary smart contracts that power the decentralized crowdfunding platform:

1. **Campaign Registry (`campaign-registry.clar`)** - Manages campaign lifecycle, metadata, and tracking
2. **Fund Distribution (`fund-distribution.clar`)** - Handles financial transactions, escrow, and reward distribution

## Campaign Registry Contract

### Purpose
The Campaign Registry contract serves as the central registry for all crowdfunding campaigns. It manages campaign creation, status updates, milestone tracking, and provides comprehensive campaign metadata storage.

### Key Features

#### Campaign Management
- **Campaign Creation**: Create new campaigns with comprehensive metadata
- **Status Management**: Track campaign lifecycle (Draft, Active, Funded, Failed, Cancelled, Completed)
- **Category Organization**: Organize campaigns by predefined categories (Tech, Creative, Social, etc.)
- **Creator Authorization**: Ensure only campaign creators can modify their campaigns

#### Data Structures
- **Campaigns Map**: Stores complete campaign information
- **Campaign Milestones**: Tracks progress milestones with achievement status
- **Campaign Updates**: Maintains campaign update history
- **User-Campaign Mapping**: Links users to their created campaigns
- **Category-Campaign Mapping**: Enables category-based filtering

#### Public Functions

##### Core Campaign Functions
- `create-campaign`: Initialize a new crowdfunding campaign
- `update-campaign-status`: Change campaign status with validation
- `add-milestone`: Add progress milestones to campaigns
- `add-campaign-update`: Post updates to campaign backers

##### Administrative Functions
- `update-raised-amount`: Update funding totals (called by fund-distribution)
- `update-supporter-count`: Track backer numbers
- `set-platform-fee-rate`: Configure platform fees
- `emergency-pause-campaign`: Emergency campaign suspension

##### Read-Only Functions
- `get-campaign`: Retrieve complete campaign details
- `get-milestone`: Get specific milestone information
- `get-platform-stats`: Platform-wide statistics
- `is-user-campaign-creator`: Verify campaign ownership

### Campaign Status Flow
```
DRAFT → ACTIVE → FUNDED/FAILED/CANCELLED
                ↓
            COMPLETED
```

## Fund Distribution Contract

### Purpose
The Fund Distribution contract handles all financial aspects of crowdfunding including contributions, escrow management, milestone-based fund releases, reward distribution, and refund processing.

### Key Features

#### Financial Management
- **Contribution Processing**: Accept and track STX contributions
- **Platform Fee Calculation**: Automatic fee deduction (2.5% default)
- **Escrow Services**: Secure fund holding until milestone completion
- **Milestone Releases**: Controlled fund distribution based on progress
- **Refund Processing**: Handle contributor refund requests

#### Reward System
- **Reward Tiers**: Create contribution-based reward levels
- **Reward Claims**: Allow backers to claim earned rewards
- **Delivery Tracking**: Manage reward fulfillment status

#### Data Structures
- **Campaign Funds**: Track financial status per campaign
- **Contributions**: Individual contributor records
- **Reward Tiers**: Structured reward offerings
- **Milestone Funds**: Milestone-based release tracking
- **Refund Requests**: Refund management system
- **Escrow Accounts**: Secure fund custody

#### Public Functions

##### Contribution Functions
- `initialize-campaign-funding`: Set up campaign financial structure
- `contribute-to-campaign`: Process STX contributions
- `request-refund`: Request contribution refunds
- `process-refund`: Execute approved refunds

##### Reward Functions
- `create-reward-tier`: Define reward levels for campaigns
- `claim-reward`: Allow backers to claim rewards

##### Fund Management
- `release-milestone-funds`: Release funds upon milestone completion
- `approve-refund-request`: Administrative refund approval

##### Administrative Functions
- `set-platform-fee-rate`: Adjust platform fees
- `set-minimum-contribution`: Set minimum contribution thresholds
- `toggle-emergency-pause`: Emergency system pause
- `withdraw-platform-fees`: Platform fee collection

##### Read-Only Functions
- `get-campaign-funds`: Campaign financial summary
- `get-contribution`: Individual contribution details
- `get-reward-tier`: Reward tier information
- `get-platform-financial-stats`: Platform financial metrics

## Security Features

### Authorization Controls
- Contract owner privileges for administrative functions
- Campaign creator restrictions for campaign modifications
- Contributor authorization for refund requests

### Input Validation
- Minimum contribution requirements
- Valid category and status checks
- Proper milestone target validation
- Emergency pause mechanisms

### Financial Security
- Escrow-based fund holding
- Platform fee calculations with limits
- Secure STX transfer operations
- Dispute resolution framework

## Integration Patterns

### Contract Interaction
The contracts are designed to work together:
1. Campaign Registry manages campaign metadata and status
2. Fund Distribution handles all financial operations
3. Cross-contract calls update campaign statistics

### External Integration
- **Frontend Applications**: Read-only functions for UI display
- **Analytics Services**: Platform statistics and metrics
- **Notification Systems**: Campaign update and milestone tracking

## Deployment Configuration

### Required Environment
- Stacks blockchain (Clarity smart contracts)
- Clarinet development framework
- Node.js environment for testing

### Deployment Steps
1. Configure Clarinet.toml with contract definitions
2. Run `clarinet check` for syntax validation
3. Execute test suite with `clarinet test`
4. Deploy to testnet for integration testing
5. Deploy to mainnet for production use

## Error Codes

### Campaign Registry Errors
- `u1000`: Unauthorized access
- `u1001`: Campaign not found
- `u1002`: Invalid campaign data
- `u1004`: Invalid status transition
- `u1006`: Insufficient funding goal
- `u1007`: Invalid campaign duration

### Fund Distribution Errors
- `u2000`: Unauthorized access
- `u2001`: Campaign not found
- `u2002`: Insufficient balance
- `u2003`: Contribution too small
- `u2006`: Refund not available
- `u2012`: Reward not found
- `u2015`: Escrow locked

## Testing Framework

### Unit Tests
- Individual function validation
- Edge case handling
- Error condition testing
- Authorization verification

### Integration Tests
- Cross-contract interactions
- End-to-end workflows
- Platform fee calculations
- Milestone progression

### Performance Tests
- Gas optimization validation
- Large dataset handling
- Concurrent operation testing

## Future Enhancements

### Planned Features
- Multi-token support (SIP-10 tokens)
- Advanced governance mechanisms
- Automated milestone verification
- Enhanced dispute resolution
- Dynamic fee structures

### Scalability Improvements
- Batch operation support
- Optimized data structures
- Reduced gas consumption
- Enhanced query capabilities

## Support and Maintenance

### Documentation Updates
This documentation will be updated with each contract version to reflect new features, bug fixes, and performance improvements.

### Community Contributions
We welcome community feedback and contributions. Please review the contribution guidelines in the main README.md file.

### Issue Reporting
For bugs, feature requests, or security concerns, please create issues in the GitHub repository with appropriate labels and detailed descriptions.
