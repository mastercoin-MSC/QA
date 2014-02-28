TEST PLAN CREATION
==
The test plan is comprised of test procedures to verify correct behavior of the application being tested.

You must have a github account, so you can clone repositories and submit/track issues that you find.

Ideally, the test plan is created by QA or the tester and reviewed by the developer
for completeness, after QA gets a description of the new feature or
thing to be tested. Less ideally, the test plan is created by the
developer and reviewed by QA or the tester to try to catch edge-cases the developer didn't think about testing. 

If we need or want to re-test something later, old test plans will be cloned or edited.

Creating a new plan
--

1. Fork this [mastercoin-MSC/QA repository](https://github.com/mastercoin-MSC/QA).
1. Create a subdirectory in the [TestPlans](TestPlans) directory of your fork for the application to be tested, e.g. OmniWallet.
1. Copy the appropriate test requirements file(s) from the [TestRequirements](TestRequirements) directory into the newly created application directory.
1. Edit each test procedure to tailor the steps for the application to be tested. Be as explicit as possible. You can use [TestPlanSkeleton.md](TestPlanSkeleton.md) as a template.
    * Include steps to initialize the test environment to a known state.
    * Make sure you verify that each action by the user produces the correct behavior and result by the application.
    * Include steps to return the environment to a known state after test completion. 
    * Feel free to add test procedures, especially for aspects specific to the application you are testing.

You may want to put each customized test procedure in its own file.

Testing
--
Follow the procedure in [TestPlanExecution.md](TestPlanExecution.md) to carry out the test plan.

Some tests will take a long time to complete. You can run multiple tests simultaneously as long as they don't conflict with each other.

Gather/report results
--

Report results as you get them (whether from other testers or from your own tests) by filling out the  
[MSC Client Test Results Reporting Form](https://docs.google.com/forms/d/1KZw-JYjt9njBXw4GJU2IXIGKP38oytdlCXZcTnw40Xc/viewform).
