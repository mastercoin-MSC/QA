# {Application} TEST PLAN

Version tested:
{0.x.y release candidate N, or git commit}

Test environment:
{Operating System or other relevant info}

## Test Setup

Describe any test environment setup that needs to be done, in an explicit, step-by-step fashion.

For example, for sanity-testing a release the setup might be:

1. Begin with a clean, non-developer operating-system image.
1. Download release candidate (RC) version to be tested.
1. Run installer or follow installation instructions.

## Tests

Each test is a level-3 section, with Title, test procedure, and expected results.  Examples:

### Blockchain download

1. Run the RC on a clean system.

EXPECT:

1. After a few minutes, GUI shows wallet with zero balance.
2. After a few minutes, GUI shows at least one connection to the network.
3. After 24 hours, GUI shows fully synchronized with network/blockchain.

PASS/FAIL  (if FAIL, tester may add notes here or links to issues filed)

### Other test here

1. Steps to be performed, with enough detail to be precisely repeated

EXPECT:

1. Specific details about presentation to user; links to annotated screenshots are helpful
2. Specific details on how to check for correct outputs, e.g. blockchain content, wallet

PASS/FAIL

### Final steps

Tell testers what they should do when they're finished.

Submit your test results, including links to log files and screenshots, by filling out the  
[MSC Client Test Results Reporting Form](https://docs.google.com/forms/d/1KZw-JYjt9njBXw4GJU2IXIGKP38oytdlCXZcTnw40Xc/viewform).
