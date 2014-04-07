Project Workflow and Conventions
=================

This is a live document describing our Git Workflow and code guidelines regarding web development.


##Git Workflow and branching

![Git Workflow](https://raw.githubusercontent.com/KnowitLabs/Project-Workflow-and-Conventions/master/img/git-workflow-release-cycle-4maintenance.png "Git Workflow")

###Master

###Release

###Develop

###Feature

###Hotfix
Hotfix branches are used to quickly patch production releases. This is the only branch that should fork directly off of master. As soon as the fix is complete, it should be merged into both master and develop (or the current release branch), and master should be tagged with an updated version number.

####Common conventions:
- **Naming convention:** hotfix-* or hotfix/*
- **branch off:** master
- **merge into:** master/develop/release
