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
There are many valid combinations of Crowdsale terms & conditions and participation in a crowdsale. Participation in a crowdsale does not require that the participant is credited with tokens from the crowdsale (e.g. the crowdsale is closed or never existed, the number of tokens to be credited is less than the minimum number of those tokens that can be transferred).

Positive tests should exercise as many combinations and conditions as possible, including both low and high ends of input value ranges, a mix of divisible and indivisible property types. Also, set up crowdsale terms and conditions where the participant (and issuer) receives fewer tokens than expected because of the limit on the total number of tokens in one currency that can be issued.

### Create a Valid Simple Send 
1. U1: Create New Property Creation via Crowdsale with Variable number of Tokens message(s) with valid values 
1. U2: Create Simple Send message(s) with valid values for:
    * Currency Identifier
    * Amount to Transfer
    * U1 Recipient address
1. U1: See that
    * U2 available balance debited by the Amount to Transfer value 
    * U2 available balance credited with the correct number of new tokens for the participant in the currency created by the crowdsale
    * U1 available balance credited with the amount transferred from the sender
    * U1 available balance credited with the correct number of new tokens for the issuer in the currency created by the crowdsale
1. U2: See that
    * U2 available balance debited by the Amount to Transfer value 
    * U2 available balance credited with the correct number of new tokens for the participant in the currency created by the crowdsale
    * U1 available balance credited with the amount transferred from the sender
    * U1 available balance credited with the correct number of new tokens for the issuer in the currency created by the crowdsale

## Negative Tests - Invalid
These tests are the same as the Negative Tests for Simple Send.
### Attempt to Create an Incorrect Simple Send
1. U1: Attempt to create Simple Send message(s):
    * Currency identifier = 0 or any non-existent id or any id not owned by the address
    * Amount to transfer = 0 or exceeds the number owned and available by the address
    * U2 Recipient address
1. U1: See that U1 balances have not changed (except BTC transaction fees)
1. U1: See that U2 balances have not changed
1. U2: See that U1 balances have not changed (except BTC transaction fees)
1. U2: See that U2 balances have not changed

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
