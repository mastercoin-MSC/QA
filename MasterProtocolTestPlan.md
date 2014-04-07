# Master Protocol Test Plan

# Introduction

The Master Protocol Test Plan applies to all deployed features and aspects of the [The Master Protocol / Mastercoin Complete Specification](https://github.com/mastercoin-MSC/spec) that are currently deployed or in the process of being deployed. MSC system integrity and user confidence in the system depend on all system components performing correctly under all circumstances.

The current major functionality areas are:
* [Distributed Exchange](http://wiki.mastercoin.org/index.php/Distributed_Exchange)
* [Smart Properties](http://wiki.mastercoin.org/index.php/Smart_property)

# Testing Philosophy

Our main goal is to ensure that all released components adhere to the [MSC Protocol spec](https://github.com/mastercoin-MSC/spec) - primarily creation of all appropriate transactions when presented with valid, well-formed inputs and appropriate initial conditions. This requires:

* presentation of a correct, meaningful message to the user that the transaction has been created
* all input and output data structures are left in a demonstrably correct state that reflects successful creation of the transaction

Master Protocol-compliant components also have to detect errors in all phases of processing and react gracefully. Graceful reaction requires:

* presentation of a correct, meaningful message to the user, with options if that’s appropriate
* the transaction is fully undone/rolled back if it cannot be completed successfully
* all input and output data structures are left as they were before the transaction was attempted - in a demonstrably known state with no corruption
* presentation of a correct, meaningful message to the user that the transaction has either succeeded or failed

Since Master Protocol transaction data is embedded in the Bitcoin blockchain, testing must confirm that the blockchain is not corrupted or incorrectly modified by the Master Protocol-compliant applications. Please refer to the [MSC Protocol spec](https://github.com/mastercoin-MSC/spec) appendix [Storing Mastercoin Data in the Blockchain](https://github.com/mastercoin-MSC/spec#appendix-a--storing-mastercoin-data-in-the-blockchain) for details about how MSC Protocol transaction data is to be embedded in the Bitcoin blockchain. 

# Test Plan Highlights

We’ll need test harnesses, object inspectors (e.g. [Masterchain.info](https://masterchain.info/), [Masterchest.info](https://masterchest.info/)  and other utilities from [https://github.com/mastercoin-MSC/omniwallet](https://github.com/mastercoin-MSC/omniwallet), [http://wiki.mastercoin.org/index.php/Block_Explorers](http://wiki.mastercoin.org/index.php/Block_Explorers)), scripts, known inputs, etc. to set up and run comprehensive and repeatable functionality testing in clean environments. We’ll have to verify that these components themselves are correct. For now, the bulk of testing can be done using Test Mastercoins (TMSC) on the Bitcoin mainnet. After testing with TMSC, it’s best to test with MSC on the Bitcoin mainnet if possible, to confirm that everything works in the production environment. In the future, we will test using TMSC on [Bitcoin testnet](https://en.bitcoin.it/wiki/Testnet), MSC on testnet, TMSC on mainnet, and finally with MSC on mainnet.

# Major Items & Scenarios To Be Tested

Each candidate application will be tested for the following minimum functionality:

1. user is able to enter valid values for all appropriate fields
1. valid input data is parsed and interpreted correctly, including all valid MSC Protocol transaction types in the blockchain that are supported by the application
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. correct transactions are generated for all MSC Protocol transaction types supported by the application
1. multi-participant sequences (e.g. Sell Offer by user A then Purchase Offer by user B)
1. multi-user tests (e.g. multiple users attempt to accept the same Sell Offer)
1. runtime error conditions are detected and handled correctly (e.g. insufficient funds, application/network/OS failure)
1. edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success/status or failure are presented to the user 

The MSC Protocol spec appendix [Webservice verification API ](https://github.com/mastercoin-MSC/spec#appendix-a--storing-mastercoin-data-in-the-blockchain)has information about basic transaction verification services that should be implemented by web-based Mastercoin services.

# MSC Protocol Transaction Types

For convenience, here’s a list of the MSC Protocol transaction types from the [MSC Protocol spec](https://github.com/mastercoin-MSC/spec), version 0.4.5.3 at the time of this update. The spec always has the authoritative list and descriptions of MSC Protocol transactions.

+ Current:
    *    0: [Simple Send](https://github.com/mastercoin-MSC/spec#transfer-coins-simple-send)
    *    1: [Investment Send](https://github.com/mastercoin-MSC/spec#investment-send)
    *   20: [Sell Coins for Bitcoins (currency trade offer)](https://github.com/mastercoin-MSC/spec#sell-mastercoins-for-bitcoins)
    *   21: [Offer/Accept Master Protocol Coins for Another Master Protocol Currency (currency trade offer)](https://github.com/mastercoin-MSC/spec#sell-master-protocol-coins-for-another-master-protocol-currency)
    *   22: [Purchase Coins with Bitcoins (accept currency trade offer)](https://github.com/mastercoin-MSC/spec#purchase-mastercoins-with-bitcoins)
    *   50: [Create a Property with fixed number of tokens](https://github.com/mastercoin-MSC/spec#new-property-creation-with-fixed-number-of-tokens)
    *   51: [New Property Creation via Crowdsale with Variable number of Tokens](https://github.com/mastercoin-MSC/spec#new-property-creation-via-crowdsale-with-variable-number-of-tokens)
    *   52: [Promote a Property](https://github.com/mastercoin-MSC/spec#promote-a-property)
    *   53: [Close a Crowdsale Manually](https://github.com/mastercoin-MSC/spec#close-a-crowdsale-manually)

+ To be added in future releases:
    *    2: [Restricted Send](https://github.com/mastercoin-MSC/spec#restricted-send)
    *    3: [Pay Dividends (Send All)](https://github.com/mastercoin-MSC/spec#pay-dividends-send-all)
    *   10: [Mark an Address as Savings](https://github.com/mastercoin-MSC/spec#marking-an-address-as-savings)
    *   11: [Mark a Savings Address as Compromised](https://github.com/mastercoin-MSC/spec#marking-a-savings-address-as-compromised)
    *   12: [Mark an Address as Rate-Limited](https://github.com/mastercoin-MSC/spec#marking-an-address-as-rate-limited)
    *   14: [Remove a Rate Limitation](https://github.com/mastercoin-MSC/spec#removing-a-rate-limitation)
    *   30: [Register a Data Stream](https://github.com/mastercoin-MSC/spec#registering-a-data-stream)
    *   31: [Publish Data](https://github.com/mastercoin-MSC/spec#publishing-data)
    *   40: [Offer/Accept a Bet](https://github.com/mastercoin-MSC/spec#offering-a-bet)
    *   60: [List Something for Sale](https://github.com/mastercoin-MSC/spec#listing-something-for-sale)
    *   61: [Initiate a Purchase from a Listing](https://github.com/mastercoin-MSC/spec#initiating-a-purchase)
    *   62: [Respond to a Buyer Offer](https://github.com/mastercoin-MSC/spec#accepting-a-buyer)
    *   63: [Release Funds and Leave Feedback](https://github.com/mastercoin-MSC/spec#leaving-feedback)
    * 100: [Create a New Child Currency](https://github.com/mastercoin-MSC/spec#new-currency-creation)

# Basic Tests

A minimum level of functionality is required for all transactions.

## Positive Tests

These tests will determine if the application under test (AUT) can produce correct results when provided with valid inputs.

Transactions for each supported transaction type will be generated. For transaction data items that accept a range of values, tests should include values at both ends of the range as well as at least three values in between. For transaction data items that accept values from a list, all values should be tested if possible.

For each transaction, the resulting blockchain will be read by at least:

* the AUT instance that generated the transaction, if possible
* a second instance of the AUT
* an independent blockchain explorer

Independently developed MP-compliant applications, if available, should also attempt to read the resulting blockchain. 

The applications that read the resulting blockchain will verify that the AUT:

* did not corrupt the blockchain
* correctly added the transaction to the blockchain
* made no other changes to the blockchain

## Negative Tests

These tests will determine if the application can detect erroneous inputs and runtime environmental errors and react properly.

Erroneous inputs include items such as missing data, malformed/corrupted data (including a bad blockchain), numeric values outside of acceptable ranges, values not in the list of valid inputs, non-numeric data where numeric values are required, unsupported transaction messages and transaction message versions. Each application is expected to have additional erroneous inputs. Runtime environmental errors can be introduced by doing things such as manually killing the application process, disconnecting the network, removing or changing permissions of data files, powering down the machine.

# Transaction-specific Tests

Baseline test requirements for each transaction type are identified in [TestRequirements](TestRequirements). These test requirements serve as guidelines for implementing specific test procedures for each application under test.
