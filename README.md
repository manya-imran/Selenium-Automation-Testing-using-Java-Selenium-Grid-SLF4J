# Selenium-Automation-Testing-using-Java-Selenium-Grid-SLF4J

For this assignment we're using Selenium powered web automation testing on a URL
```
https://www.saucedemo.com
```

To set up we need to understand the workflow of this assignment:
We have Automated 7 test cases using parellel exceution in Selenium Grid. We have also utilized both Chrome and Firefox (gecko) drivers. If you want to add more drivers to the Grid Session navigate to the \resourses folder and add your driver executable file.

First you need to set up Selenium Grid
- Add the ```selenium-server-<version>.jar``` file in \libs folder.
- Then add a 'config.toml' having the information of your drivers.

Here's what your config.toml should look like to run Grid on port 4444 and server on 5555. You can access Grid status at http://localhost:4444/ui
```
[node]
detect-drivers = true
hub = "http://localhost:4444"

[server]
port = 5555  # Or whichever port you'd like to use for your node

[driver-configuration]
# These are the paths to your specific drivers
webdriver.chrome.driver = "D:/JetBrains/Projects/selenium-assign/resources/chromedriver.exe"
webdriver.gecko.driver = "D:/JetBrains/Projects/selenium-assign/resources/geckodriver.exe"

```
After adding the required files you need to start your Grid. Use the following command:
```
java -jar .\libs\selenium-server-<version>.jar hub
```
Then add the driver information using config.toml:
```
java -jar .\libs\selenium-server-<version>.jar node --config ".\libs\config.toml"
```
After that your environment is ready to execute tests.
To execute test you need an XML file having the tags and classes you want to automate. Lets first understand the testcases to automate then we'll add them in the testing file.
1. Automate Login - \src\test\login\LoginTest
2. Add Items to Cart - Products Page  - \src\test\Products\AddToCart
3. Add Items to Cart - Product Details Page  - \src\test\ProductDetails\productDetailsTests
4. Add Items to Cart - Cart Page - \src\test\Checkout\CartManageTest
5. Buy Items - \src\test\Checkout\PurchaseTest
6. Cart Retention after Login Test - \src\test\CartRetention\cartRetentionCheck
7. Sorting Options Test - \src\test\Products\SortTests

Now we need to add all of our test flows into the XML file to test the automated test cases. Set ```parallel="classes"``` in suite level to excute testcases in parallel.
```
<suite name="Selenium Grid Suite"  parallel="classes">
    <test name="ChromeTest">
        <parameter name="browser" value="chrome" />
<!--        <groups>-->
<!--            <run>-->
<!--                <include name="Login Test"/>-->
<!--            </run>-->
<!--        </groups>-->

        <classes>
            <class name="login.LoginTest" />
            <class name="CartRetention.cartRetentionCheck"/>
            <class name="Checkout.CartManageTest"/>
            <class name="Checkout.PurchaseTest"/>
            <class name="ProductDetails.productDetailsTests"/>
            <class name="Products.AddToCart"/>
            <class name="Products.SortTests"/>
        </classes>
    </test>
    <test name="FirefoxTest">
        <parameter name="browser" value="firefox" />
        <classes>
            <class name="login.LoginTest" />
            <class name="CartRetention.cartRetentionCheck"/>
            <class name="Checkout.CartManageTest"/>
            <class name="Checkout.PurchaseTest"/>
            <class name="ProductDetails.productDetailsTests"/>
            <class name="Products.AddToCart"/>
            <class name="Products.SortTests"/>
        </classes>
    </test>
</suite>
```
If you are using IntelliJ IDE you can right click on the XML file and select run the XML file. If you are using Maven in any other IDE you can use 
```
mvn test -Dsurefire.suiteXmlFiles=src/test/resources/yourTestNG.xml
```
And because we have implemented the SLF4J logger in our assigment we'll see our test cases being logged in our console like the following. You can change its format in the src\test\resources\logback.xml file
```
17:28:37.340 [TestNG-test=FirefoxTest-3] INFO  testautomatinau.BaseTest - Post Login Workflow Started
17:28:37.340 [TestNG-test=FirefoxTest-3] INFO  Checkout.CartManageTest - Add to Cart from Cart Page
17:28:37.340 [TestNG-test=FirefoxTest-3] INFO  Checkout.CartManageTest - Adding items
not-clicking
17:28:37.414 [TestNG-test=FirefoxTest-2] INFO  testautomatinau.BaseTest - Post Login Workflow Started
not-clicking
17:28:37.450 [TestNG-test=FirefoxTest-4] INFO  testautomatinau.BaseTest - Post Login Workflow Started
not-clicking
17:28:37.517 [TestNG-test=FirefoxTest-1] INFO  testautomatinau.BaseTest - Post Login Workflow Started
17:28:37.543 [TestNG-test=FirefoxTest-1] INFO  login.LoginTest - Product Page Loaded
AfterClass
17:28:37.807 [TestNG-test=FirefoxTest-3] INFO  Checkout.CartManageTest - Viewing Cart
17:28:38.069 [TestNG-test=FirefoxTest-3] INFO  Checkout.CartManageTest - Getting Item Count
```
And this is how you automate and test the workflow of a website. Hope it helps.


