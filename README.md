

All right, so let’s first understand what Agentic Shift Left Testing actually means.

From a QA perspective, this is how we work today. Whenever a Jira ticket is assigned to us, we perform functional testing first. This is usually done in the SIT or QA0 environment. Once the sprint work is completed, we perform regression testing, which is generally executed in the QA environment before the release.

Now, with the shift-left testing model, this entire approach is going to change. With AI becoming a core part of our engineering workflow, the goal is to make testing faster, more productive, and more automated.

Whenever we talk about faster product delivery, a few common questions always come up:

* Are all our test cases automated?
* Do we have enough test coverage?
* Can testing start as soon as development begins instead of waiting until later?

To solve these challenges, we have introduced AI-powered Agents and Skills.

Most of you have probably heard about AI agents already, but today I’ll also introduce Skills, explain what they are, how they have been developed, and what will be expected from us going forward.

⸻

What is changing?

The biggest change is the ownership of functional testing.

Traditionally, QA teams have been responsible for planning test cases, performing functional testing, creating in-sprint automation, and finally executing regression testing before every release.

In the new model, a large part of the functional testing responsibility shifts towards the development team, while QA focuses more on release regression, end-to-end testing, accessibility testing, and overall quality validation.

You’ll notice on the architecture slide that Development owns the early testing activities, while QA owns release validation.

The input to this process can either be a Jira story or, in the future, a Specification. The reason both are supported is because the organization is exploring Spec-Driven Development. While Jira is still being used today, future development may move towards specification-based workflows. Therefore, the AI skills are designed to support both approaches.

⸻

Four Phases of Agentic Testing

To achieve this workflow, the entire process has been divided into four phases:

* Plan
* Build
* Execute
* Audit

Let’s understand each phase one by one.

⸻

Phase 1 – Plan

This is where everything begins.

In today’s process, when a user story is assigned, we first understand the requirement. We review the Jira story, acceptance criteria, comments, Epic, Figma designs, Confluence pages, or any other available documentation.

Based on this information, we prepare a test plan and identify all the functional test cases required to validate the feature.

This planning activity is exactly what the Plan Skill automates.

Instead of manually creating test plans and identifying scenarios, AI performs the analysis and generates them automatically.

⸻

Phase 2 – Build

Once the test cases are ready, the next step is automation.

During the Build phase, AI analyzes the existing automation framework and understands how automation has already been implemented.

It then generates the automation code for the newly created test cases.

Along with code generation, it also creates the required test data.

The Build phase understands the existing framework structure, coding standards, and test data format so that the generated automation remains consistent with the current framework.

In simple terms:

* Plan creates the test cases.
* Build creates the automation code and test data.

⸻

Phase 3 – Execute

The Execute phase is straightforward.

Once the automation code has been generated, the framework executes the test cases.

It performs the execution, collects the results, and reports whether each scenario has passed or failed.

⸻

Phase 4 – Audit

The final phase is Audit.

Here the framework validates whether the generated test cases actually cover the complete business requirement.

This is similar to the review that a QA Lead or Senior QA would normally perform to ensure that nothing has been missed.

Once the audit is completed successfully, we can say that the functional testing activity has been completed.

⸻

Training Roadmap

Today’s session is focused only on the Plan phase.

The complete workflow has been divided into multiple sessions.

Today’s session covers how the Plan Skill works and how test plans and test cases are generated.

The next session will cover the Build phase.

After that, we’ll discuss the Execute and Audit phases.

We’ll also have a dedicated Q&A session so that everyone gets enough time to understand the Plan phase before moving further.

⸻

Overall Flow

To summarize the complete workflow:

Developers will own functional testing.

The Plan phase creates the test plan and functional test cases.

The Build phase generates automation code and prepares test data.

The Execute phase runs the automation.

Finally, the Audit phase validates that the generated tests provide complete coverage.

⸻

Calling the Skill

Now let’s see how these skills are actually invoked.

To generate test cases, we simply use the command:

/create-test-case

followed by the Jira ticket ID.

There is no need to explicitly call the Plan phase.

Once this command is executed, the Plan Skill is automatically triggered.

Behind the scenes, the skill interacts with multiple systems including Jira (Atlassian), Figma, Playwright, and other internal integrations.

⸻

Test Plan Creation

The first thing the skill does is check whether the Epic already contains a test plan.

Suppose this user story belongs to an Epic.

The skill navigates to that Epic and checks whether a test plan already exists.

If a test plan is available, it reuses it.

If not, it asks whether a new test plan should be created.

The reason for storing test plans at the Epic level is simple.

A single test plan can be reused across multiple user stories within the same Epic, reducing duplicate work and saving AI tokens.

For example, if an Epic contains 30 or 40 stories, all of them can share the same high-level test plan.

⸻

Skills vs Agents

You may already be familiar with Agents from the migration activity.

Agents are selected from the dropdown and generally require instruction files to be added as context.

Skills work differently.

They are stored inside the Skills folder within the repository and can simply be invoked using slash commands like:

/create-test-case

No additional setup is required.

⸻

Test Plan Contents

The generated test plan contains multiple sections.

It identifies:

* What is in scope
* What is out of scope
* Any assumptions or exemptions
* Child stories associated with the Epic
* Requirement traceability
* Overall Epic coverage and readiness

This gives complete visibility into what will and will not be tested.

⸻

SME Approval Gate

Once the test plan is generated, an SME approval gate is introduced.

If no test plan exists, the framework asks:

“No test plan was found for this Epic. Would you like me to create one?”

You can simply reply:

Yes

or

No

If you choose Yes, the framework generates the complete test plan.

As a reviewer, you can examine the generated content.

If any modifications are required, you can ask AI to update the plan.

Once satisfied, you simply approve it and the framework uploads it back to the Epic.

Human review remains an important part of this workflow.

⸻

Test Case Generation

Once the test plan is approved, the framework moves to the next stage—creating the actual test cases.

Internally, all generated artifacts are stored inside a test folder containing:

* Test Plan
* Test Cases
* Execution assets

For generating test cases, the framework doesn’t rely on a single AI model.

Instead, it uses three different LLMs.

Think of it as having three experienced QA engineers independently reviewing the same requirement.

Each LLM generates its own set of test cases.

For example:

* LLM A may generate 24 test cases.
* LLM B may generate 20 test cases.
* LLM C may generate 19 test cases.

These three outputs are then compared, consolidated, and deduplicated.

The final result is a much stronger and more comprehensive test suite than what a single model could generate.

⸻

Accessibility Validation

After functional test cases are generated, the framework asks whether accessibility test cases should also be created.

If accessibility is in scope, simply answer Yes.

Otherwise, answer No.

This allows the framework to generate both functional and accessibility test cases as part of the same workflow.

⸻

Human Review

Before anything is finalized, all generated test cases are presented for review.

The test cases are written in standard Given-When-Then format.

At this stage, you can:

* Approve a test case.
* Modify it.
* Delete it.
* Add additional test cases.

This ensures that AI remains under human supervision before anything is committed.

⸻

Final Upload

Once all test cases have been reviewed and approved, the framework uploads the generated test plan and all approved test cases back to the Epic.

At the end, it provides a summary showing everything that was created and asks for final confirmation before completing the process.

That completes the overall workflow of the Plan phase.

































Certainly! Here’s a personalized goodbye email for your Gift City team:

---

Subject: Farewell and Heartfelt Thanks

Dear Gift City Team,

As I prepare to say goodbye, I find myself filled with gratitude and a bit of nostalgia. Today marks my last day here, and while I'm excited about what the future holds, it's incredibly hard to leave behind such a fantastic group of people.

My time here at Gift City has been nothing short of extraordinary. The bond we have shared is something I will always treasure. There was never a dull moment, whether we were tackling challenging projects or simply enjoying each other’s company. Our lunches, dinners, and team outings are memories I will hold dear. You all made work feel less like a job and more like spending time with friends.

Working with each of you has been a privilege. Your support, laughter, and camaraderie have made my journey here truly special. We’ve celebrated successes, faced challenges, and grown together in ways I will always be proud of. You have not just been colleagues but friends who have made a significant impact on my life.

I will deeply miss our time together—the jokes, the shared meals, and the amazing experiences. It’s rare to find such a cohesive and supportive team, and I feel incredibly fortunate to have been a part of it.

Though I’m moving on to new adventures, I would love to stay in touch with all of you. Please feel free to reach out to me anytime at [your personal email]. Let’s continue to share our journeys and keep our wonderful connections alive.

Thank you all for everything. It has been an absolute joy to work alongside such remarkable individuals. I wish you all continued success, happiness, and many more wonderful moments together.

Warmest regards,

[Your Name]

---

Feel free to adjust any part of the message to better fit your personal experiences and sentiments. Best wishes on your new journey!





GENERAL TEAM MAIL:
Sure! Here is a farewell email for your last working day:

---

Subject: Farewell and Thank You

Dear Team,

As many of you know, today marks my last working day with [Company Name]. It has been a remarkable journey filled with both professional growth and personal memories that I will cherish.

Working at [Company Name] has been an invaluable experience. I am grateful for the opportunities I've had to contribute to our projects, collaborate with such talented individuals, and learn from all of you. Your support and camaraderie have made my time here truly special.

I want to extend my heartfelt thanks to everyone for your guidance, encouragement, and friendship over the years. Each of you has played a significant role in my journey, and for that, I am deeply appreciative.

Though I am moving on to new challenges and opportunities, I hope our paths cross again in the future. Please keep in touch—you can reach me at [your personal email address or LinkedIn profile link].

Wishing you all continued success and happiness.

Warm regards,

[Your Full Name]  
[Your Job Title]  
[Your Contact Information]

---

Feel free to customize it further to suit your style and specific circumstances.







# Java TestNG Selenium 

### Environment Setup

1. Global Dependencies
    * Install [Maven](https://maven.apache.org/install.html)
    * Or Install Maven with [Homebrew](http://brew.sh/) (Easier)
    ```
    $ install maven
    ```
2. Project Dependencies
    * checkout the repository
    * Check that packages are available
    ```
    $ cd Java-TestNG-Selenium
    ```
    * You may also want to run the command below to check for outdated dependencies. Please be sure to verify and review updates before editing your pom.xml file as they may not be compatible with your code.
    ```
    $ mvn versions:display-dependency-updates
    ```




   

**LambdaTest Authentication Credentials:** Make sure you have your LambdaTest credentials with you to run test automation scripts with Jest on LambdaTest Selenium Grid. You can obtain these credentials from the [LambdaTest Automation Dashboard](https://automation.lambdatest.com/) or through [LambdaTest Profile](https://accounts.lambdatest.com/detail/profile).

Set LambdaTest Username and Access Key in environment variables.

* For Linux/macOS:
`export LT_USERNAME="YOUR_USERNAME"
export LT_ACCESS_KEY="YOUR ACCESS KEY"`

* For Windows:
`set LT_USERNAME="YOUR_USERNAME"
set LT_ACCESS_KEY="YOUR ACCESS KEY"`
    
### Running Tests

```
To run single test
    $ mvn test -D suite=single.xml

To run parallel test

    $ mvn test -D suite=single.xml


```
## About LambdaTest

[LambdaTest](https://www.lambdatest.com/) is a cloud based selenium grid infrastructure that can help you run automated cross browser compatibility tests on 2000+ different browser and operating system environments. LambdaTest supports all programming languages and frameworks that are supported with Selenium, and have easy integrations with all popular CI/CD platforms. It's a perfect solution to bring your [selenium automation testing](https://www.lambdatest.com/selenium-automation) to cloud based infrastructure that not only helps you increase your test coverage over multiple desktop and mobile browsers, but also allows you to cut down your test execution time by running tests on parallel.


--------------------------------------------


Sure, here's a basic example of C# code to connect to an Oracle database and execute a script on the server:using System;
using Oracle.ManagedDataAccess.Client;

class Program
{
    static void Main()
    {
        string connectionString = "Data Source=<your_data_source>;User Id=<your_username>;Password=<your_password>;";

        try
        {
            using (OracleConnection connection = new OracleConnection(connectionString))
            {
                connection.Open();

                // Write your SQL script here
                string sqlScript = "SELECT * FROM your_table";

                using (OracleCommand command = new OracleCommand(sqlScript, connection))
                {
                    using (OracleDataReader reader = command.ExecuteReader())
                    {
                        while (reader.Read())
                        {
                            // Process the result if needed
                            Console.WriteLine(reader.GetString(0));
                        }
                    }
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("An error occurred: " + ex.Message);
        }
    }
}
Make sure to replace <your_data_source>, <your_username>, and <your_password> with your actual database connection details. Also, replace "SELECT * FROM your_table" with your actual SQL script.Note: This code assumes you have installed the Oracle Managed Data Access (ODP.NET) NuGet package. You can install it via NuGet Package Manager or using the following command in the Package Manager Console:Install-Package Oracle.ManagedDataAccess
