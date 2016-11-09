## Deployment Automation?
Note:  How do you automate deployment of an On Premise product that has dozens of different deployment strategies all controlled by the customer?  The product supports 4 operating system, 2 relational databases and 3 OLAP Engines, and that is before the customer even starts to configure the product.


#### Deployment Automation
## Mimic the Customer
Note:  This is the same concept as in normal DevOps where you automate the service deployment, but you have to make the automation itself
configuable so that you can mimic all of the customers, instead of just the internal operations.


#### Deployment Automation
## Customer Deployment
* Run the Installer
* Configure the product
* Load Data
Note:  So to mimic the customer's deployment behavior we need to be able to automate three major tasks.  The installer is created by a 3rd party commercial tool that you are all probably familiar with at least as a user.  The product is highly configuable which makes it possible to be used by a wide range of Enterprice customers so the configuration step can by length to say the least.  Loading the data is fairly straight forward, but the shape of the data needs to exactly match the configuration, so we need a way to match up the gigabytes of custom data to the specific configuration.


#### Deployment Automation
## Automate the Installer?
Note:  So the first step is to automate the installation tool, we had a couple of false starts here where we attempted to use the tools built in silent install suppport.  But this lead to a difficult to maintain automation that needed detailed knowledge about the installer to maintain.  We also wanted to exactly mimic the behavior of our customers for the most accurate test, so we needed a better way.


#### Deployment Automation
## Installer Console Mode
Note:  Our installer supports a simple text based console mode as well as the more typical graphical mode.
So our solution was to simply run the Installer process from the JVM, capture the input and output streams.
By reading the installer text and responding to the questions it asks it becomes relatively trivial to automte using a Gradle task.


#### Deployment Automation
## Example Task
    task installSimpleSetup(type: com.pros.gradle.SilentInstall) {
        installerTarBall = ...

        consoleValues = [
            'Installation Directory': installDir,
            ...
            'Java Home Directory': javaHome,
            'Max JVM Memory (DEFAULT: -Xmx512M): ': '-Xmx2G'
        ]
    }
Note:   To us the taks you just point the task to where it can find the installer's tarball, and give it a map of questions and responses.
The tasks unpacks the tarball and executes the installer, it searches the text output by the installer until it ends with the Key in the map, then it responds with the cooresponding value.  By setting some values from Gradle properties it allows the automation to be very flexible and a single task definition to work for many different environments.  We are also able to use the automation for both clean installs and upgrades.


#### Deployment Automation
## Configure & Load Data?
Note:  So with the installation fully automated we now need to handle configuring the product and loading data.


#### Deployment Automation
#### Configure & Load Data
## DSL to automate the product
Note:  To stay as close as possible to the way that the customers handle this we just created a very simple DSL around the existing product features.  For the most part this is through command line processes, but in some cases the DSL is wrapping web service calls.  With the DSLs in place the system setup automation is easy to maintain by anyone familiar with the product.


#### Deployment Automation
#### Configure & Load Data
## Example Task
    ext.productInstallDir = file(installDir)
    task dataLoadQaAllModules() {
        finalizedBy stopServices
        doFirst() {
            startServices()
            addToUserProps ['default.timeout': '3600']
            invokeProductTask 'loadProductData'
            invokeProductTask 'loadCustomerData'
        }
    }

Note:  The DSL just goes inside a simple doFirst() block and the QEs that are maintaining the deployments can just ignore the gradle task information.  In a real implementation the configuration steps averages between 50 and 200 steps, but they are still relatively easy to understand.


#### Deployment Automation
#### Configure & Load Data
## DSL Implementation
    project.metaClass.invokeProductTask << { List<String> args ->
        exec {
            workingDir = project.productInstallDir
            commandLine = ['./product.sh',] + args
        }
    }
Note:  We are using basic groovy metaprogramming to add the new DSL directly to the Gradle project object when our plugin is applied.
I left all of the error checking off the example to make it fit on a slide, but the user must store the product install directory on the
project object once so that all of the DSL methods can access it without it being repeated in every call.


#### Deployment Automation
## Why Gradle?
Note:  Nothing that I have mentioned so far requires Gradle, we could have implemented all of this using dozens of tools.  So what made Gradle the best fit.


#### Deployment Automation
#### Why Gradle?
## Dependency Resolution
    task installSimpleSetup(type: com.pros.gradle.SilentInstall) {
        installerTarBall = project.configurations.installer.singleFile
        ...
    }
Note:  We make extensive use of Gradle's dependency resolution to download the correct version of the product, and the datafiles that need to be loaded.  We don't need to do any special work ourselves to make this work, other than publishing all of the artifacts form their builds.  No Error handling, no integrity checks, no uneeded downloads, etc...  From this example you can see one way we automate the downloading of the installer to the local machine for use.


#### Deployment Automation
#### Why Gradle?
## Built in Functions
* Exec
* JavaExec
* Copy
* UnZip
* UnTar
Note:   Gradle's built in functions make it so easy to do 90% of the tasks we need to automate the deployment.  Instead of writing our own code for each of these tasks it is trivial to just use what Gradle provides.


#### Deployment Automation
#### Why Gradle?
## ![Deploy Task Graph](images/Deploy-TaskGraph.png)
Note:  Because we are doing all of the automation steps through gradle tasks we can use the standard gradle tasks dependency graph to make reuse trivial. We end up having four or five install tasks that are used by several dozen configuration tasks, and there are slightly more than a one to one relationship between configuration and data.

