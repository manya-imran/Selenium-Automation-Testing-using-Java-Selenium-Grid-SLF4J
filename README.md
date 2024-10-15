﻿# Selenium-Automation-Testing-using-Java-Selenium-Grid-SLF4J

For this assignment we're using Selenium powered web automation testing on a URL
```
https://www.saucedemo.com
```

To set up we need to understand the workflow of this assignment:
We have Automated 7 test cases using parellel exceution in Selenium Grid. We have also utilized both Chrome and Firefox (gecko) drivers. If you want to add more drivers to the Grid Session navigate to the \resourses folder and add your driver executable file.

First you need to set up Selenium Grid
- Add the selenium-server-<version>.jar file in \libs folder.
- Then add a 'config.toml' having the information of your drivers.

Here's what your config.toml should look like ro run Grid on port 4444 and server on 5555. You can access Grid status at http://localhost:4444/ui
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
java -jar .\libs\selenium-server-4.25.0.jar node --config ".\libs\config.toml"
```
After that your environment is ready to execute tests.

