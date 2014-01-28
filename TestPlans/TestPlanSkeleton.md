# TEST PLAN TITLE

Submit completed tests and debug.log files to:  {Name &lt;email&gt;}

Version tested:
{0.x.y release candidate N, or git commit}

Test environment:
{Operating System or other relevant info}

## Test Setup

Describe any test environment setup that needs to be done, in an explicit, step-by-step fashion.

For example, for sanity-testing a release the setup might be:

0. Fork the test plan's github repository (see [TestPlanExecution.md](TestPlanExecution.md) )
1. Begin with a clean, non-developer operating-system image.
2. Download release candidate (RC) version to be tested.
3. Run installer or follow installation instructions.

## Tests

Each test is a level-3 section, with Title, test procedure, and expected results.  Examples:

### Blockchain download

Run the RC on a clean system.

EXPECT:

1. After a few minutes, GUI shows wallet with zero balance.
2. After a few minutes, GUI shows at least one connection to the network.
3. After 24 hours, GUI shows fully synchronized with network/blockchain.

PASS/FAIL  (if FAIL, tester may add notes here or links to issues filed)

### Other test here

Steps to be performed, with enough detail to be precisely repeated

EXPECT:

1. Specific details about presentation to user; links to annotated screenshots are helpful
2. Specific details on how to check for correct outputs, e.g. blockchain content, wallet

PASS/FAIL

### Final steps

Tell testers what they should do when they're finished; for example:

Email a link to your forked repository with attached log files to {...}. If the log files are
too large to attach, upload them to a service like mediafire.com, dropbox, etc. and include a link in the email.
