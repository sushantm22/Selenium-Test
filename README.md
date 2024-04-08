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
