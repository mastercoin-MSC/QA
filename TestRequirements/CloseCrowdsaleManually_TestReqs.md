# Close a Crowdsale Manually

Transaction Type 53: [Close a Crowdsale Manually](https://github.com/mastercoin-MSC/spec#close-a-crowdsale-manually)

Each application under test (AUT) must adhere to [The Master Protocol / Mastercoin Complete Specification](https://github.com/mastercoin-MSC/spec/blob/master/README.md) and pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/mastercoin-MSC/MasterProtocolTestPlan.md#major-items--scenarios-to-be-tested).

The tests for Close a Crowdsale Manually include:

1. user is able to enter a valid value for:
    * Property identifier
1. valid input data is parsed and interpreted correctly, including all valid MSC Protocol transaction types in the blockchain that are supported by the AUT
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. correct Close a Crowdsale Manually transactions are generated from valid test input data
1. runtime error conditions are detected and handled correctly (e.g. insufficient funds, application/network/OS failure)
1. all edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user

For each test sequence, start in a known state and return to a known state after the test is complete. Run the tests separately and also simultaneously. The simultaneous tests should be run by the same users/addresses in the same roles where possible, and also by different users/addresses.

Where appropriate, tests should be run using the end-user UI and using the API directly.

## Positive Tests - Valid
### Close a Crowdsale Manually 
1. U1: Create Close a Crowdsale Manually message(s) with valid values for:
    * Property identifier
1. U1: See that the Crowdsale is no longer active
1. U2: See that the Crowdsale is no longer active

## Negative Tests - Not valid
### Attempt to Create an Incorrect Close a Crowdsale Manually message
1. U1: Attempt to create Close a Crowdsale Manually message(s):
    * Property identifier = 0, 1, 2 or any non-existent id or a Property identifier owned by another address
1. U1: See that the Crowdsale is still active
1. U2: See that the Crowdsale is still active

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
