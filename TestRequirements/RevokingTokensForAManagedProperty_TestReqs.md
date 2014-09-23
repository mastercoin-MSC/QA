# Revoking Tokens for a Managed Property

Transaction Type 56: [Revoking Tokens for a Managed Property](https://github.com/mastercoin-MSC/spec#granting-tokens-for-a-managed-property)

Each application under test (AUT) must adhere to [The Master Protocol / Mastercoin Complete Specification](https://github.com/mastercoin-MSC/spec/blob/master/README.md) and pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/marv-engine/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

The tests for Revoking Tokens for a Managed Property include:

1. user is able to enter valid values for all appropriate fields:
    * Property ID
    * Number Properties
    * Memo
1. valid input data is parsed and interpreted correctly, including all valid MSC Protocol transaction types in the blockchain that are supported by the AUT
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. correct Create a Property with Fixed Number of Tokens transactions are generated from valid test input data
1. runtime error conditions are detected and handled correctly (e.g. insufficient funds, application/network/OS failure)
1. all edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user

For each test sequence, start in a known state and return to a known state after the test is complete. Run the tests separately and also simultaneously. The simultaneous tests should be run by the same users/addresses in the same roles where possible, and also by different users/addresses.

Where appropriate, tests should be run using the end-user UI and using the API directly.

## Positive Tests - Valid
### Revoking Tokens for a Managed Property 
1. U1: Create a New Property with Managed Number of Tokens message(s) with valid values.
1. U1: Create a Granting Tokens for a Managed Property message(s) with valid values for:
    * Property ID (for the property created in the previous step)
    * Number Properties
    * Memo
1. U1: Create a Revoking Tokens for a Managed Property message(s) with valid values for:
    * Property ID (for the property created in the previous step)
    * Number Properties
    * Memo
1. U1: See that the specified number of tokens are deducted for the specified Property ID from the address that issued the message
1. U2: See that the specified number of tokens are deducted for the specified Property ID from the address that issued the message

## Negative Tests - Not valid
### Attempt to Create an incorrect Revoking Tokens for a Managed Property message
1. U1: Attempt to create Revoking Tokens for a Managed Property transactions:
    * Property ID != an existing Property ID owned by the address created with Create a New Property with Managed Number of Tokens
    * Number Properties is not within the range of valid values for the property's property type (Divisible, Indivisible), see [Number of Coins](https://github.com/mastercoin-MSC/spec#field-number-of-coins)
    * Number Properties exceeds the number of tokens of Property ID owned and available by the address

1. U1: See that no token balances are changed for the address that issued the message
1. U2: See that no token balances are changed for the address that issued the message

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
