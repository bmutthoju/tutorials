## Single Sign-on (SSO) ##
1. It is authentication scheme
2. Enables users to access multiple applications securely using single id
	1. Example: gmail, workday. slack, ...
		1. Login only once
3. SSO is built on federated identity
	1. Sharing of identity information across trusted but independent systems
	2. Two common protocols
		1. SAML
			1. Security Assertion Markup Language: XML based open standard for exchanging identity information between services
			2. Commonly found in work environment
		2. OpenID
			1. Example: Signing into google to open YouTube
			2. Uses JWT (JSON Web Token) to share identity information between services
4. SSO Login Flow:
	1. Using SAML
		1. Office worker visits Gmail (SSO Login page)
			1. Gmail in this case is Service Provider
		2. Gmail recognizes that user is from a work domain and returns a SAML Authentication Request (SAR) back to browser
		3. Browser redirects user to Identity Provider for company specified in SAR (Forward SAR)
			1. Examples of commercial identity providers:
				1. okta
				2. Auth0
				3. onelogin
		4. Identity provider shows login page where user enters login credentials
		5. Once user is authenticated, Identity Provider generates a SAML response and returns it to the browser (SAML assertion)
			1. SAML assertion:
				1. It is a cryptographically signed XML document that contains information about the user and what user can access with the service provider
		5. Browser forwards signed SAML assertion to Service Provider (Gmail)
		6. Service Provider does validation of signed SAML assertion
			1. Usually done with public key cryptography
		7. Service provider returns the protected resource to the browser based on what the user the allowed to access as specified in the SAML assertion
5. SSO navigates to another integrator application
	1. Service Provider (Workday say) detects the work domain and sends a SAML authentication request back to the browser
	2. Browser redirects (forwards SAR) to Identity Provider
	3. Since user is already logged in, Identity Provider skips the login process and isntead generates a signed SAML assertion for the Service Provider (specifying what the user can access there)
	4. SAML assertion is sent to browser which is in-turn forwarded to the Service Provider (workday)
	5. Service Provider validates signed SAML assertion and grants access accordingly
6. OpenID:
	1. The protocol is similar to SAML but instead of passing signed XMLs around, it passes JWT (signed JSON document)
		1. Implementation details are a little different
7. Which on to use?
	1. Both are secure
	2. Enterprise: Commercial Identity Providers support both
		1. Examples:
			1. Duo
			2. PingID
			3. Thales
			4. jumpcloud
			5. cyberark
			6. Microsoft
			7. okta
			8. onelogin
			9. RSA
			10. secureauth
	3. Decision is on the application and depends on which protocol is easier to integrate with
	4. For new applications:
		1. OpenID connect platforms can be used (Google, Facebook, Twitter, Github, ...)