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
1. Send to Owners
    * Currency Id = 1, 2, at least 2 smart properties (divis, indiv)
    * Amount to transfer <= the sender's available balance
        * For MSC & TMSC, Amount to transfer leaves enough to pay transfer fee
1. Confirm:
    * sending address Currency Id balance decremented by Amount to transfer
    * sending address MSC (or TMSC) balance decremented based on number of addresses that received payment
    * correct amounts transferred to the correct addresses

## Negative Tests - Not Valid

### Erroneous Message Field Data
1. Attempt to Send to Owners:
    * currency id = 0 (bitcoin)
    * a non-existent currency id
    * available balance = 0
    * Amount to transfer > available balance
    * Amount to transfer <= 0
    * insufficient MSC (or TMSC) to pay calculated transfer fee (based on number of addresses that would receive payment)

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
