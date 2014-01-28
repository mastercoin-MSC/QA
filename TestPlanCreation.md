TEST PLAN CREATION
==

Prerequisite: you must have a github account, so you can clone repositories and file/track issues that you find.

Ideally, the test plan is created by QA and reviewed by the developer
for completeness, after QA gets a description of the new feature or
thing to be tested. Less ideally, the test plan is created by the
developer and reviewed by QA to try to catch edge-cases the developer
didn't think about testing.

There is no global list of all test plans; instead, pull requests,
forum posts, or whatever makes sense for the thing being tested (new
feature, release candidate) just link to the relevant master test plan
or plans.  If we need or want to re-test something later, old test
plans will be cloned or edited.

Creating a new plan
--

1. Fork this repository<br/>
  ![github fork](https://copy.com/2laWomE4VjAj)
2. Create a new file to contain the new test plan. Try to choose a good filename.<br/>
  ![github add](https://copy.com/IWYNSeKhu3XA)
3. Create the test plan in QA/TestPlans; copy/paste the [TestPlanSkeleton.md](TestPlanSkeleton.md) template to start.

Testing
--

Follow the procedure in [TestPlanExecution.md](TestPlanExecution.md) to carry out the test plan.

Gather/report results
--

Update the test plan as you get results (whether from other testers or from your own tests).
If this is a test plan for a new feature, update the pull request with test results to help
convince the core developers it is safe to pull.
