# CI/CD #
1. Acronyms:
	1. CI - Continous Integration
	2. CD - Continous Delivery
2. CI/CD automates software development process from the initial commit all the way through to deployment.
	1. Takes care of
		1. Building
		2. Testing
		3. Deploying
3. Promise
	1. Enables software teams to deploy better-quality software faster
4. Does it work in real-life?
	1. CI:
		1. Less controvertial and more common
		2. Enables automation for teams to merge code changes to a shared repository early and often
		3. Each commit triggers an automated workflow on a CI server that triggers a series of tasks to make sure the commit is safe to merge into the main branch
		4. A good CI process relies on a good set of tests
			1. It is non-trivial to maintain sufficient tests with good coverage and that are non-flaky
			2. High test coverage takes longer to run which decreases a developer's productivity
				1. Tough balancing act
					1. Worth the effort to get it right
		5. Build Tools
			1. Github - popular
				1. Has everything to build a software
				2. Github actions
				3. Buildkite
			2. GitLab
			3. Jenkins
			4. TravisCI
			5. CircleCI
			6. Tools:
				1. Gradle
				2. Bazel
				3. Webpack
					1. Other tools are faster but not as extensible
		6. Test tools
			1. They are language and ecosystem specific
				1. Example:
					1. JS: Jest (Unit Tests)
					2. Payright: (Integration tests)
					3. Cypress: (Integration tests)
	2. CD:
		1. Continuous Deployment
			1. Hard
				1. Not as common
		2. CD is usually practiced on most basic systems
			1. APIs or Web Server tiers
		3. CD can be achieved with good monitoring
			1. Datadog
				1. Rollback can be implemented
		4. CD can also be backed by feature flags
			1. Separates deployment of code from the activation of new features
				1. Allows teams to quickly shut off features that cause issues (full rollback is avoided)
		5. Canary deployments
			1. Good strategy for 100s of millions of users
			2. Deployment of production code to a tiny subset of power users and staff
				1. They appreciate new features as well as help catch problems before the new code is deployed widely
				2. Allows team to test new code in a real world environment
					1. Limits blast radius if something goes wrong
			3. Works well for simple stateless systems
		6. Very few teams have the resources or convictions to implement real continous hands-off deployment for stateful systems
		7. Stateful systems
			1. The systems are on a fixed deploy cadence
			2. Deployment process is manual, risky and time-consuming
				1. They require the care of a dedicated platform team
			3. These systems can rarely be deployed continuously and automatically
		8. Tools
			1. Github actions
			2. Buildkite
			3. Jenkins
			4. Argo CD (infra specific)
				1. Kubernetes
5. CI/CD is not a one-size fits all solution
	1. Implementation may vary depending on the complexity of the system