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

###Further details and complete guide
Read more about the [Gitflow Workflow](https://www.atlassian.com/git/workflows?_escaped_fragment_=workflow-gitflow#!workflow-gitflow)

