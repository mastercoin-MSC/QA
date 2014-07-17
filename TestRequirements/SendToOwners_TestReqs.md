# Send to Owners

Transaction Type 3: [Send to Owners](https://github.com/mastercoin-MSC/spec#send-to-owners)

Each application under test (AUT) must pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/mastercoin-MSC/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

The tests for Send to Owners include:

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
For the positive tests, each step must succeed - with correct results. 
### Basic Send to Owners
1. U1: Send to Owners
    * Currency Id = 1, 2, at least 2 smart properties (divis, indiv)
    * Amount to transfer <= the sender's available balance
        * For MSC & TMSC, Amount to transfer leaves enough in balance to pay transfer fee
1. U1, U2: Confirm:
    * sending address Currency Id available balance decremented by Amount to transfer
    * sending address MSC (or TMSC) balance decremented based on number of addresses that received payment
    * correct amounts added to available balance of the correct addresses (rounding up to nearest unit, smaller owners receive 0 if Amount to transfer consumed in payments to larger owners)

### Send to Owners that have reserved balances
1. U1: Send to Owners
    * Currency Id = 1, 2, at least 2 smart properties (divis, indiv)
    * Amount to transfer <= the sender's available balance
        * For MSC & TMSC, Amount to transfer leaves enough in balance to pay transfer fee
1. U1, U2: Confirm:
    * sending address Currency Id available balance decremented by Amount to transfer
    * sending address MSC (or TMSC) balance decremented based on number of addresses that received payment
    * correct amounts added to available balance of the correct addresses (rounding up to nearest unit, smaller owners receive 0 if Amount to transfer consumed in payments to larger owners)
        * reserved balances unchanged for all addresses involved

### Only largest owner receives tokens
1. U1: Send to Owners
    * Amount to transfer = 1 for indiv, .00000001 for divis token
    * More than 1 owner
1. U1, U2: Confirm
    * Only largest owner receives the Amount to transfer, others receive 0
    * .00000001 MSC (or TMSC) transfer fee deducted from sender's balance

## Negative Tests - Not Valid
### Erroneous Message Field Data (each condition is individually invalid)
1. U1: Attempt to Send to Owners:
    * currency id = 0 (bitcoin)
    * a non-existent currency id
    * available balance = 0
    * Amount to transfer > sender's available balance
    * Amount to transfer <= 0
    * insufficient MSC (or TMSC) to pay calculated transfer fee (based on number of addresses that would receive payment)
1. U1, U2: Confirm, for each condition
    * transaction message was invalid
    * All owners' addresses still own the same number of tokens
    * 0 transfer fee deducted from sender's MSC (or TMSC) balance

### Sender owns all the tokens
1. U1: Attempt to Send to Owners:
    * Sender's address owns all the tokens
    * Amount to transfer <= sender address's balance
1. U1, U2: Confirm
    * transaction message was invalid
    * Sender's address still owns the same number of tokens
    * 0 transfer fee deducted from sender's MSC (or TMSC) balance

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
