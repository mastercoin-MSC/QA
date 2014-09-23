# P2SH

Pay to Script Hash: []()

Each application under test (AUT) must pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/mastercoin-MSC/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

The tests for P2SH include:

1. each transaction produces behavior and results that are demonstrably the same for P2SH addresses per the BIP-16 Protocol, as for conventional addresses
1. user is able to enter valid values for all appropriate fields:
    * Currency identifier
    * Amount to transfer
1. valid input data is parsed and interpreted correctly, including all valid MSC Protocol transaction types in the blockchain that are supported by the AUT
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. correct Send to Owners transactions are generated from valid test input data
1. runtime error conditions are detected and handled correctly (e.g. insufficient funds, application/network/OS failure)
1. all edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user

For each test sequence, start in a known state and return to a known state after the test is complete. Run the tests separately and also simultaneously. The simultaneous tests should be run by the same users/addresses in the same roles where possible, and also by different users/addresses.

Where appropriate, tests should be run using the end-user UI and using the API directly.

## Positive Tests - Valid
For all positive tests, 
* each step must succeed with correct results, and

### Basic P2SH Tests with Existing Transaction Types
1. U1: Use a P2SH as one of the Recipient Addresses
1. U1, U2: Confirm:
    * sending address Currency Id available balance decremented by Amount to transfer
    * P2SH address Currency Id available balance incremented by Amount to transfer
    
1. U1: Use a P2SH as the Sending Addresses
1. U1, U2: Confirm:
    * P2SH address Currency Id available balance decremented by Amount to transfer
    * receiving address Currency Id available balance incremented by Amount to transfer
    
## Negative Tests - Not Valid
The message must be detected as invalid, with no changes made to any MP balances.

### Erroneous Message Field Data (each condition is individually invalid)


The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
