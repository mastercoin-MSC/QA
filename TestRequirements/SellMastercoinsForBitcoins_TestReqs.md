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

For each test sequence, start in a known state and return to a known state after the test is complete. Run the tests separately and also simultaneously. The simultaneous tests should be run by the same users/addresses in the same roles where possible, and also by different users/addresses.

Where appropriate, tests should be run using the end-user UI and using the API directly.

## Positive Tests - Valid
For the positive tests, each step must succeed with correct results. 
### Basic Sell Offer manipulation
1. U1: Create sell offer
1. U1, U2: See:
 1. correct terms of new sell offer
 1. U1 MSC available balance decreased by amount for sale
 1. U1 MSC reserved balance increased by amount for sale
1. U1: Update sell offer
1. U1, U2: See:
 1. correct terms of updated sell offer
 1. U1 MSC available balance reflects updated amount for sale
 1. U1 MSC reserved balance reflects updated amount for sale
1. U1: Cancel sell offer
1. U1, U2: See:
 1. sell offer is no longer active
 1. amount for sale added to U1 MSC available balance
 1. U1 MSC reserved balance decreased by amount for sale
1. U1: Create sell offer
1. U1, U2: See correct terms of new sell offer
 1. U1 MSC available balance decreased by amount for sale
 1. U1 MSC reserved balance increased by amount for sale

### Basic Sell/Accept/Pay
1. U1: Create sell offer for more MSC than available
1. U1, U2: See:
 1. correct terms of new sell offer
 1. U1 MSC available balance decreased by amount for sale
 1. U1 MSC reserved balance increased by amount for sale
1. U2: Send full purchase offer
1. U1, U2, U3: See U2 has accepted the full sell offer
1. U2: Send full payment
1. U1, U2, U3: See that:
 1. full payment has been received by U1
 1. all MSC from sell offer now transferred to U2
 1. U1 MSC reserved balance decreased by amount transferred to U2
 1. U1 MSC available balance unchanged
 1. Sell offer is no longer active because full amount for sale has been paid for

### Update/Cancel after One Full Accept
1. U1: Create sell offer
1. U1, U2: See:
 1. correct terms of new sell offer
 1. U1 MSC available balance decreased by amount for sale
 1. U1 MSC reserved balance increased by amount for sale
1. U2: Send full accept
1. U1, U2, U3: See U2 has accepted the full sell offer
1. U1: Update sell offer before payment received
1. U1, U2: See:
 1. Amount and terms accepted by U2 is unchanged
1. U1: Cancel sell offer before payment received
1. U1, U2, U3: See:
 1. Amount and terms accepted by U2 are unchanged
 1. U1 MSC reserved balance decreased by 0 (because the full amount for sale has been accepted)

### Update/Cancel with Two or More Partial Accept
1. U1: Create sell offer
1. U1, U2: See:
 1. correct terms of new sell offer
 1. U1 MSC available balance decreased by amount for sale
 1. U1 MSC reserved balance increased by amount for sale
1. U2: Send partial accept #1
1. U1, U2, U3: See:
 1. U2 has accepted partial sell offer
 1. U1 amount remaining for sale decreased by amount accepted
1. U1: Update sell offer
1. U1, U2, U3: See:
 1. correct terms of updated sell offer
 1. U1 MSC available balance reflects updated amount for sale
 1. U1 MSC reserved balance reflects updated amount for sale
1. U2: Send payment for accept #1
1. U1, U2, U3: See that:
 1. payment for accept #1 has been received by U1
 1. MSC for accept #1 now transferred to U2
 1. U1 MSC reserved balance decreased by amount transferred to U2
 1. U1 MSC available balance unchanged
1. U2: Send partial accept #2
1. U1, U2, U3: See:
 1. U2 has accepted partial sell offer
 1. U1 amount remaining for sale decreased by amount accepted
1. Cancel sell offer
1. U1, U2, U3: See:
 1. sell offer is no longer active
 1. Amount and terms accepted by U2 are unchanged
 1. remaining amount for sale added to U1 MSC available balance
 1. U1 MSC reserved balance decreased by remaining amount for sale

### No Payment after Partial Purchase
1. U1: Create sell offer
1. U1, U2: See:
 1. correct terms of new sell offer
 1. U1 MSC available balance decreased by amount for sale
 1. U1 MSC reserved balance increased by amount for sale
1. U2: Send partial accept #1
1. U1, U2, U3: See:
 1. U2 has accepted partial sell offer
 1. U1 amount remaining for sale decreased by amount accepted
1. U2: Send no payment within time limit
1. U1, U2, U3: See:
 1. U2 accept now expired
 1. U1 amount remaining for sale increased by amount accepted
 1. U1 MSC available balance unchanged
 1. U1 MSC reserved balance unchanged

## Negative Tests - Not Valid
For the negative tests, at least the final step of each test must not succeed.

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
1. U1: Create sell offer
1. U1, U2: See:
 1. correct terms of new sell offer
 1. U1 MSC available balance decreased by amount for sale
 1. U1 MSC reserved balance increased by amount for sale
1. U1: Attempt to create a second sell offer
1. U1, U2: See:
 1. new sell offer not created
 1. U1 MSC available balance unchanged
 1. U1 MSC reserved balance unchanged
 
### Cancel a Completed Sell Offer
1. Perform test [Basic Sell/Accept/Pay](#sell-accept-pay)
1. U1: Attempt to cancel sell offer

### Update a Completed Sell Offer
1. Perform test [Basic Sell/Accept/Pay](#sell-accept-pay)
1. U1: Attempt to update sell offer

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.

