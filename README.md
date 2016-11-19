This document defines the general process management guidelines we will adhere to.  It is intentionally lean and covers primarily how individual releases are managed.

* [Scope Management](#scope-management)
  * [Release Scope] (#release-scope)
  * [Operational Scope] (#operational-scope)
* [Task Management](#task-management)
  * [Integration Testing](#integration-testing)
  * [Failed Tests](#failed-tests)
* [Release Closure](#release-closure)
* [Tool Configuration](#tool-configuration)
  * [GitHub Issues](#github-issues)
  * [Waffle.io](#waffle)

# Scope Management
There are two forms of scope that we have to manage. The first is planned release scope, and the second is operational scope. Tasks generated by both sets of scope will follow the same task management process, but the method by which items are introduced to the scope and packaged in deliverables varies.

Generally speaking, release scope covers work that needs to be done for the next set of features. Releases are planned in advance and are time boxed with expected release dates. Code changes for releases are performed on the trunk. Operational scope covers bugs or newly discovered needs that cannot wait until the current release cycle completes and must be deployed as a hot-fix.

### Release Scope
For release scope we are using a predictive model (within the scope of a release) in which the set of work to be performed will be determined prior to work beginning on the release. Once the set of work is committed to, no additional work can be added without evaluating how it will impact the release.

The starting scope of work for a given release will be determined in two phases, using primarily expert judgement.  First, the analysts and project lead will create the initial list of planned work items by assigning them to the appropriate milestones. Once the initial list is compiled, the development team will be notified that the milestone items are loaded and can be reviewed.  Ideally, this will occur 2-3 days before the release starts to provide time for resolution of questions and concerns about level of effort.

### Operational Scope
For operational scope we are using an adaptive approach with dynamically determined releases. Most operational scope items are considered to be immediate needs and take priority over release scope items.  As such, the impact of adding of operational scope should be juxtaposed against the impact to the the scope or timing of the current release.

Issues that arise during the course of business should typically only be handled as an operational item if it is actively inhibiting operations. When performing impact analysis on new issues try to keep in mind that the default preference is to hold issues until a formal release, and that the purpose of impact analysis is to determine if the issue justifies deviating from preference.

For example, a small issue that only affects staff and has a known work-around does not necessarily need to be hot-fixed even if it is a quick fix, as it is not actively limiting the company's ability to do business.  As such, it falls into the default process and should be incorporated into the current or future release, depending on the priority of the item.

In the case that a release must be handled in operational scope, it should be included in a an operational milestoned labeled using the major, minor, and revision versions for the build it applies to, followed by the operations release number. The following format should be used: "Major.Minor.Revision Ops#XX"

![Operational Issue Intake Process](https://github.com/80-20/ProcessManagement/blob/master/Operational%20Issue%20Intake%20Process.png)

# Task Management
Issues flow through the following states during their lifecycle:

1. **Backlog** issues have been identified but are not yet ready for development.
2. ![Analysis Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/analysis.png) issues are actively being worked on, but may not be ready for development.
2. ![Ready Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/Ready.png) issues have been fleshed out to the point where it is believed they are ready to be acted upon by developers working on the associated milestone.
3. ![In Development Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/InDevelopment.png) issues are actively being worked on by a developer.  With the exception of items that are blocked or returned to development due to failed tests, each developer should strive to have as few items in this state as possible.
4. ![Feature Testing Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/FeatureTesting.png) issues are code complete and can be acted on by testers.  All code is assumed to be checked in and deployed to the appropriate environments for testing.
5. ![Integration Testing Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/IntegrationTesting.png) issues have been unit tested and are ready for closure pending end of sprint integration testing.
6. **Done** issues have passed testing and are closed.

All states are controlled via GitHub labels mapped to the appropriate state. By default, state transitions are managed simply by removing the current state label and applying the appropriate next state label.  Waffle.io may be used to do this automatically via drag-drop. The following label mappings are in use:

* Backlog -> No State Label, issue is Open
* Analysis -> Analysis
* Ready -> Ready
* In Development -> In Development
* Feature Testing -> Feature Testing
* Integration Testing -> Integration Testing
* Done -> Issue is Closed

### Integration Testing
Items in the integration testing state have passed all unit tests in the development environment and are considered complete pending final end of phase integration testing.  Once all development work for the sprint has been completed, items will be integration tested before being moved to Done.

### Failed Tests
When a test fails, in addition to moving the item back to **In Development**, the tester should apply the **Test Failed** label and re-assign the issue to the original developer.  This will aid in tracking priorities and help developers identify what needs their immediate attention.

![Issue Management Process](https://github.com/80-20/ProcessManagement/blob/master/Software%20Development%20Process.png)

# Release Closure
Each release has several tasks that need to be carried out to finalize the release.  These tasks are designed to facilitate testing and publication of the completed release, as well as to prepare for the next release.

The first step is to update the test and development databases with the latest data from production.  Following that, we publish the completed release to the test environment and perform integration testing.  Once all of the release items have passed integration testing, we deploy the release and update any pending operational items to indicate which ones can now be worked on.  The following graphic shows the individual steps for this process.

![Sprint Closure Process](https://github.com/80-20/ProcessManagement/blob/master/Sprint%20Closure.png)

# Tool Configuration

### GitHub Issues
Configuration of GitHub Issues requires only two steps:
- Add the **Operations** milestone
- Configure labels

The following can be used for configuring the label names and colors:
* ![Analysis](https://github.com/80-20/ProcessManagement/blob/master/Labels/analysis.png) [Analysis, #fbca04]
* ![Ready Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/Ready.png) [Ready, #fbca04]
* ![In Development Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/InDevelopment.png) [In Development, #fbca04]
* ![Feature Testing Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/FeatureTesting.png) [Feature Testing, #009800]
* ![Integration Testing Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/IntegrationTesting.png) [Integration Testing, #009800]
* ![Blocked Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/blocked.png) [Blocked, #b60205]
* ![Test Failed Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/testFailed.png) [Test Failed, #b60205]
* ![Bug Label](https://github.com/80-20/ProcessManagement/blob/master/Labels/bug.png) [Bug, #d93f0b]
* ![Trash](https://github.com/80-20/ProcessManagement/blob/master/Labels/Trash.png) [Trash, #000000]
