# Redemption Exemption Functionality

## Overview

This merge request adds the ability to exempt specific troves from being redeemed during redemption operations. This provides governance with additional control over the redemption process, allowing them to protect certain troves from being liquidated through redemptions.

## Changes Made

### 1. GovernableVariables.sol
- Added `redemptionExemptAccounts` mapping to track exempt addresses
- Added redemption exemption functions following the same pattern as fee exemptions:
  - `addRedemptionExemptAccount(address _account)`
  - `addRedemptionExemptAccounts(address[] calldata _accounts)`
  - `removeRedemptionExemptAccount(address _account)`
  - `removeRedemptionExemptAccounts(address[] calldata _accounts)`
  - `isAccountRedemptionExempt(address _account)`
- Added corresponding events:
  - `RedemptionExemptAccountAdded(address _account)`
  - `RedemptionExemptAccountRemoved(address _account)`

### 2. IGovernableVariables.sol
- Updated interface to include all redemption exemption functions and events
- Maintains consistency with existing fee exemption interface

### 3. TroveManager.sol
- Modified `redeemCollateral()` function to check for redemption exemptions
- Added exemption check after ICR validation but before redemption processing
- Exempt troves are skipped during the redemption loop

### 4. Tests
- Added comprehensive test suite in `GoverableVariables.test.ts`
- Tests cover all redemption exemption functions
- Includes integration tests showing exemption behavior during redemptions
- Tests both adding and removing exemptions
- Verifies that exempt troves are not redeemed while non-exempt troves are

## Usage

### Adding Redemption Exemption
```solidity
// Add a single account to redemption exempt list
governableVariables.addRedemptionExemptAccount(address);

// Add multiple accounts to redemption exempt list
governableVariables.addRedemptionExemptAccounts([address1, address2, address3]);
```

### Removing Redemption Exemption
```solidity
// Remove a single account from redemption exempt list
governableVariables.removeRedemptionExemptAccount(address);

// Remove multiple accounts from redemption exempt list
governableVariables.removeRedemptionExemptAccounts([address1, address2, address3]);
```

### Checking Exemption Status
```solidity
// Check if an account is exempt from redemptions
bool isExempt = governableVariables.isAccountRedemptionExempt(address);
```

## Security Considerations

1. **Governance Only**: All redemption exemption functions are restricted to governance (council or treasury) only
2. **Consistent Pattern**: Follows the same security model as existing fee exemptions
3. **No Bypass**: Exempt troves are completely skipped during redemption, not just partially protected
4. **Reversible**: Exemptions can be removed at any time by governance

## Testing

The implementation includes comprehensive tests that verify:
- Basic functionality of adding/removing exemptions
- Integration with redemption process
- Proper skipping of exempt troves during redemptions
- Governance access control
- Error handling for edge cases

## Impact

- **Positive**: Provides governance with fine-grained control over redemption process
- **Neutral**: No impact on existing functionality for non-exempt troves
- **Risk**: Low - follows established patterns and includes comprehensive testing

## Migration

No migration required. The new functionality is additive and doesn't affect existing contracts or user interactions.

## Related Issues

This addresses the requirement to allow troves to be exempted from redemptions, providing governance with additional control mechanisms for the protocol.