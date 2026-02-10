# React Native: Advanced Concepts #
## Facebook Authentication ##
### Facebook Auth Flow ###
1. Facebook authentication using Expo
2. Flow:
	1. User starts app
	2. Have they logged in before? (how to do this?)
		1. Yes
			1. Send them to map screen
		2. No
			1. Send them to welcome
3. How to:
	1. Call Expo.loginWithReadPermissionsAsync
		1. Expo makes it simple
		2. Function
		3. Facebook popup is displayed
	2. Facebook popup displayed to user
	3. User enters details
	4. Our app gets a token if auth was successful
		1. If token exists, send the user to map screen
	5. That's it!
3. Expo documentation:
	1. Facebook - [https://docs.expo.dev/guides/facebook-authentication/](https://docs.expo.dev/guides/facebook-authentication/)

### The Facebook Dev Console ###
### Redux Setup ###
### Using Async Storage ###
### Crazy Async/Await Syntax ###
### Logging in With Facebook ###
### Testing Facebook's Login Flow ###
### Quick Note ###
### World's Biggest Gotcha ###
### The Auth Reducer ###
### Skipping the Auth Screen ###
### Testing Auth Flow ###
### Advancing the Welcome Screen ###
### Resolving the Loading Screen ###

## MapViews on React Native ##
### Showing a Map ###
### Interacting with the MapView ###
### Working around MapView Issues ###
### Indeed API Key ###
### The Indeed Jobs API ###
### Location API Mismatch ###
### Converting LatLong to Zip Code ###
### Fetching a List of Jobs ###
### Issuing Action Creators from MapScreen ###
### The Jobs Reducer ###
### Navigating from Action Creators ###
### The Deck Screen ###
### Importing the Deck Component ###
### Applying the Swipe Component ###
### Styling Job Cards ###
### Customizing MapViews ###
### Android Compatibility ###
### Dynamic Key Props ###
### One More Swipe Deck Fix ###
### Liking a Job ###
### Considering Only Unique Jobs ###
### The Review Screen ###
### Rendering a List of Liked Jobs ###
### Applying to Jobs ###
### Mapping a Jobs Location ###
### Styling the Job Card ###
### Crearing Liked Jobs ###
### Redirecting Back to the Map ###
### Callback Gotcha ###
### Tab Bar Icons ###
### Tab Bar Config ###
### Android Specific Fixes ###

## Offline Data Persistence ##
### Push Notifications and Data Persistence ###
### Persisting Application State ###
### Wiring Up Redux Persist ###
### How Redux Persist Works ###
### Redux Persist - Huge Gotcha! ###

## Push Notifications ##
### Push Notification Overview ###
### Registering For Push Notifications ###
### Generating Push Tokens ###
### Testing Notifications ###
### More on Notifications and Wrapup ###