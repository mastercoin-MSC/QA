# Mastercoin Distributed Exchange Test Plan

# Introduction

The [Distributed Exchange ](http://wiki.mastercoin.org/index.php/Distributed_Exchange)(Dist-Ex) is a primary feature of Mastercoin (MSC) functionality. MSC system integrity and user confidence in the system depend on the Dist-Ex performing correctly under all circumstances.

# Testing Philosophy

Our main goal is to ensure that all Dist-Ex components adhere to the [MSC spec](https://github.com/mastercoin-MSC/spec) - primarily creation of all appropriate transactions when presented with valid, well-formed inputs and appropriate initial conditions. This requires:

* presentation of a correct, meaningful message to the user that the transaction has been created
* all input and output data structures are left in a demonstrably correct state that reflects successful creation of the transaction

Dist-Ex components also have to detect errors in all phases of processing and react gracefully. Graceful reaction requires:

* presentation of a correct, meaningful message to the user, with options if that’s appropriate
* the transaction is fully undone/rolled back if it cannot be completed successfully
* all input and output data structures are left as they were before the transaction was attempted - in a demonstrably known state with no corruption
* presentation of a correct, meaningful message to the user that the transaction has either succeeded or failed

Since MSC transaction data is embedded in the Bitcoin blockchain, testing must confirm that the blockchain is not corrupted or incorrectly modified by the Dist-Ex components. Please refer to the [MSC spec](https://github.com/mastercoin-MSC/spec) appendix [Storing Mastercoin Data in the Blockchain](https://github.com/mastercoin-MSC/spec#appendix-a--storing-mastercoin-data-in-the-blockchain)[ ](https://github.com/mastercoin-MSC/spec#appendix-a--storing-mastercoin-data-in-the-blockchain)for details about how MSC transaction data is to be embedded in the Bitcoin blockchain. 

# Test Plan Highlights

We’ll need test harnesses, object inspectors (e.g. [Masterchain.info](https://masterchain.info/) and other utilities from [https://github.com/grazcoin/mastercoin-tools](https://github.com/grazcoin/mastercoin-tools), [http://wiki.mastercoin.org/index.php/Block_Explorers](http://wiki.mastercoin.org/index.php/Block_Explorers)), scripts, known inputs, etc. to set up and run comprehensive and repeatable functionality testing in clean environments. We’ll have to verify that these components themselves are correct. For now, the bulk of testing can be done using Test Mastercoins (TMSC) on the Bitcoin mainnet. After testing with TMSC, it’s best to test with MSC on the Bitcoin mainnet if possible, to confirm that everything works in the production environment. In the future, we will test using TMSC on [Bitcoin testnet](https://en.bitcoin.it/wiki/Testnet), MSC on testnet, TMSC on mainnet, and finally with MSC on mainnet.

The major items & scenarios to be tested include:

1. valid input data is parsed and interpreted correctly, including all valid MSC transaction types in the blockchain that are supported by the application
1. erroneous input data, including a corrupted blockchain, is detected as not valid and handled correctly
1. creation of valid transactions for all MSC transaction types supported by the application
1. multi-participant sequences (e.g. Sell Offer by user A then Purchase Offer by user B)
1. multi-user tests (e.g. multiple users attempt to accept the same Sell Offer)
1. runtime error conditions (e.g. application, network or OS failure) are detected and handled correctly
1. edge cases are handled correctly
1. correct, meaningful messages reflecting transaction success or failure are presented to the user 

The MSC spec appendix [Webservice verification API ](https://github.com/mastercoin-MSC/spec#appendix-a--storing-mastercoin-data-in-the-blockchain)has information about basic transaction verification services that should be implemented by web-based Mastercoin services.

# MSC Transaction Types

For convenience, here’s a list of the MSC transaction types from the [MSC spec](https://github.com/mastercoin-MSC/spec), currently version 0.3.5. The spec always has the authoritative list and descriptions of MSC transactions.

*    0: [Simple Send](https://github.com/mastercoin-MSC/spec#transferring-mastercoins-simple-send)
*    1: [Pay Dividends (Send All)](https://github.com/mastercoin-MSC/spec#pay-dividends-send-all)
*   10: [Mark an Address as Savings](https://github.com/mastercoin-MSC/spec#marking-an-address-as-savings)
*   11: [Mark a Savings Address as Compromised](https://github.com/mastercoin-MSC/spec#marking-a-savings-address-as-compromised)
*   12: [Mark an Address as Rate-Limited](https://github.com/mastercoin-MSC/spec#marking-an-address-as-rate-limited)
*   14: [Remove a Rate Limitation](https://github.com/mastercoin-MSC/spec#removing-a-rate-limitation)
*   20: [Sell Mastercoins for Bitcoins (currency trade offer)](https://github.com/mastercoin-MSC/spec#selling-mastercoins-for-bitcoins)
*   21: [Offer/Accept Mastercoins for other Mastercoin-derived Currency (currency trade offer)](https://github.com/mastercoin-MSC/spec#selling-mastercoins-for-other-mastercoin-derived-currencies)
*   22: [Purchase Mastercoins with Bitcoins (accept currency trade offer)](https://github.com/mastercoin-MSC/spec#purchasing-mastercoins-with-bitcoins)
*   30: [Register a Data Stream](https://github.com/mastercoin-MSC/spec#registering-a-data-stream)
*   40: [Offer/Accept a Bet](https://github.com/mastercoin-MSC/spec#offering-a-bet)
*   50: [Create a Property](https://github.com/mastercoin-MSC/spec#smart-property)
*   60: [List Something for Sale](https://github.com/mastercoin-MSC/spec#listing-something-for-sale)
*   61: [Initiate a Purchase from a Listing](https://github.com/mastercoin-MSC/spec#initiating-a-purchase)
*   62: [Accept a Buyer Offer](https://github.com/mastercoin-MSC/spec#accepting-a-buyer)
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

Independently developed dist-ex applications, if available, should also attempt to read the resulting blockchain. 

The applications that read the resulting blockchain will verify that the AUT:

* did not corrupt the blockchain
* correctly added the transaction to the blockchain
* made no other changes to the blockchain

## Negative Tests

These tests will determine if the application can detect erroneous inputs and runtime environmental errors and react properly.

Erroneous inputs include items such as missing data, malformed/corrupted data (including a bad blockchain), numeric values outside of acceptable ranges, values not in the list of valid inputs, non-numeric data where numeric values are required. Runtime environmental errors can be introduced by doing things such as manually killing the application process, disconnecting the network, removing or changing permissions of data files, powering down the machine.

# Transaction-specific Tests

We’ll have a baseline test procedure for each transaction type. We expect these test procedures to be customized for the particular application under test.
