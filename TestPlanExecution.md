Running Test Plans
==

Prerequisites: you must have a github account; we're using github to store test results, and to keep track of issues.

Configure the application under test (AUT) to include timestamps in its log file(s), if possible.

What should you test?
--

Generally, testers are recruited by developers or QA leads by asking for help on the bitcointalk forums,
in IRC chat, in pull request comments, on twitter, etc.

The developer or QA lead will create the test plan in a repository here at github, usually by forking this
main QA repository. So you can look at its forking history to see testing activity or find things
that might need more testing.


Test procedure
--

1. Fork the github repository that has the test plan you'll be working on.<br/>
  ![github fork](https://copy.com/2laWomE4VjAj)
2. Do what it says in the test plan.
3. File any issues **in the application's repository issue tracker!** If you just poke the
Issues button in your forked test plan repository the developers will never see them.
4. Edit the copy of the test plan in your repository with the results of your testing. Feel free to add
notes, etc.
5. Save a copy of the log file(s) created by the AUT in case the developers need them to
find issues or to prove that you tested what you said you tested in order to claim a testing bounty.

When you have finished running the test plan, submit a pull request or
send a message to the person who created the test plan to let them know you've finished testing.<br/>
  ![github fork](http://dl.dropbox.com/u/38065353/Github_PullRequest.jpg)

Bounties
--
J.R. Willets announced the [300 BTC Coding Contest: Distributed Exchange (MasterCoin Developer Thread)](https://bitcointalk.org/index.php?topic=292628.msg3133386#msg3133386) in September 2013. The contest is still active as of January 2014. 100 BTC will be split up among people who help by doing code reviews, testing, and bug reporting (this may be the same people as the developers, or different people). 
