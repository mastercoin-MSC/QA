# Purchase Mastercoins with Bitcoins (accept currency trade offer)

Transaction Type 22: [Purchase Mastercoins with Bitcoins (accept currency trade offer)](https://github.com/mastercoin-MSC/spec#purchase-mastercoins-with-bitcoins)

Each application under test (AUT) must pass the applicable tests listed in [Major Items & Scenarios To Be Tested](https://github.com/marv-engine/QA/blob/master/MastercoinDistributedExchangeTestPlan.md#major-items--scenarios-to-be-tested).

The tests for Purchase Mastercoins with Bitcoins include:

1. user is able to enter valid values for all appropriate fields:
    * Currency identifier (1 for MSC, 2 for Test MSC)
    * Amount to be purchased
    * Address of Sell Offer
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

### View a New, Updated, Canceled Sell Offer
1. U1: Create a sell offer
1. U2: See the original sell offer
1. U1: Update the sell offer at least once
1. U2: See the updated sell offer after each update
1. U1: Cancel the sell offer
1. U2: See that the sell offer has been canceled

### Full Purchase of Exact Amount of Sell Offer
1. U1: Create a sell offer
1. U2: View the sell offer
1. U2: Send a purchase offer for the full amount of the sell offer
1. U2: See that you purchased the full amount
1. U2: Send payment for the purchase offer within the time limit
1. U2: See that your address now owns the purchased coins
1. U1: See that your address now owns the amount paid

### Attempt to Purchase More Than is Available
1. U1: Create a sell offer
1. U2: View the sell offer
1. U3: View the sell offer
1. U2: Send a purchase offer for a partial amount of the sell offer
1. U2: See that you purchased the partial amount 
1. U3: Send a purchase offer for the full amount of the sell offer
1. U3: See that you purchased only the remaining amount 
1. U3: Send exact payment for the purchase offer within the time limit
1. U3: See that your address now owns the purchased coins
1. U2: Send exact payment for the purchase offer within the time limit
1. U2: See that your address now owns the purchased coins
1. U1: See that your address now owns the amount paid
1. U1: See that the sell offer has been completed
1. U2: See that the sell offer has been completed
1. U3: See that the sell offer has been completed

### Attempt to Purchase When None is Available
1. U1: Create a sell offer
1. U2: View the sell offer
1. U3: View the sell offer
1. U2: Send a purchase offer for the full amount of the sell offer
1. U3: Send a purchase offer for the full amount of the sell offer
1. U2: See that you purchased the full amount 
1. U3: See that none of the sell offer is currently available 
1. U2: Send exact payment for the purchase offer within the time limit
1. U3: See that the sell offer has been completed
1. U2: See that your address now owns the purchased coins
1. U1: See that your address now owns the amount paid

### Extra Payment after Full Purchase
1. U1: Create a sell offer
1. U2: View the sell offer
1. U2: Send a purchase offer for the full amount of the sell offer
1. U2: See that you purchased the full amount
1. U2: Send payment for the purchase offer within the time limit
1. U2: Send extra payment for the purchase offer within the time limit
1. U2: See that your address now owns the exact amount of coins purchased
1. U1: See that your address now owns the total amount paid

### Two or More (Partial Purchase, Payment) Pairs
1. U1: Create a sell offer
1. U2: View the sell offer
1. U2: Send a purchase offer for a partial amount of the sell offer
1. U2: Send payment for the amount purchased within the time limit
1. U2: See that your address now owns the purchased coins
1. U2: Send a purchase offer for a partial amount of the remaining sell offer
1. U2: Send payment for the amount purchased within the time limit
1. U2: See that your address now owns the purchased coins
1. U1: See that your address now owns the total amount paid

### Two or More Partial Purchases Followed by Multiple Payments
1. U1: Create a sell offer
1. U2: View the sell offer
1. U2: Send a purchase offer for a partial amount of the sell offer
1. U2: See the new amount available in the sell offer
1. U2: Send a purchase offer for a partial amount of the remaining sell offer
1. U2: Send some payment for the amount owed within the time limit
1. U2: Send payment for the balance owed within the time limit
1. U2: See that your address now owns the purchased coins
1. U1: See that your address now owns the total amount paid

### Partial Payment after Full Purchase
1. U1: Create a sell offer
1. U2: View the sell offer
1. U2: Send a purchase offer for the full amount of the sell offer
1. U2: See that no amount is available in the sell offer
1. U2: Send partial payment within time limit
1. U2: Let time limit expire
1. U2: See that your address now owns the coins that were paid for
1. U2: See amount not paid for is again available
1. U1: See that your address now owns the amount paid

### Extra Payment after Partial Purchase
1. U1: Create a sell offer
1. U2: View the sell offer
1. U2: Send a purchase offer for a partial amount of the sell offer
1. U2: See that the remainder is available in the sell offer
1. U2: Send more payment than required within time limit
1. U2: See that you own the amount you paid for
1. U2: See that the correct remaining amount is now available for sale
1. U1: See that your address now owns the amount paid

### No Payment after Partial Purchase
1. View a sell offer
1. Send a purchase offer for a partial amount of the sell offer
1. See the new amount available in the sell offer
1. Send no payment within time limit
1. See full amount of the sell offer again available

## Negative Tests - Not Valid
For the negative tests, the final step of each test must not succeed.

### Erroneous Message Field Data
1. Attempt to send purchase offers:
    * to an address that does not have an active sell offer
    * to an address that canceled a sell offer
    * using a currency id other than 1 and 2
    * Amount to be purchased = 0
    * No output to the Exodus Address
    * Output amount to the Exodus Address is below the dust level

The tester and developer should work together to write and run procedures that thoroughly test this functionality in the AUT.
