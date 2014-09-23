# Participate in a Crowdsale

Transaction Type 0: [Simple Send](https://github.com/mastercoin-MSC/spec#simple-send) and Bitcoin Send

Each application under test (AUT) must adhere to [The Master Protocol / Mastercoin Complete Specification](https://github.com/mastercoin-MSC/spec/blob/master/README.md) and pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/marv-engine/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

The tests for Participate in a Crowdsale include:

1. user is able to enter valid values for all appropriate fields:
    * Currency ID
    * Amount
1. valid input data is parsed and interpreted correctly, including all valid MSC Protocol transaction types in the blockchain that are supported by the AUT
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. correct Create a Property with Fixed Number of Tokens transactions are generated from valid test input data
1. runtime error conditions are detected and handled correctly (e.g. insufficient funds, application/network/OS failure)
1. all edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user

For each test sequence, start in a known state and return to a known state after the test is complete. Run the tests separately and also simultaneously. The simultaneous tests should be run by the same users/addresses in the same roles where possible, and also by different users/addresses.

Where appropriate, tests should be run using the end-user UI and using the API directly.

## Positive Tests - Valid
### Create a Valid Simple Send 
1. U1: Create New Property Creation via Crowdsale with Variable number of Tokens message(s) with valid values 
1. U2: Create Simple Send message(s) with valid values for:
    * Currency identifier = Currency Identifier Desired for the crowdsale
    * Amount to transfer
    * U1 Recipient address
1. U1: See that
    * U1 no longer owns the amount transferred
    * U1 balance credited with the correct number of new tokens in the currency created by the crowdsale
    * U2 now owns the amount transferred
1. U2: See that
    * U1 no longer owns the amount transferred
    * U1 balance credited with the correct number of new tokens in the currency created by the crowdsale
    * U2 now owns the amount transferred

## Negative Tests - Not valid
### Attempt to Create an Incorrect Simple Send
1. U1: Attempt to create Simple Send message(s):
    * Currency identifier = 0 or any non-existent id or any id not owned by the address
    * Amount to transfer = 0
    * U2 Recipient address
1. U1: See that U1 still owns the amount
1. U2: See that U2 balance was not credited with the amount

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
