# OMNIWALLET TEST PLAN

Version tested: 
(include branch & last commit on branch)

Test environment:
Jquery 1.11
Angular.js 1.2.13
Nginx 1.4.4
Linux 3.12.8 x86_64

## Test Setup

git clone https://github.com/mastercoin-MSC/omniwallet
bower install

## Tests

Each test is a level-3 section, with Title, test procedure, and expected results.  Examples:

### Sending TMSC to yourself

0. Start nginx 
1. Run app.sh from omniwallet root.
2. Browse to localhost
3. Click Create Wallet
4. Enter tester@email.com and 'tester' for the password
5. Click 'Create', and then click 'Your Wallet'
6. Click Trade Assets in the left-hand sidecar
7. Click Start new send transaction
8. Select 'TMSC' for the type of coin, and enter your address in the 'Send funds to' input.
9. Enter 0.000000001 for the Amount to send
10. Set miner fees to 0.0001 
11. Click Send Transaction
12. Enter 'tester' for your passphrase
13. Click Send Funds

EXPECT:

1. After a moment, you should see a reply from the server if your transaction was successful.

PASS/FAIL  (if FAIL, tester may add notes here or links to issues filed)

Your test passed if you are able to get a reply from the server IN GREEN ('Your funds were sent.')
Your test failed if you are able to get a reply from the server IN RED ('Your funds could not be sent.')

### Final steps

Ensure the requirements in /TestRequirements/SimpleSend_TestReqs.md are also met during testing.  
Clean up after yourself, delete all temporary files, and reboot your machine.

Submit your test results, including links to log files and screenshots, by filling out the  
[MSC Client Test Results Reporting Form](https://docs.google.com/forms/d/1KZw-JYjt9njBXw4GJU2IXIGKP38oytdlCXZcTnw40Xc/viewform).
