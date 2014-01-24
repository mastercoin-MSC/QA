# Simple Send

Transaction Type 0: [Simple Send](https://github.com/mastercoin-MSC/spec#transferring-mastercoins-simple-send)

Each application under test (AUT) must pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/marv-engine/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

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
1. edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.

(More words to come)
