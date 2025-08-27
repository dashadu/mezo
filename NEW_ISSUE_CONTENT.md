# Improve Deployment Scripts for Version Management and Network-Specific Deployments

## Summary
Update the current deployment scripts to support conditional deployments, version management, and better network-specific configurations as outlined in `solidity/FIXME.md`.

## Problem Description
Currently, the deployment scripts have several limitations that make deployments less flexible and harder to manage:

1. **Lack of conditional deployments** - Scripts don't differentiate between TroveManager and TroveManagerTester based on network requirements
2. **No version-based deployment** - Deployments are not organized by version numbers, making it difficult to track and manage different contract versions
3. **Network configuration issues** - Deployment artifacts are not properly organized by network, making multi-network deployments cumbersome

## Current State
From `solidity/FIXME.md`, the following issues are identified:
- Add conditional deployments for TroveManager / TroveManagerTester for networks
- Update to deploy by version number and network

## Proposed Solution

### 1. Conditional Network Deployments
- Implement logic to deploy different contract variants based on the target network
- Use TroveManagerTester for test networks (matsnet, testnet)
- Use TroveManager for production networks (mainnet)

### 2. Version-Based Organization
- Structure deployments to include version numbers in the deployment artifacts
- Create a versioning strategy that aligns with the project's release cycle
- Ensure deployment artifacts are tagged with appropriate version metadata

### 3. Enhanced Network Configuration
- Improve network-specific deployment configurations
- Ensure proper artifact organization in the `deployments/` directory
- Add validation to prevent accidental deployments to wrong networks

## Acceptance Criteria

- [ ] Deployment scripts conditionally deploy TroveManager vs TroveManagerTester based on network type
- [ ] Deployment artifacts are organized by version and network
- [ ] Clear documentation on how to deploy to different networks with different configurations
- [ ] Deployment process includes version tagging and validation
- [ ] Tests validate that correct contracts are deployed for each network type
- [ ] Updated README.md with new deployment instructions

## Technical Implementation Notes

### Files to Modify
- Deployment scripts in `solidity/deploy/` directory
- Network configuration files
- `solidity/FIXME.md` (remove items once completed)
- `README.md` deployment section

### Testing Requirements
- Verify deployments work correctly for different networks
- Ensure deployment artifacts are properly structured
- Test that version information is correctly embedded in deployments

## Priority
**Medium** - This improvement will enhance deployment reliability and maintainability, which is important for production deployments and development workflow.

## Labels
- `enhancement`
- `deployment`
- `infrastructure`
- `good first issue` (for developers familiar with Hardhat deployments)

---

*This issue is based on the identified improvements in `solidity/FIXME.md` and aims to enhance the deployment process for better version management and network-specific configurations.*