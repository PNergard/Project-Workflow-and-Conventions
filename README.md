Project Workflow and Conventions
=================

This is a live document describing our Git Workflow and code guidelines regarding web development.


##Git Workflow and branching

![Git Workflow](https://raw.githubusercontent.com/KnowitLabs/Project-Workflow-and-Conventions/master/img/git-workflow-release-cycle-4maintenance.png "Git Workflow")

This workflow uses two branches to record the history of the project. The master branch stores the official release history, and the develop branch serves as an integration branch for features. It's also convenient to tag all commits in the master branch with a version number.

###Master
This is the main repository used for deploying releases. No development is done here but rather branched to **develop** or **hotfix** to later be merged back into the master branch when ready for a release. The master holds all release tags, and tags are made using [Semantic Versioning 2.0.0](http://semver.org).

####Common conventions:
- **Naming convention:** Refer to [Semantic Versioning 2.0.0](http://semver.org)

###Hotfix
Hotfix branches are used to quickly patch production releases. This is the only branch that should fork directly off of master. As soon as the fix is complete, it should be merged into both master and develop (or the current release branch), and master should be tagged with an updated version number.

####Common conventions:
- **Naming convention:** hotfix-* or hotfix/*
- **branch off:** master
- **merge into:** master/develop/release

###Release
Once develop has acquired enough features for a release (or a predetermined release date is approaching), you fork a release branch off of develop. Creating this branch starts the next release cycle, so no new features can be added after this point—only bug fixes, documentation generation, and other release-oriented tasks should go in this branch. Once it's ready to ship, the release gets merged into master and tagged with a version number. In addition, it should be merged back into develop, which may have progressed since the release was initiated.

Using a dedicated branch to prepare releases makes it possible for one team to polish the current release while another team continues working on features for the next release. It also creates well-defined phases of development (e.g., it's easy to say, “this week we're preparing for version 4.0” and to actually see it in the structure of the repository).

####Common conventions:
- **branch off:** develop
- **merge into:** master
- **naming convention:** release-* or release/*

###Develop
This is the main branch where the source code of HEAD always reflects a state with the latest delivered development changes for the next release. This is where any automatic nightly builds are built from. Larger tasks, issues and/or fatures are branched into a feature branch only to be marged back into the develop branch in the future.


###Feature
Feature branches (or sometimes called topic branches) are used to develop new features for the upcoming or a distant future release. When starting development of a feature, the target release in which this feature will be incorporated may well be unknown at that point. The essence of a feature branch is that it exists as long as the feature is in development, but will eventually be merged back into develop (to definitely add the new feature to the upcoming release) or discarded (in case of a disappointing experiment).

####Common conventions:
- **branch off:** develop
- **merge into:** develop
- **naming convention:** anything except master, develop, release-*, or hotfix-*

###JIRA Integration
All Git repositories are connected to a project in JIRA and you can add comments and log time from the commit message in git to a project issue.

#####comment Directive
ISSUE_KEY #comment <comment_string>

Records a comment against an issue.  For example:
```
JRA-34 #comment corrected indent issue
```
Adds the comment "corrected indent issue" to the issue.

#####time Command
ISSUE_KEY #time <value>w <value>d <value>h <value>m  <comment_string> 
```
JRA-34 #time 1w 2d 4h 30m Total work logged
```
This example records 1 week, 2 days, 4hours and 30 minutes against an issue, and adds the comment 'Total work logged' in the Work 

All commits must be associated with an Issue in JIRA. If no issue exists you should create one. For example, you might need to refactor some code. Instead of logging your time to the last issue you were working on, create a new issue called "refactoring code" and commit that code with a comment to that very issue. That will keep ourselves informed on what's happening and why someone just "wasted" 8 hours work on some seamingly meaningless task that didn't produce any neat features.


###Further details and complete guide
- [Gitflow Workflow](https://www.atlassian.com/git/workflows?_escaped_fragment_=workflow-gitflow#!workflow-gitflow)
- [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)

##Front-End Code Conventions

###HTML Templates
###Less and CSS
###Java Scripts


##Back-End Code Conventions

##The laws of code
1. The developer must not commit faulty code to any other branch than his/her own feature branch. 
2. The developer must at all times commit to follow the naming and code conventions.
3. The developer must not go on vacation to far away countries without first doing a commit and push.
4. The developer must associate all commits with an Issue in JIRA

Any failure to comply to the laws of code is forced to buy fika for the entire team
