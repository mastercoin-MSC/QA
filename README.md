QA
==

This repository contains Quality Assurance artifacts (processes, master test plans, resources available, etc)
for the Master Protocol specification. It's forked from https://github.com/bitcoin/QA.

[Master Protocol Test Plan](MasterProtocolTestPlan.md) describes the testing strategy we are using.

Each transaction type will have an implementation-independent test requirements spec in [TestRequirements](TestRequirements) identifying what has to be tested for that transaction. That spec is to be used as the starting point for producing and running test procedures for each candidate implementation.

If you are a developer or QA lead, also read
[TestPlanCreation.md](TestPlanCreation.md)

If you want to help out (and maybe earn some bounty for testing), then read [TestPlanExecution.md](TestPlanExecution.md)
