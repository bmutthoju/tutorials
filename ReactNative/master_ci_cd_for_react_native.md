# Master CI/CD for React Native #
## Section 1: DevOps ##
### Course Structure ###
1. Structure
2. DevOps
	1. It helps automate things (builds especially)
		1. CI/CD process
	2. Helps test in cloud automatically
	3. Automate delivery process
		1. Distributes to final users (beta-testers, stores)
3. GitHub
	1. master
		1. Little feature
		2. Bug feature
	2. Pull requests
		1. It triggers CI
			1. It triggers CD
4. AppCenter
	1. VS App Center
		1. Tool to automate
		2. Tracks bots
		3. Tracks how users behave
		4. Use DBs, auth, notfications
5. Continuous Integration
	1. Builds are triggered automatically
6. Continuous Quality
	1. The ability to automate tests in the cloud
	2. Running on devices in cloud
7. Continuous Delivery
	1. To deliver to Beta testers - automatically, through app center
	2. Delivering through the store

### What is DevOps? ###
1. DevOps - Building, testing and deplying software (automation)
	1. We need to quickly code and deliver to users - DevOps helps
		1. DevOps ensures
			1. Builds correctly
			2. Tests run successfully
			3. Bugs are caught
			4. Deploy automatically
	2. It is the automation of the development process

### Why use DevOps? ###
1. Better delivery times & more
	1. Automating builds
	2. Automating tests
	3. Automating delivery
2. Your focus
	1. Not to focus on
		1. Building your code
		2. Testing your code
		3. Deploying your code
	2. Focus on
		1. **Coding the next feature!**
			1. Once we code a feature, we must be able to deliver quickly
3. You vs Your Competition
	1. Discover issues quickly
		1. Example: with app center - how users behave
	2. Code the solution
	3. Let CI/CD do the rest
	4. Happy users!
4. Why is this important?
	1. Bugs happen
		1. We need to solve them as soon as we find them.
	2. OS updates break things
	3. Users ask for new features
	4. Users don't use your app the way you though they would
		1. App center would help identify
	5. Product team finds improvements
	6. New devices come up
		1. New aspect ratios
		2. New interfaces
	7. New interfaces are created
		1. Apple Watch
		2. AR
	8. Design languages get outdated
		1. Keep it latest
	9. New requirements from Apple/Google are added
		1. Signup up to app store is mandatory say
5. Of course, there is a business advantage
	1. Continuous innnovation
	2. Stay ahead of competition
	3. Meet new market needs
		1. Users want new features
	4. Faster time to market

### What You Will Accomplish by the end? ###
1. CI/CD trigger
	1. New feature
		1. feature branch - commit our changes
			1. `git commit -m "Update button label"
			2. `git push origin feature-6`
				1. It exists on Github
		2. Pull requests
			1. Compare & pull request
				1. Merge into dev
					1. On merge, buil will be triggered
		3. App center
			1. Android and iOS applications
				1. Build is tracked on Github
			2. Merge on build success
		4. Merge into dev has triggered another build
		5. Tests that run on real devices
		6. Distribution to beta testers
			1. Continuous delivery
		7. Distribution to store from master

## Section 2: Source Control and GitHub ##
### Source Control and Branch Structure ###
1. What is version control?
	1. It is managing changes made to documents.
		1. Also contains who made the changes
		2. Contains when were the changes made
2. Why is version control so important?
	1. To keep track of changes
	2. To have the ability to go back to a previous working version
	3. To add someone else's work (merge)
3. Where can I use git version control?
	1. Code
		1. JS, CSS, Java, ...
	2. Doc
		1. Word
		2. PDF
		3. ...
	3. (any file)
4. How do development teams use version control?
	1. Init version control in a project
	2. The changes are pushed to cloud
	3. Other computers can pull the changes
5. You should always have a working version of your project
	1. How are we supposed to add new code?
		1. `master` branch - initialized with Git repository
			1. We don't make direct commits to it
		2. `test` branch - sends commits to master (only after testing)
		3. `dev` branch - most direct commits are made
			1. The changes are pushed to `test` branch
		4. `feature-x` branches - they contain their own commits
			1. Merged to `dev` branch
			2. `bug-x` - similar
				1. Rarely merged to `test` branch - hot-fix

### Initialize Version Control ###
1. Project:

```bash
expo init CICDExample
cd CICDExample

# Git project is already initialized or else run
git init

# First clean version must be committed
git status # Shows what's happening in repo

# Untracked files exist
git add .gitignore

# File is staged

# Adding all at once
git add . # current directory

# Staged area - ready to be committed

# Commit
git commit -m "Initial commit"

# Log
git log 
```

### Committing Changes ###
1. Open the project in VS Code:
	1. `git commit -a -m "message"` (adds and commits)
	2. `git commit -am "message"` - shorter version

### Defining Branches ###
1. Branches:

```bash
git checkout -b test # checkout - to switch between branches, `-b` - branch creation
git branch -a # list of branches in current repo

# Both test and master point to the same commit
git checkout master
git branch -a
git checkout -b dev
git branch -a
```

2. VS Code:
	1. Checkout to > <branch>
3. Search: Shift + Cmd + p (command Palette)
	1. `git`

### Working with Branches ###
1. Feature branch:

```
git checkout -b feature-1 # From `dev`
```

```bash
git checkout dev
git merge feature-1
git log
git branch -d feature-1 # delete
```

```bash
git checkout test
git merge dev
```

```bash
git checkout master
git merge test
```

### Constructing a GitHub Repo ###
1. Github
	1. Repository: `ReactNativeExample`
	2. Private
	3. Create repository
	4. URL: `*.git`
	5. Issues
		1. Track issues or features we want to code.
			1. An id is set to an issue - associated with feature branch
	6. Projects
		1. To manage the issues
			1. Sort
			2. Plan project
			3. Automate workflow
			4. ...
	7. Pull requests
		1. A request to merge a branch into another
	8. Settings
		1. Webhooks
		2. Integrations & services
			1. Establish connection between Github and appcenter
		3. Collaborators
			1. Enable access to the repository for a github account
		4. Branches
			1. Protection rules
				1. To check if code works
					1. The application must build
					2. The tests have to pass

### Pushing to GitHub ###
1. Set remote repo:

```bash
git remote add origin https://github.com/bmutthoju/ReactNativeExample.git # origin can be any name
git remote -v
# fetch - downloading, push - uploading

git push -u origin master # -u - upstream. The local master branch is going to use the remote master branch as upstream. `git push` is sufficient for subsequent pushes.
```

```bash
git branch -M main # rename current branch to `main` forcefully
git push -u origin main # push to remote `main` and track `main` as remote branch from `origin`
```

```bash
git checkout test
git push -u origin test

git checkout dev
git push -u origin dev
```

### Working in Teams ###
1. Collaborators:
	1. Branchs: Branch protection rule
		1. Branch name pattern: master (pattern can be used like: `feature-`)
		2. Rules settings:
			1. Require pull request reviews before merging
				1. Requires approving reviews: 1
			2. Require status checks to pass before merging (later)
			3. Include administrators (later)
				1. Restrictions should include admins (otherwise admins can merge)
		3. Create
	2. Collaborators
		1. lalorosas
			1. Add collaborator
				1. Will get invitation

### Making Pull Requests ###
1. New issue
	1. Title: Wrong text
	2. Assignee: benesyslabs
	3. Submit new issue
		1. Issue id: #1
2. New feature branch
	1. dev
		1. Dropdown: feature-1
			1. greeting.js
				1. Edit
					1. `placeholder="Enter your name..."`
					2. `Welcome to this CI/CD for React Native course, {this.state.name}!`
			2. Commit:
				1. `Update text to solve #1` (references issue)
					1. They also apply to PRs
					2. Issues: References the commit
		2. Pull requests
			1. Compare & pull request (dev <- feature-1)
			2. PR is assigned an ID (#2) (#1 is used by issue)
			3. Merge pull request
			4. Delete feature branch
		3. Issue: Close the issue
	2. test
		1. PR to merge dev
		2. Merge PR
		3. Don't delete the `dev` branch
	3. main
		1. PR to merge test
		2. Merge is blocked
			1. Approval is required
				1. Admin can merge
				2. Review changes
				3. Approve
				4. Submit review

### A Simulated CI/CD Rundown ###
1. CD process
	1. Settings
		1. GitHub Pages - a site about Github repo
			1. master branch
				1. URL for site
				2. Source: master branch
	2. Code
		1. `dev` branch
			1. Add a README
			
			```
			# ReactNativeExample
			
			CI/CD React Native Example
			
			## By Eduardo Rosas and the Learn Programming Academy
			```
			
		2. Commit
			1. `feature-2` (Create branch and open PR)
			2. Merge
			3. Delete `feature-2`
		3. Merge dev to test
		4. PR from test to master
			1. Approve and submit review
			2. Merge PR
				1. Github page has the README

## Section 3: Intro to App Center ##
### Intro to App Center ###
1. What is App Center?
	1. An intro to Microsoft's mobile-centered DevOps service
		1. AppCenter - Mobile-centered
			1. Automate integration of new version of code - triggered when merge happens
			2. Execute tests added to the project
			3. Automates delivery of the new version (directly or to stores)
			4. Track bugs
			5. App usage tracking
				1. To track user issues
			6. DBs
			7. User auth
			8. Push notifications
	2. Track errors
		1. From a single place we can identify errors of millions of users
	3. Track events (are users behave the way we think they might do?)
		1. Are users using the new feature?
		2. Are they finding the page?
		3. Are they signing up?
		4. ...

### Instantiating an App Center Account ###
1. https://appcenter.ms
2. Pricing
	1. Free - 240 build minutes per month
	2. Test: Free 30 day trial
	3. Distribute: Unlimited distributions and users
3. Login
	1. Add new organization
		1. New applications
		2. Name: App Center Course
3. Organization
	1. People 
		1. Add teammates
		2. Add teams
		3. Add Distribution groups
			1. Group that recieves updates for a set of applications
	2. Manage
		1. Azure - connect
		2. Integrations
	3. Apps
		1. New app: `InflationCalc`
			1. Release Type: later
			2. OS: iOS
			3. Platform: React Native
		2. New app: `InflationCalc - Droid`
			1. Release Type: later
			2. OS: Android
			3. Platform: React Native

### Connecting App Center ###
### Source Code and GitHub Repo ###
### Crashing the Application ###
### Uploading iOS Symbols to App Center ###
### Check if the App Crashed in previous session ###
### Tracking All Kinds of Events ###
### Tracking Events with Better Context ###

## Section 4: Continous Integration ##
### Why Use Continuous Integration? ###
### Working with Feature Branches ###
### A First CI Build ###
### Adding Checks to Pull Requests ###
### Cleaning Up the Connections ###
### Using Checks to Protect Branches ###
### A Complete CI Flow ###

## Section 5: Continuous Quality ##
### Intro to Continuous Quality ###
### Prepare Android Project for Tests ###
### Prepare iOS Project for Tests ###
### Installing the App Center CLI ###
### Uploading the Android Tests ###
### Uploading the iOS Tests ###
### Running Automated Tests - iOS ###
### Running Automated Tests - Android ###

## Section 6: Continuous Delivery ##
### Intro to Continuous Delivery ###
### Constructing an iOS Distribution Group ###
### Configuring Android Continuous Delivery ###
### Configuring iOS Continuous Delivery ###
### Installing from App Center - Android ###
### Installing from App Center - iOS ###
### Connecting the Play Store to App Center ###
### Connecting the iOS App Store to App Center ###
### Continuous Delivery to the App Store ###
### Continuous Integration / Continuous Delivery ###

## Section 7: Extra Information - Source code, and other stuff ##
### Source Codes ###
### Bonus Lecture and Information ###