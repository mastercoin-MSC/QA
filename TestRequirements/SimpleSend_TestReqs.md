# Simple Send

Transaction Type 0: [Simple Send](https://github.com/mastercoin-MSC/spec#transfer-coins-simple-send)

Each application under test (AUT) must adhere to [The Master Protocol / Mastercoin Complete Specification](https://github.com/mastercoin-MSC/spec/blob/master/README.md) and pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/marv-engine/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

The tests for Simple Send include:

1. user is able to enter valid values for all appropriate fields:
    * Currency identifier
    * Amount to transfer
    * Recipient address
    * fields for the Bitcoin protocol
1. valid input data is parsed and interpreted correctly, including all valid MSC Protocol transaction types in the blockchain that are supported by the AUT
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. correct Simple Send transactions are generated from valid test input data
1. runtime error conditions are detected and handled correctly (e.g. insufficient funds, application/network/OS failure)
1. all edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user

For each test sequence, start in a known state and return to a known state after the test is complete.

## Positive Tests - Valid
1. Create Simple Send message(s) with valid values for:
    * Currency identifier
    * Amount to transfer
    * Recipient address

## Negative Tests - Not valid
1. Attempt to create Simple Send message(s):
    * Currency identifier = 0 or any non-existent id
    * Amount to transfer = 0
    * Recipient address

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.

