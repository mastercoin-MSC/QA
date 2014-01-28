QA
==

This repository contains Quality Assurance artifacts (processes, master test plans, resources available, etc)
for the Mastercoin Distributed Exchange. It's forked from https://github.com/bitcoin/QA.

[Mastercoin Distributed Exchange Test Plan](MastercoinDistributedExchangeTestPlan.md) describes the testing strategy we are using.

Each transaction type will have an implementation-independent test requirements spec in [TestRequirements](TestRequirements) identifying what has to be tested for that transaction. That spec will be used as the starting point for producing and running test procedures for each candidate implementation.

We're still working out the details of when the candidate implementations will be ready for formal testing and how testing & results reporting will work. 

If you are a developer or QA lead, also read
[TestPlanCreation.md](TestPlanCreation.md)

If you want to help out (and maybe earn some BTC for testing), then read [TestPlanExecution.md](TestPlanExecution.md)
