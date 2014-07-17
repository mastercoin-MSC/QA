# Create a Property with Fixed Number of Tokens

Transaction Type 50: [Create a Property with Fixed Number of Tokens](https://github.com/mastercoin-MSC/spec#new-property-creation-with-fixed-number-of-tokens)

Each application under test (AUT) must adhere to [The Master Protocol / Mastercoin Complete Specification](https://github.com/mastercoin-MSC/spec/blob/master/README.md) and pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/marv-engine/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

The tests for Create a Property with Fixed Number of Tokens include:

1. user is able to enter valid values for all appropriate fields:
    * Ecosystem
    * Property Type
    * Previous Property ID
    * Property Category
    * Property Subcategory
    * Property Name
    * Property URL
    * Property Data
    * Number Properties
    * fields for the Bitcoin protocol
1. valid input data is parsed and interpreted correctly, including all valid MSC Protocol transaction types in the blockchain that are supported by the AUT
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. correct Create a Property with Fixed Number of Tokens transactions are generated from valid test input data
1. runtime error conditions are detected and handled correctly (e.g. insufficient funds, application/network/OS failure)
1. all edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user

For each test sequence, start in a known state and return to a known state after the test is complete. Run the tests separately and also simultaneously. The simultaneous tests should be run by the same users/addresses in the same roles where possible, and also by different users/addresses.

Where appropriate, tests should be run using the end-user UI and using the API directly.

## Positive Tests - Valid
### Create a Property with Fixed Number of Tokens 
1. U1: Create Create a Property with Fixed Number of Tokens message(s) with valid values for:
    * Ecosystem
    * Property Type
    * Previous Property ID
    * Property Category
    * Property Subcategory
    * Property Name
    * Property URL
    * Property Data
    * Number Properties
1. U1: See that the property is created with all the specified values and is assigned the next sequential Property ID in the specified ecosystem
1. U2: See that the property is created with all the specified values and is assigned the next sequential Property ID in the specified ecosystem

## Negative Tests - Not valid
### Attempt to Create an Incorrect Create a Property with Fixed Number of Tokens message
1. U1: Attempt to create Create a Property with Fixed Number of Tokens transactions:
    * Ecosystem != a valid value
    * Property Type != a valid value
    * Previous Property ID != 0 or != an existing Property ID owned by the address
    * One or more of the string fields has more than 255 bytes plus the null terminator:
        + Property Category
        + Property Subcategory
        + Property Name
        + Property URL
        + Property Data
    * Number Properties = 0 and Property Type = 1 or 2
    * Number Properties > max allowed per spec [Number of Coins](https://github.com/mastercoin-MSC/spec#field-number-of-coins)
1. U1: See that a property is not created with the erroneous input values
1. U2: See that a property is not created with the erroneous input values

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
