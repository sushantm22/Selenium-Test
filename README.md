So, last time we talked about the Plan phase, and we specifically covered the different skills involved in that phase.

Most of you have already tried these two skills, and I’ve also received some good feedback from you. Based on the constructive feedback and the challenges that were identified, we have already implemented several improvements.

The latest changes have also been pushed to the feature-migration branch. So whatever feedback we received, we have tried to incorporate those changes to make these skills better and easier to use.

Today, I’m going to talk about the next phases — Build, Execute, and Audit.

As we discussed in the previous session, the Plan phase created the complete set of test cases in the Given-When-Then format, and those test cases were also uploaded to Jira Xray.

Now, in the next stage, which is the Build phase, our objective is to scan the existing repository and generate the automation code accordingly.

The reason we need to scan the repository is because our developers can be working on very different technology stacks. We can have front-end developers, backend developers, and developers working on completely different codebases and frameworks.

So, when we have this level of diversity, how do we make sure that the automation we generate is resilient enough to work with the existing framework?

That’s where the Build phase comes into the picture.

⸻

Build Testing Code

The first thing the Build phase does is a repository scan.

It analyzes the existing repository and tries to understand how the automation framework is structured.

For example, it looks at:

* How test data is stored
* How feature files are stored
* Whether feature files exist or whether the framework directly uses spec files
* Where the spec files are located
* What automation framework is being used
* What locator strategy is being followed
* Whether Page Object Model is being used
* Whether the application is using Playwright
* Whether it is a backend framework
* Whether it is Java with Rest Assured
* And other framework-specific patterns

Once it understands the existing framework, it generates the automation code according to that structure.

As testers, this is something we already do manually today.

We look at the user story, understand the acceptance criteria, identify the test cases that are feasible for automation, and then create the automation code.

The Build skill is essentially doing this process using AI.

⸻

Change Exploration

Another important part of the Build phase is change exploration.

We want to understand exactly what changes have been introduced by the developer.

For example, let’s say the requirement was only to make a change to a dropdown.

There is always a possibility that along with that change, something else might have been modified accidentally — maybe some text, a field, or another part of the UI.

So, the change exploration helps us understand the scope of the actual development changes.

This gives us better visibility into our automation coverage and helps us make sure that we are testing the right areas.

⸻

Feasibility

The next step is feasibility.

I think everyone on this call is already familiar with what we mean by feasibility.

Basically, we want to identify how many of the generated test cases can actually be automated.

When we think about AI, it can sometimes feel like everything should be automatable.

But that’s not the approach we want to take.

For example, suppose we have six test cases.

Maybe four of them can be automated, but two cannot.

Those two could involve something like biometric authentication or another scenario that cannot practically be automated using our current framework.

The framework clearly identifies those cases as manual.

This feasibility check is important because we don’t want to claim that AI can automate everything.

The objective is to automate as much as realistically possible while clearly identifying what still needs manual testing.

⸻

Code Generator

Once repository exploration, change exploration, and feasibility are completed, we move to the Code Generator.

Based on everything that was analyzed, the framework understands what automation code needs to be generated and creates the code accordingly.

For example, in our previous phase, we may have had 24 final test cases.

But when we perform the feasibility analysis, let’s say only 22 test cases are automatable.

In that case, code will be generated for those 22 test cases, while the remaining two will be identified as manual.

I’ll show you an example of this during the demo.

⸻

Get Test Data

Now, creating the automation code from a logical perspective is relatively straightforward.

But creating the code is only one part.

The more critical part is making sure that the test cases are actually ready to execute.

And that’s where the Get Test Data skill comes into the picture.

As the name suggests, this skill looks at the test cases that were created in the Plan phase.

It understands the requirement and determines what kind of test data is required for those test cases.

Then it generates or retrieves the required test data in the format supported by the existing framework.

Again, this is where the repository analysis becomes important.

The skill understands how your framework currently maintains test data.

For example, maybe your framework stores data in:

* JSON files
* Properties files
* Database tables
* Or some other format

The generated output will follow the same structure so that it can be directly consumed by the existing automation framework.

⸻

Test Data Capabilities

So far, I’ve talked about Get Test Data mainly from the perspective of fetching or generating data.

But there is much more that this skill can do.

It can also manipulate existing test data and perform different data-related operations.

For example, let’s say you want to create an ET account or a dual account.

Instead of manually going through all the steps, you can simply invoke the skill.

You can use:

/get-test-data

and provide a prompt such as:

Create a margin account in UAT.

The skill will automatically understand that the request is for the UAT environment, route the request to the appropriate UAT/ET platform and integrated services, and generate the required test data in the expected format.

This is one example of how we can use the skill for test data creation.

⸻

Test Data Manipulation

We can also use the same skill to manipulate existing data.

For example, suppose you want to reset the password or disable MFA for a particular user in the UAT environment.

You can invoke:

/get-test-data

and provide a prompt such as:

Remove the MFA block for this user.

The skill will identify the required operation and perform the corresponding test-data action.

So, Get Test Data is not limited to simply fetching data. It provides a broader set of capabilities for creating, updating, and manipulating test data, depending on the use case.

And that’s an important part of making the generated automation actually executable.


Here is where I explain about how to use it:  Got it. This is the demo walkthrough portion, so I’ve kept the exact sequence of what the presenter does: Plan → Build → Verification → Manifest → Execute → Xray update → Get Test Data → Audit → PR readiness.
I’ve made it more natural to speak while keeping the technical details and demo cues intact.
End-to-End Pipeline Demo
Now, I’ll quickly walk you through the entire pipeline that we’ve covered so far, so you can understand how everything actually moves from one phase to the next.
So, what I did here is, I started by calling Create Test Case, and I provided the user story ID.
Before starting the actual workflow, the framework performs some pre-checks.
In my case, Python was already available on my local machine, and all the required MCPs were already started. So the framework performed the pre-check and verified that everything was in working condition.
The first step was the Test Plan.
From our previous session, you may remember that we use LLM A, LLM B, and LLM C for generating test cases. The framework generated the test cases using these three LLMs.
It also asked me whether I wanted to generate accessibility-based test cases.
I selected No, and then I reviewed and approved the generated test cases.
After that, the framework asked whether I wanted to upload the test cases to Xray.
Before approving the upload, I quickly verified the important information, such as the user story, assignee, project key, and other relevant details.
Once I verified everything, I approved it, and the test cases were uploaded to Xray.
So at this point, the Plan phase is complete.
Now I want to move to the next step, which is Build Testing Code.
If we go back to our overall pipeline diagram, the Plan phase has already happened, and now we are moving into the Build phase.

⸻

Build Testing Code – Repository Analysis
The first thing the Build phase does is understand the entire context of the repository.
It analyzes the application and the environment in which we want to execute the tests.
For example, it identifies the application type, the target environment, the test type, the test case source file, the feature name, and other important information.
These details are important because if I don’t agree with something that has been identified, I can review it and provide the correct information before continuing.
The framework also analyzes the existing automation framework.
For example, in my case, it identified that the framework is using Playwright.
It went into the package.json file and identified the Playwright version being used, along with other framework details.
This is important because we don’t want AI to blindly generate automation code.
It first needs to understand the existing framework and then generate code according to that framework.

⸻

Feasibility
The next step is the feasibility analysis.
As we discussed earlier, the framework checks how much of the identified test scope can actually be automated.
One important thing to notice here is that it does not simply say that everything is 100% automatable.
Instead, it provides an estimate based on the analysis.
This is important because there can always be scenarios where automation is not feasible or where additional manual testing is required.
So the objective is not to claim that AI can automate everything.
The objective is to identify what can realistically be automated and clearly call out the remaining areas.

⸻

Code Generation and Verification
Once I approve the feasibility analysis, the framework starts generating the automation code.
After generating the code, it performs another important step — verification.
This verification is required because our next phase is Execute.
We don’t just want to generate code; we want to make sure that the generated code is actually ready to execute.
So the framework checks whether:
* All required files have been created
* Imports are correct
* Files are properly linked
* Dependencies are consistent
* The overall code structure is correct
Basically, it validates that everything generated during the Build phase is internally consistent.

⸻

Review Gate and Manifest
After the verification, we get another review gate.
The framework shows what has been included and what has been excluded.
It then asks whether we want to approve the changes and create a manifest.
I would recommend that everyone always create the manifest.
The reason is that the manifest acts as a record of everything that happened during the Build phase.
It tells us:
* What files were created or changed
* When they were created
* How they were created
* What structure was followed
* What was included and excluded
This becomes especially important when we reach the Audit phase because the audit needs to understand exactly what was built.
So, from my perspective, the manifest is a very important artifact.

⸻

Build Folder
Just to quickly connect this with the structure we discussed in the previous session:
During the Plan phase, under the test folder, we created the test plan and test case artifacts.
Now, during the Build phase, the framework creates a Build folder under test.
The manifest is also stored here.
So we now have a clear separation between what was planned, what test cases were created, and what automation code was actually built.

⸻

Execute Testing Code
Once the Build phase is complete, we don’t stop here.
The code has already been verified, so the next logical step is to execute it.
We simply invoke:
Execute Testing Code
This will execute the automation code that was generated during the Build phase.
The framework will run the test cases and generate the execution results.

⸻

Xray Update
Once execution is complete, the pass and fail status will be uploaded back to Xray.
Remember, these test cases were already uploaded to Xray during the Plan phase.
Now the execution phase updates those same test cases with their latest execution status.
This gives us a complete view of how the generated test cases are performing.

⸻

Get Test Data During Execution
The Execute phase can also invoke the Get Test Data skill when required.
For example, if test data is missing, expired, or needs to be refreshed during execution, Get Test Data can be called to create or manipulate the required data.
So, the different skills are not working completely independently.
They can work together as part of the overall pipeline.

⸻

Audit
Finally, we come to the Audit phase.
The purpose of Audit is to verify whether the test cases that were initially created actually satisfy the original requirement.
A common question here is:
Why do we perform the audit at the end? Why not do it at the beginning?
The reason is that we have multiple SME approval gates throughout the process.
For example, during test case review, I might decide to remove some test cases.
I could say:
“I don’t need these test cases.”
Or I might approve only three test cases and reject the remaining ones.
In that situation, the Audit phase becomes very important.
It validates whether the final result still provides sufficient coverage for the original requirement.

⸻

Audit – Traceability
The Audit phase has access to multiple artifacts.
First, it has the artifact representing the original test cases that were generated during the Plan phase.
Second, it has the manifest, which tells it exactly what was built during the Build phase.
Third, it has the execution reports, which tell it what actually happened when the automation was executed.
By comparing all of these, the Audit phase can determine whether the complete requirement has been covered.
It can identify whether:
* The requirement was covered
* The required test cases were created
* The expected automation was built
* The automation was actually executed
* The execution results are available
* Anything important was missed

⸻

PR Readiness
The final objective of the Audit phase is to determine whether the overall output is PR-ready.
Based on the analysis, Audit can also create a Pull Request.
It provides a readiness score indicating whether the PR is ready to be merged.
So whoever reviews the PR can immediately understand what functional testing has been completed as part of that user story.
They can review the generated automation, test results, coverage, and audit information, and then make the final decision on whether the PR can be approved and merged.

⸻

Conclusion
So, that’s the complete pipeline that we have covered.
We start with Plan, where we understand the requirement and generate the test cases.
Then we move to Build, where the repository is analyzed and automation code and test data are generated.
Next comes Execute, where the generated automation is actually run and the results are updated in Xray.
Finally, Audit validates the complete flow — from requirement to test cases, from test cases to code, and from code to execution.
And ultimately, the goal is to provide enough information for the final PR review and make the entire testing lifecycle much more automated and traceable.
That’s pretty much it from the complete pipeline perspective.
I’ll open it up for any questions.
