Project Workflow and Conventions
=================

This is a live document describing our Git Workflow and code guidelines regarding web development.


##Git Workflow and branching

![Git Workflow](https://raw.githubusercontent.com/KnowitLabs/Project-Workflow-and-Conventions/master/img/branching.png "Git Branching Workflow")

This workflow uses two branches to record the history of the project. The master branch stores the official release history, and the develop branch serves as an integration branch for features. It's also convenient to tag all commits in the master branch with a version number.

#Front-end branching and project branching
The front-end code operates on two main branches, `fe-master` and `fe-develop`. The project branch retreives the front-end code from the `fe-master` branch. The `fe-master` operates according to the same rules as the `master` branch with the only exception that it only handles front-end code.

###master
This is the main repository used for deploying releases. No development is done here but rather branched to **develop** or **hotfix** to later be merged back into the master branch when ready for a release. The master holds all release tags, and tags are made using [Semantic Versioning 2.0.0](http://semver.org).

####Common conventions:
- **Naming convention:** Refer to [Semantic Versioning 2.0.0](http://semver.org)

###hotfix
Hotfix branches are used to quickly patch production releases. This is the only branch that should fork directly off of master. As soon as the fix is complete, it should be merged into both master and develop (or the current release branch), and master should be tagged with an updated version number.

####Common conventions:
- **Naming convention:** hotfix-* or hotfix/*
- **branch off:** master
- **merge into:** master/develop/release

###release
Once develop has acquired enough features for a release (or a predetermined release date is approaching), you fork a release branch off of develop. Creating this branch starts the next release cycle, so no new features can be added after this point—only bug fixes, documentation generation, and other release-oriented tasks should go in this branch. Once it's ready to ship, the release gets merged into master and tagged with a version number. In addition, it should be merged back into develop, which may have progressed since the release was initiated.

Using a dedicated branch to prepare releases makes it possible for one team to polish the current release while another team continues working on features for the next release. It also creates well-defined phases of development (e.g., it's easy to say, “this week we're preparing for version 4.0” and to actually see it in the structure of the repository).

####Common conventions:
- **branch off:** develop
- **merge into:** master
- **naming convention:** release-* or release/*

###develop
This is the main branch where the source code of HEAD always reflects a state with the latest delivered development changes for the next release. This is where any automatic nightly builds are built from. Larger tasks, issues and/or fatures are branched into a feature branch only to be marged back into the develop branch in the future.

###feature
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
####General thumb rules
* HTML templates contains either one block or page.
* The filename for a template are page-[pagename].html or block-[blockname].html

####Block Templates
Wrap your block with a div and name it with a class
```html
<div class="block-myblock">...</div>
```

Avoid further classes unless neccessary
```html
<div class="block-myblock">
	<h3>Lorem ipsum</h3>
	<p>lorem ipsum dolor sit amet</p>
</div>
```

####Page Templates
Wrap your page template with a div and name it with a class.
```html
<div class="page-mypage">...</div>
```

###Less and CSS
####General thumb rules
* Create one less file per block and/or page template
* Create one less file per global function such as side-navigation, pagination or footer
* Use classes, always. Never use ID's unless hell has frozen over.
* If not sure wether to create a new less file or add to an existing, create a new one.

####Templates
Wrap your styling with the page- or block-template class name
```css
page-newsarchive {
	h2 {
		font-size:30px;
	}
	...
}
```

###Java Scripts
* Create one script file per object
* Keep variables in data-properties in the HTML mockup or read them from a JSON-file. Never keep variables or paths in the JavaScript files.
* Keep your functions dynamic. Do not rely on static information, keep in mind that information can and will change.
* Keep common functions in the main.js
* If you create something amazing that other projects may benefit from, consult your co-workers, we might want to extract it into a dependency
* Do not reinvent the wheel

##Back-End Code Conventions
###General
* AutoEventWireup shall always be set to false in all .masterpage, .ascx and .aspx files
* We have a 'Business' folder in the main web project as well as a separate Business project. Any function, extention, webcontrol etc that can be reused by other projects should be placed in the separate project. Project specifc in the main web project.
* Don't just copy/paste code that are not included in the solution. Take the time to clean up the code if you see anything that needs to be done. Could be removing obsolete code, removing old comments, renaming variables, renaming class names, adding new comments etc.
* Files that are not needed should not just be exluded from the projecte. Delete, commit and push to keep the Git-repo nice and clean.

###Languages
* Always think multi-language site. Which properties need to be [CultureSpecific]?!
* If you add properties to templates or blocks always add a correct caption and if needed helptext via the admin-plugin XML Language manager.
* All other things that are possible to translate via the XML Language manger should be translated.
* Never hardcode texts in .aspx or .asxc files. Add a property for the editor to be able to add a text or add translation to views_sv file. Add a descriptive first element and all translations for the template / block below that (don't add more sub elements since the tool doesn't support it).
* Knowit.Business have different webcontrols for creating labels for properties. (Uses the property caption.

##The laws of code
1. The developer must not commit faulty code to any other branch than his/her own feature branch. 
2. The developer must at all times commit to follow the naming and code conventions.
3. The developer must not go on vacation to far away countries without first doing a commit and push.
4. The developer must associate all commits with an Issue in JIRA

Any failure to comply to the laws of code is forced to buy fika for the entire team
