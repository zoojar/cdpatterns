# **THE DEPLOYMENT PIPELINE**

The purpose of the deployment pipeline is threefold:

* Visibility: All aspects of the delivery system – building, deploying, testing, and releasing – are visible to all team members promoting collaboration.  
* Feedback: Team members learn of problems as soon as they occur so that issues are fixed as soon as possible.  
* Continually Deploy: Through a fully automated process, you can deploy and release any version of the software to any environment. (1)

In the Deployment Pipeline diagram above, all of the patterns are shown in context. There are some patterns that span multiple stages of the pipeline, so I chose the stage where it’s most predominately used.

## **BENEFITS**

* Empowering Teams: Because the deployment pipeline is a pull system, testers, developers, operations, and others can self service the application version into an environment of their choice.  
* Reducing Errors: Ensuring the correct version, configuration, database schema, etc. are applied the same way every time through automation.  
* Lowering Stress: Through push-button releases to production and Rehearsing Deployments, a release becomes commonplace without the typical stress.  
* Deployment Flexibility: Instantiate a new environment or configuration by making a few changes to the automated delivery system.  
* Practice makes Perfect: Through the deployment pipeline, the final deployment into production is being rehearsed every single time the software is deployed to any target environments. (1)

# **CONFIGURATION MANAGEMENT**

Configuration Management is “the process by which all artifacts relevant to your project, and the relationships between them, are stored, retrieved, uniquely identified, and modified”. (1) *Note: Each pattern is cited with a number in parentheses that corresponds to the source in the References section.*

## **Configurable Third-Party Software (1)**

* **Pattern** Evaluate and use third-party software that can be easily configured, deployed, and automated.
* **Anti-Patterns** Procuring software that cannot be externally configured. Software without an API or command-line interface that forces teams to use the GUI only.

## **Configuration Catalog (1)**

* **Pattern** Maintain a catalog of all options for each application, how to change these options and storage locations for each application. Automatically create this catalog as part of the build process.  
* **Anti-Patterns** Configuration options are not documented. The catalog of applications and other assets is “tribal knowledge”.

## **Mainline (3)**

* **Pattern** Minimize merging and keep the number of active code lines manageable by developing on a mainline.  
* **Anti-Patterns** Multiple branches per project.

## **Merge Daily (1)**

* **Pattern** Changes committed to the mainline are applied to each branch on at least a daily basis.  
* **Anti-Patterns** Merging every iteration once a week or less often than once a day.

## **Protected Configuration (5) ,(1)**

* **Pattern**Store configuration information in secure remotely accessible locations such as a database, directory, or registry.  
* **Anti-Patterns** Open text passwords and/or single machine or share.

## **Repository (3) , (1)**

* **Pattern**All source files – executable code, configuration, host environment, and data – are committed to a version-control repository.  
* **Anti-Patterns** Some files are checked in, others, such as environment configuration or data changes, are not. Binaries – that can be recreated through the build and deployment process – are checked in.

## **Short-Lived Branches (1)**

* **Pattern**Branches must be short lived – ideally less than a few days and never more than an iteration.  
* **Anti-Patterns** Branches that last more than an iteration. Branches by product feature that live past a release.

## **Single Command Environment (1)**

* **Pattern**Check out the project’s version-control repository and run a single command to build and deploy the application to any accessible environment, including the local development.  
* **Anti-Patterns** Forcing the developer to define and configure environment variables. Making the developer install numerous tools in order for the build/deployment to work.

## **Single Path to Production (1)**

* **Pattern**Configuration management of the entire system – source, configuration, environment and data. Any change can be tied back to a single revision in the version-control system.  
* **Anti-Patterns** Parts of system are not versioned. Inability to get back to a previously configured software system.

# **CONTINUOUS INTEGRATION (CI)**

## **Build Threshold (5)**

* **Pattern** Fail a build when a project rule is violated – such as architectural breaches, slow tests, and coding standard violations.  
* **Anti-Patterns** Manual code reviews. Learning of code quality issues later in the development cycle.

## **Commit Often (6)**

* **Pattern** Each team member checks in regularly to trunk – at least once a day but preferably after each task to trigger the CI system.  
* **Anti-Patterns** Source files are committed less frequently than daily due to the number of changes from the developer.

## **Continuous Feedback (6)**

* **Pattern** Send automated feedback from CI system to all Cross-Functional Team members.  
* **Anti-Patterns** Notifications are not sent; notifications are ignored; CI system spams everyone with information they cannot use.

## **Continuous Integration (6)**

* **Pattern** Building and testing software with every change committed to a project’s version control repository.  
* **Anti-Patterns** Scheduled builds, nightly builds, building periodically, building exclusively on developer’s machines, not building at all.

## **Stop the Line (5) , (1) , (4), (12)**

* **Pattern** Fix software delivery errors as soon as they occur; stop the line. No one checks in on a broken build as the fix becomes the highest priority.  
* **Anti-Patterns** Builds stay broken for long periods of time, thus preventing developers from checking out functioning code.

## **Independent Build (6)**

* **Pattern** Write build scripts that are decoupled from IDEs. These build scripts are executed by a CI system so that software is built at every change  
* **Anti-Patterns** Automated build relies on IDE settings. Builds are unable to be run from the command line.

## **Visible Dashboards**

* **Pattern** Provide large visible displays that aggregate information from your delivery system to provide high-quality feedback to the Cross-Functional Team in real time.  
* **Anti-Patterns** Email-only alerts or not publicizing the feedback to the entire team.

# **TESTING**

## **Automate Tests**

* **Pattern** Automate the verification and validation of software to include unit, component, capacity, functional, and deployment tests  
* **Anti-Patterns** Manual testing of units, components, deployment, and other types of tests.  
* *Unit- Automating tests without any dependencies.*  
* *Component- Automating tests with dependencies to other components and heavyweight dependencies such as the database or file system.*  
* *Deployment- Automating tests to verify the deployment and configuration were successful. Sometimes referred to as a “smoke tests”.*  
* *Functional- Automating tests to verify the behavior of the software from a user’s perspective.*  
* *Capacity- Automating load and performance testing in near- production conditions.*

## **Isolate Test Data (1)**

* **Pattern** Use transactions for database-dependent tests (e.g., component tests) and roll back the transaction when done. Use a small subset of data to effectively test behavior  
* **Anti-Patterns** Using a copy of production data for Commit Stage tests. Running tests against a shared database.

## **Parallel Tests (1)**

* **Pattern** Run multiple tests in parallel across hardware instances to decrease the time in running tests.  
* **Anti-Patterns** Running tests on one machine or instance. Running dependent tests that cannot be run in parallel.

## **Stub Systems (1)**

* **Pattern** Use stubs to simulate external systems to reduce deployment complexity.  
* **Anti-Patterns** Manually installing and configuring interdependent systems for Commit Stage build and deployment.

# **DEPLOYMENT PIPELINE**

## **Deployment Pipeline (1)**

* **Pattern** A deployment pipeline is an automated implementation of your application’s build, deploy, test, and release process.  
* **Anti-Patterns** Deployments require human intervention (other than approval or clicking a button). Deployments are not production ready.

## **Value-Stream Map (4) \#\#**

* **Pattern** Create a map illustrating the process from check in to the version-control system to the software release to identify process bottlenecks.  
* **Anti-Patterns** Separately defined processes and views of the checkin to release process.

# **BUILD AND DEPLOYMENT SCRIPTING**

## **Dependency Management (5)**

* **Pattern** Centralize all dependent libraries to reduce bloat, classpath problems, and repetition of the same dependent libraries and transitive dependencies from project to project.  
* **Anti-Patterns** Multiple copies of the same binary dependencies in each and every project. Redefining the same information for each project. Classpath hell\!

## **Common Language (1)**

* **Pattern** As a team, agree upon a common scripting language – such as Perl, Ruby, or Python – so that any team member can apply changes to the Single Delivery System  
* **Anti-Patterns** Each team uses a different language making it difficult for anyone to modify the delivery system reducing cross-functional team effectiveness.

## **Externalize Configuration (5)**

* **Pattern** Changes between environments are captured as configuration information. All variable values are externalized from the application configuration into build/deployment-time properties  
* **Anti-Patterns** Hardcoding values inside the source code or per target environment.

## **Fail Fast (6)**

* **Pattern** Fail the build as soon as possible. Design scripts so that processes that commonly fail run first. These processes should be run as part of the Commit Stage.  
* **Anti-Patterns** Common build mistakes are not uncovered until late in the deployment process.

## **Fast Builds (6)**

* **Pattern** The Commit Build provides feedback on common build problems as quickly as possible – usually in under 10 minutes.  
* **Anti-Patterns** Throwing everything into the commit stage process, such as running every type of automated static analysis tool or running load tests such that feedback is delayed.

## **Scripted Deployment (5)**

* **Pattern** All deployment processes are written in a script, checked in to the version-control system, and run as part of the Single Delivery System.  
* **Anti-Patterns** Deployment documentation is used instead of automation.Manual deployments or partially manual deployments. Using GUI to perform a deployment.

## **Unified Deployment (5)**

* **Pattern** The same deployment script is used for each deployment. The Protected Configuration – per environment – is variable but managed.  
* **Anti-Patterns** Different deployment script for each target environment or even for a specific machine. Manual configuration after deployment for each target environment.

# **DEPLOYING AND RELEASING APPLICATIONS**

## **Binary Integrity (5)**

* **Pattern** Build your binaries once, while deploying the binaries to multiple target environments, as necessary.  
* **Anti-Patterns** Software is built in every stage of the deployment pipeline.

## **Canary Release**

* **Pattern** Release software to production for a small subset of users (e.g. , 10%) to get feedback prior to a complete rollout.  
* **Anti-Patterns** Software is released to all users at once.

## **Blue-Green Deployments (1)**

* **Pattern** Deploy software to a non-production environment (call it blue) while production continues to run. Once it’s deployed and “warmed up”, switch production (green) to non-production and blue to green simultaneously.– **Anti-Patterns** Production is taken down while the new release is applied to production instance(s).

## **Dark Launching (11)**

* **Pattern** Launch a new application or features when it affects the least amount of users.  
* **Anti-Patterns** Software is deployed regardless of number of active users.

## **Rollback Release (5)**

* **Pattern** Provide an automated single command rollback of changes after an unsuccessful deployment.  
* **Anti-Patterns** Manually undoing changes applied in a recent deployment. Shutting down production instances while changes are undone.

## **Self-Service Deployment (1)**

* **Pattern** Any Cross-Functional Team member selects the version and environment to deploy the latest working software.  
* **Anti-Patterns** Deployments released to team are at specified intervals by the “Build Team”. Testing can only be performed in a shared state without isolation from others.

# **INFRASTRUCTURE AND ENVIRONMENTS**

## **Automate Provisioning (1)**

* **Pattern** Automate the process of configuring your environment to include networks, external services, and infrastructure.  
* **Anti-Patterns** Configured instances are “works of art” requiring team members to perform partially or fully manual steps to provision them.

## **Behavior-Driven Monitoring (1)**

* **Pattern** Automate tests to verify the behavior of the infrastructure. Continually run these tests to provide near real-time alerting.  
* **Anti-Patterns** No real-time alerting or monitoring. System configuration is written without tests.

## **Immune Systems**

* **Pattern** Deploy software one instance at a time while conducting Behavior-Driven Monitoring. If an error is detected during the incremental deployment, a Rollback Release is initiated to revert changes.  
* **Anti-Patterns** Non-incremental deployments without monitoring.

## **Lockdown Environments (1)**

* **Pattern** Lock down shared environments from unauthorized external and internal usage, including operations staff. All changes are versioned and applied through automation.  
* **Anti-Patterns** The “Wild West”: any authorized user can access shared environments and apply manual configuration changes, putting the environment in an unknown state leading to deployment errors.

## **Production-Like Environments (1)**

* **Pattern** Target environments are as similar to production as possible.  
* **Anti-Patterns** Environments are “production like” only weeks or days before a release. Environments are manually configured and controlled.

## **Transient Environments**

* **Pattern** Utilizing the Automate Provisioning, Scripted Deployment and Scripted Database patterns, any environment should be capable of terminating and launching at will.  
* **Anti-Patterns** Environments are fixed to “DEV, QA” or other pre-determined environments.

# **DATA**

## **Database Sandbox (7)**

* **Pattern** Create a lightweight version of your database – using the Isolate Test Data pattern. Each developer uses this lightweight DML to populate his local database sandboxes to expedite test execution.  
* **Anti-Patterns** Shared database. Developers and testers are unable to make data changes without it potentially adversely affecting other team members immediately.

## **Decouple Database (1)**

* **Pattern** Ensure your application is backward and forward compatible with your database so you can deploy each independently  
* **Anti-Patterns** Application code data are not capable of being deployed separately.

## **Database Upgrade (7)**

* **Pattern** Use scripts to apply incremental changes in each target environment to a database schema and data.  
* **Anti-Patterns** Manually applying database and data changes in each target environment.

## **Scripted Database (7)**

* **Pattern** Script all database actions as part of the build process.  
* **Anti-Patterns** Using data export/import to apply data changes. Manually applying schema and data changes to the database.

# **INCREMENTAL DEVELOPMENT**

## **Branch by Abstraction (2)**

* **Pattern** Instead of using version-control branches, create an abstraction layer that handles both an old and new implementation. Remove the old implementation.  
* **Anti-Patterns** Branching using the version-control system leading to branch proliferation and difficult merging. Feature branching.

## **Toggle Features (10)**

* **Pattern** Deploy new features or services to production but limit access dynamically for testing purposes.  
* **Anti-Patterns** Waiting until a feature is fully complete before committing the source code.

# **COLLABORATION**

## **Delivery Retrospective (1)**

* **Pattern** For each iteration, hold a retrospective meeting where everybody on the Cross-Functional Team discusses how to improve the delivery process for the next iteration.  
* **Anti-Patterns** Waiting until an error occurs during a deployment for Dev and Ops to collaborate. Having Dev and Ops work separately.

## **Cross-Functional Teams (1)**

* **Pattern** Everybody is responsible for the delivery process. Any person on the Cross-Functional Team can modify any part of the delivery system.  
* **Anti-Patterns** Siloed teams: Development, Testing, and Operations have their own scripts and processes and are not part of the same team.  
  Amazon.com has an interesting take on this approach. They call it “You build it, you run it”. Developers take the software they’ve written all the way to production.

## **Root-Cause Analysis (1)**

* **Pattern** Learn the root cause of a delivery problem by asking “why” of each answer and symptom until discovering the root cause.  
* **Anti-Patterns** Accepting the symptom as the root cause of the problem.

# **TOOLS**

This is meant to be an illustrative list, not an exhaustive list, to give you an idea of the types of tools and some of the vendors that help to enable effective Continuous Delivery. The Java, .NET and Ruby platforms are represented. The tools that span categories have been assigned to the most appropriate category or duplicated when necessary.

* **Configuration Management** Subversion (SVN), git, Perforce, PassPack, PasswordSafe, ESCAPE, ConfigGen  
* **Continuous Integration** Bamboo, Jenkins, AntHill Pro, Go, TeamCity, TFS 2010, Electric Commander  
  * **Supporting tools:** Doxygen, Grand, GraphViz, JavaDoc, NDoc, SchemaSpy, UmlGraph, CheckStyle, Clover, Cobertura, FindBugs,FxCop, JavaNCSS, JDepend, PMD, Sonar, Simian  
* **Testing** Twist , AntUnit, Cucumber, DbUnit, webrat, easyb, Fitnesse, JMeter, JUnit, NBehave, SoapUI, Selenium, RSpec, SauceLabs  
* **Deployment Pipeline** Go, AntHill Pro  
* **Build and Deployment Scripting** Ant, AntContrib, NAnt, MSBuild, Buildr, Gant, Gradle, make, Maven, Rake, Java Secure Channel, ControlTier, Altiris, Capistrano, Fabric, Func  
* **Infrastructure and Environments** AWS EC2, AWS S3, Windows Azure, Google App Engine, AWS Elastic Beanstalk, Heroku, Capistrano, Cobbler, BMC Bladelogic, CFEngine, IBM Tivoli Provisioning Manager, Puppet, Chef, Bcfg2, AWS Cloud Formation, Windows Azure AppFabric, rPath, JEOS, BoxGrinder, CLIP, Eucalyptus, AppLogic, CloudKick, CloudWatch, Nagios, Zabbix, Zenoss  
* **Data** Hibernate, MySQL, Liquibase, Oracle, PostgreSQL, SQL Server, SimpleDB, SQL Azure, Ant, MongoDB, dbdeploy  
* **Components and Dependencies** Ivy, Archiva, Nexus, Artifactory, Bundler  
* **Collaboration** Mingle, Greenhopper, JIRA

# **REFERENCES**

1. Jez Humble and David Farley, “Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation”, Addison Wesley Professional, 2010  
2. Paul Hammant and www.continuousdelivery.com  
3. Stephen P. Berczuk and Brad Appleton, “Software Configuration Management Patterns.”, Addison Wesley Professional, 2003  
4. Mary and Tom Poppendieck, “Leading Lean Software Development”, Addison Wesley, 2009  
5. Paul M. Duvall, “Continuous integration. Patterns and Antipatterns”, DZone refcard \#84, 2010 [http://bit.ly/l8rfVS](http://bit.ly/l8rfVS)  
6. Paul M. Duvall, “Continuous integration. Improving Software Quality and Reducing Risk”, Addison Wesley, 2007  
7. Scott W. Ambler and Pramodkumar J. Saladage, “Refactoring Databases. Evolutionary Database Design”, Addison Wesley, 2006\.  
8. Paul M. Duvall, IBM developerWorks series “Automation for the people” [http://ibm.co/iwwvPX](http://ibm.co/iwwvPX)  
9. IMVU: [http://bit.ly/jhqP5f](http://bit.ly/jhqP5f)  
10. Martin Fowler and Facebook: [http://on.fb.me/miBrOM](http://on.fb.me/miBrOM)  
11. Facebook Engineering: [http://on.fb.me/miBrOM](http://on.fb.me/miBrOM)  
12. Paul Julius, Enterprise Continuous Integration Maturity Model, [http://bit.ly/m7h5vC](http://bit.ly/m7h5vC)

