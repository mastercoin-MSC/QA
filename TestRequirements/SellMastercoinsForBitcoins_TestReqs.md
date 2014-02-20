# Sell Mastercoins for Bitcoins (currency trade offer)

Transaction Type 20: [Sell Mastercoins for Bitcoins (currency trade offer)](https://github.com/mastercoin-MSC/spec#sell-mastercoins-for-bitcoins)

Each application under test (AUT) must adhere to [The Master Protocol / Mastercoin Complete Specification](https://github.com/mastercoin-MSC/spec/blob/master/README.md) and pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/marv-engine/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

The tests for Sell Mastercoins for Bitcoins include:

1. user is able to enter valid values for all appropriate fields:
    * Currency identifier (1 for MSC, 2 for Test MSC)
    * Amount for sale
    * Amount of bitcoins desired
    * Time limit in blocks
    * Minimum bitcoin transaction fee
    * Action (1 for New, 2 for Update, 3 for Cancel)
1. valid input data is parsed and interpreted correctly, including all valid MSC Protocol transaction types in the blockchain that are supported by the AUT
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. correct Sell Mastercoins for Bitcoins transactions are generated from valid test input data
1. runtime error conditions are detected and handled correctly (e.g. insufficient funds, application/network/OS failure)
1. all edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user

For each test sequence, start in a known state and return to a known state after the test is complete.

## Positive Tests - Valid
For the positive tests, each step must succeed with correct results. 
### Basic Sell Offer manipulation
1. Create sell offer
1. Update sell offer
1. Cancel sell offer
1. Create sell offer

### Basic Sell/Purchase/Pay
1. Create sell offer for more MSC than available
1. Receive full purchase offer
1. Receive full payment

### Update/Cancel after One Purchase
1. Create sell offer
1. Receive full purchase offer
1. Update sell offer before payment received
1. Cancel sell offer before payment received

### Update/Cancel with Two or More Partial Purchases
1. Create sell offer
1. Receive partial purchase offer #1
1. Update sell offer
1. Receive payment for purchase offer #1
1. Receive partial purchase offer #2
1. Cancel sell offer

### No Payment after Partial Purchase
1. Create sell offer
1. Receive partial purchase offer #1
1. Receive no payment within time limit
1. See full amount of sell offer again available


## Negative Tests - Not Valid
For the negative tests, the final step of each test must not succeed.

### Erroneous Message Field Data
1. Attempt to create sell offers:
    * for currency id other than 1 and 2
    * time limit = 0
    * bitcoins desired = 0
    * Action other than 1, 2 and 3

1. Attempt to update sell offer: 
    * for currency id other than 1 and 2
    * time limit = 0
    * bitcoins desired = 0
    * after fully purchased and payment received

### Create a Sell Offer While One is Active
1. Create sell offer
1. Attempt to create a second sell offer

### Cancel a Completed Sell Offer
1. Attempt to cancel sell offer:
    * after fully purchased and full payment received

### Cancel When No Sell Offer is Active
1. Attempt to cancel sell offer when no sell offer active

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.

