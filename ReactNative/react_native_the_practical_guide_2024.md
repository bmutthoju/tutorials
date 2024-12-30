# React Native - The Practice Guide [2024] #
## Section 1: Getting Started ##
### Welcome to this Course & What to Expect! ###
1. React Native from scratch
2. Core features
3. Prerequisite - React
4. Theory + practical examples (to understand the theory)

### What is React Native? ###
1. What is React Native?
	1. Related to React.JS
	2. React.JS + React Native -> Real Native Mobile Apps (iOS, Android)
		1. React.JS
			1. A javascript library for building user interfaces
			2. Typically used for web development
			3. But it's actually react-dom that adds web support
			4. React itself is platform-agnostic
				1. It doesn't care about the underlying platform
					1. Supports state management
					2. Supports virtual component trees
					3. ...
				2. React-DOM translates result produced by React to an platform (like browser)
		2. React Native - Alternative to React DOM
			1. A collection of "special" React components (in JSX code)
				1. Built-in components
			2. Components are compiled to native UI elements
				1. For iOS and Android
				2. React Native takes care of the compilation step
			3. Native platform APIs exposed to JavaScript (RN takes care of it)
				1. Enables us to use the features in the JS (camera, ...)
			4. React Native is like React-DOM: It "connects" React to a specific platform (iOS, and Android)
			5. Gives components and APIs to interact with the platforms and build apps for the platforms
			6. Pre-requisite - React.JS

### Join our Online Learning Community ###
1. [https://academind.com/community/](https://academind.com/community/)
	1. perfect complimentary resource for this course.

### A Glance Under the Hood of React Native ###
1. A Look Under the Hood
	1. React + React Native App
	
	```javascript
	const App = props => {
		return (
			<View>
				<Text>Hello There!</Text>
			</View>
		);
	};
	```

2. Real Native App is produced
3. `View`s are compiled by React Native - just the JSX code/components & not JS logic itself
4. Components are Compiled
	1. Web Browser (react-dom)
		1. `<div>`
		2. `<input>`
	2. Native Component (Android)
		1. `android.View`
		2. `EditText`
	3. Native Component (iOS)
		1. `UIView`
		2. `UITextField`
	4. React Native JSX
		1. `<View>` (targets `android.View` and `UIView` (compiled to the respectively))
		2. `<TextInput>` (targets `EditText` and `UITextField`)
5. React Native maps (and compiles) re-usable components (`<View>`, `<TextInput>`, ...) to respective platform equivalents
6. What about the logic?
	1. JS code (functions, if statement, state management, ...)
	2. UI Elements -> Components exposed by React Native -> Compiled to native views
	3. Written by us, in JS -runs in-> JS thread, hosted by React Native (in the native app built) (it is not compiled)
		1. RN spins up a JS process as part of the native app we built and manages the process for us
			1. It allows the process to talk to the underlying native platform
			2. JS talks to underlying android or ios platform through translation bridge (provided by RN)

### Constructing React Native Projects: Expo CLI vs React Native CLI ###
1. [reactnative.dev](reactnative.dev)
	1. Get Started
		1. Two approaches
			1. Expo Go Quickstart (recommended)
				1. Simplifies managing RN apps easier
			2. React Native CLI Quickstart
		2. Differences between approaches (CLIs help us construct RN projects, and run RN apps on testing devices and simulators, and build RN apps to ship to the app-store). One of the following is enough
			1. Expo CLI (Expo)
				1. Third-party service (free!)
					1. No sign-up & no payment (but has extra-paid services)
				2. CLI + other free tools give
					1. Managed app development workflow
						1. Starting projects is easy
						2. Writing code is easier
						3. Tapping into native device functionality (using camera, say) is easier
						4. Very convenient, less friction
						5. You can leave the Expo ecosystem any time ("eject") (and switch to React Native CLI)
			2. React Native CLI
				1. By the React Native team & community
				2. Bare-bone development (you need to set up way more)
					1. More config and setup work
				3. Less convenience features
					1. For native device features, there is more work
				4. Easier integration with native source code (Java, Objective C, Swift, Kotlin)
					1. To mix with native source code is easier
						1. Not required too often

### Constructing React Native Projects ###
1. Install Node.JS LTS
2. Creation:

		```bash
		npx create-expo-app@latest --template blank RNCourse
		```

	1. No TS
	2. More barebones
	3. `RNCourse` - project name and folder
3. [https://expo.dev/](https://expo.dev/)
4. Open in editor (VS Code)

### Constructing a New React Native Project ###
### Analyzing the Created Project ###
1. Folders
	1. assets
		1. Images
		2. Icons
	2. package.json
		1. Dependencies
			1. expo - JS package
				1. It gives many util functions that makes code easier
			2. react
			3. react-native
	3. app.json
		1. Used to configure settings and behavior of RN app
			1. Picked up by expo for preview or for actual app store
		2. Properties
			1. Name
			2. BG colors
			3. ...
	4. App.js
		1. Special JSX components
		2. Styling

### Running Our First App on a Real Device! ###
1. Previewing app on Real device with expo is easy
	1. App store
		1. Expo Go
			1. Open
2. Terminal
	1. `npm start` - starts expo development server (it builds and watches our code)
		1. Allows preview
		2. Scan with Android
		3. Browser
			1. QR Code
		4. Scan QR Code with iOS
			1. Open in expo
	2. Changes are instantly updated on device
3. Install simulator
	1. Android studio - download and install
		1. To run Android emulators
			1. More Actions
				1. Virtual Device Manager
					1. Create device
						1. Select preset
						2. Android version (API 32)
						3. Finish
					2. Play
	2. iOS XCode - not available on Windows or Linux
		1. Alternative cloud build service
			1. Preferences
				1. Locations
					1. Command Line Tools: Xcode version
	3. Expo app
		1. Keep it running
			1. `a` - open on Android
				1. Starts a simulator and runs the app
					1. Expo needs playstore so use the emulator that has a play-store (because Expo Go is downloaded)
			2. `i` - open on iOS
				1. XCode
					1. Show package contents
						1. Contents > Developer > Applications
							1. Simulator.app (double click)
								1. File > Open Simulator > Choose a device
			3. `r` - reloads manually

### Setting up a Local Development Environment ###
1. [https://www.jetbrains.com/ides/#choose-your-ide](https://www.jetbrains.com/ides/#choose-your-ide)
	1. Webstorm - Web development
	2. To get Jetbrains IDE for 6 months for free:
		1. `ACADEMIND_JETBRAINS`
			1. [https://sales.jetbrains.com/hc/en-gb/articles/206544449-I-received-a-coupon-code-for-a-JetBrains-license-how-can-I-use-it](https://sales.jetbrains.com/hc/en-gb/articles/206544449-I-received-a-coupon-code-for-a-JetBrains-license-how-can-I-use-it)
			
### About this Course ###
1. Course Content
	1. Getting Started
	2. Essentials
		1. Basics & Fundaments
			1. Building UIs with RN components
			2. Styling UIs
			3. Building powerful layouts
		2. Dynamic and Adaptive Layouts
		3. Navigation
			1. Switching between screens with nice animations
			2. Drawers, tabs, ...
	3. Prerequisites: JS, and React
		1. JavaScript & React.js Refreshers (don't replace real JS and React courses) - optional
	4. React & React Native (connecting key concepts with RN)
		1. Redux & React Native
			1. Or Context API
		2. Complete Example App
		3. Handling User Input
		4. Http Requests
	5. Advanced
		1. User Authentication
		2. Native Device Features
			1. Storage
			2. Camera
			3. Locations - locating user/showing map
		3. Push Notifications
		4. Publishing Apps
		
#### How to Get the Most Out of the Course ####
1. Watch videos
2. At your own pace
3. Speed up, slow down, pause & rewind!
4. Code along
5. Pause & practice
6. Experiement & build your own demo apps
	1. Add extra features
		1. To get even more out of the course
7. Use the course resources & attachments
8. See next lecture!
	1. All code resources
	2. Use the attached code to compare & replace
9. Help each other in the Q&A section
10. Ask & reply to others
11. By replying to others, you'll learn way more!
	1. Helps us get challenged, and articulate the solution

### Course Resources, Code Snapshots & How to Use ###
1. [Course resources + Instructions](https://github.com/academind/react-native-practical-guide-code)
	1. Resources
		1. Code snapshots (to compare against our code, when coding along)
		2. Slides
		3. Extra resources (images used in a section)

## Section 2: React Native Basics [COURSE GOALS APP] ##
### Module Introduction ###
1. Topics:
	1. Diving into the core concepts
		1. using React Native Components & building UIs
		2. Styling React Native Apps
		3. Adding interactivity & Managing state
			1. Buttons that can be clicked & what happens on click

### Exploring Core Components & Component Styling ###
1. React component: functional component
	1. `Text`, `View` - built in components
		1. Native devices don't have DOM
			1. With a few components, we can build any kind of interface
2. Working With Core Components
	1. "Core" Components
		1. (Built into React Native)
		2. Core components are translated into native UI widgets (provided by RN)
			1. `<View />`
			2. `<Text />`
			3. `<Button />`
			4. `<TextInput />`
			5. `<Image />`
			6. ...
	2. Your UI & Custom Components
		1. Combining of "Core" components & other buit-in components [to build our own components and UI]
		
		```javascript
		const MyTitle = props => {
		  return (
		    <View>
			  <Text>{props.title}</Text>
			</View>
		  );
		}
		```
		
		2. There are many HTML elements comparatively.
3. Styling React Native Apps
	1. There is no CSS
		1. Solution:
			1. Inline - using props on core components
			2. StyleSheet Objects
		2. Written in JavaScript
			1. (i.e. in the JS code files, next to the component code)
			2. It is based on CSS syntax, but only a **subset** of properties & features is supported!
4. Code: App.js

```javascript
import { StatusBar } from "expo-status-bar";
import { StyleSheet, Text, View } from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  /* style prop */
  return (
    <View style={styles.container}>
      <Text>Alhamdulillah!</Text>
      <StatusBar style="auto" />
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

### Working with Core Components ###
1. `<View>random text</View>` - not allowed
	1. It is only used to build boxes and contents
		1. `<Text>` must be used
	2. It is only used to hold other components
	3. It is not like `<div>`
	4. It holds and lays out other components
	5. `View`s can be nested
	6. Styling can be used on `<View>` to control where child elements must be placed
2. Other RN core components
	1. `Image`
	2. `ScrollView`
	3. `TextInput` - to enter text
	4. `Button`
3. With RN, we need to import core elements
	1. Unlike in React for web where we don't have to import HTML elements
	2. Example:
	
	```
	<Button title="Tap me!" />
	```
	
	3. Every component has clearly defined purpose

### Styling React Native Apps ###
1. There is no CSS
	1. No CSS files or CSS language
2. Methods:
	1. Inline Styles - passing style object through props
	2. SteleSheet Objects - passing through props
3. Written in JS language (in JS code files, next to the component code)
4. Based on CSS syntax, but only a **subset** of properties & features is supported!
	1. And not all names are the same
5. `style` prop is supported by some elements
	1. `View`
	2. `Text`
6. `margin` - requires a value as a number - translated to px (adjusted to device's pixel density)
7. `padding` - requires a number
8. `borderWidth` - requires a number
	1. `border` is not supported as in the Web
9. Inline styling is not the best option. We need to go for `StyleSheet` objects
	1. Separates JSX code and styles
	2. Makes styles re-usable
10. Why `StyleSheet` object?
	1. We get style auto-completion
	2. Provides validation
		1. If we use invalid style properties or values, we get an error/warning
11. Code: App.js

```javascript
import { Button, StyleSheet, Text, View } from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  /* style prop */
  return (
    <View style={styles.container}>
      <Text style={styles.dummyText}>Alhamdulillah!</Text>
      <Text style={styles.dummyText}>Another Piece of Text</Text>
      <Button title="Tap me!" />
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
  dummyText: {
    margin: 16,
    padding: 16,
    borderWidth: 2,
    borderColor: "red",
  },
});
```

### React Native: Core Components, Styling & Colors - More Information ###
1. [Official styling documentation](https://reactnative.dev/docs/style)
2. [Official article about colors](https://reactnative.dev/docs/colors)
	1. Different ways of setting & using colors in RN apps
3. [Official API reference articles for the different core components](https://reactnative.dev/docs/view)
	1. All props we can set on `<View>` component
4. [Style properties for the component](https://reactnative.dev/docs/view#style)
	1. [https://reactnative.dev/docs/view-style-props](https://reactnative.dev/docs/view-style-props)
	2. `View` maps directly to the native view equivalent on whatever platform React Native is running on, whether that is a `UIView`, `<div>`, `android.view`, etc.

### Exploring Layouts & Flexbox ###
1. New styling features
	1. Flexbox
2. Code: App.js

```javascript
import { Button, StyleSheet, Text, TextInput, View } from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  /* style prop */
  // First `View` - Users add text for the goal and click a button for the goal
  // Second `View` - List of goals rendered
  return (
    <View style={styles.appContainer}>
      <View>
        <TextInput placeholder="Your course goal!" />
        <Button title="Add Goal" />
      </View>
      <View>
        <Text>List of goals...</Text>
      </View>
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    padding: 50,
  },
});
```

### React Native & Flexbox ###
1. Layouts & Flexbox
	1. Layouts are (typically) constructed with Flexbox
		1. Very similar to browser CSS flexbox!
		2. Elements are positioned inside of containers
		3. Positioning is controlled via style settings applied to the element container
	2. Two axes
		1. Main Axis
		2. Cross Axis
	3. Properties
		1. `flex: 1` - The element (container) should expand to occupy available space (in relation to other containers)
		2. `flexDirection: 'column'` - Controls the orientation of 'Main Axis' and 'Cross Axis'
			1. `Column` - Main axis from top to bottom
		3. `justifyContent` - controls how the elements are layed out in their axis
		4. `alignItems` - controls how the elements are layed out in their axis
	4. Note: Flexbox is enabled by default on the views
2. Code: App.js

```javascript
import { Button, StyleSheet, Text, TextInput, View } from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  /* style prop */
  // First `View` - Users add text for the goal and click a button for the goal
  // Second `View` - List of goals rendered
  return (
    <View style={styles.appContainer}>
      <View style={styles.inputContainer}>
        <TextInput style={styles.textInput} placeholder="Your course goal!" />
        <Button title="Add Goal" />
      </View>
      <View>
        <Text>List of goals...</Text>
      </View>
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    padding: 50,
  },
  inputContainer: {
    flexDirection: "row",
    justifyContent: "space-between",
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#cccccc",
    width: "80%",
    marginRight: 8,
    padding: 8,
  },
});
```

### Using Flexbox to Construct Layouts ###
### Flexbox - A Deep Dive ###
1. Example: flex = 1, flex = 2, flex = 3 => 1 + 2 + 3 = 6; 1/6, 2/6, 3/6

```javascript
import React from 'react';
import {StyleSheet, View} from 'react-native';

const Flex = () => {
  return (
    <View
      style={[
        styles.container,
        {
          // Try setting `flexDirection` to `"row"`.
          flexDirection: 'column',
        },
      ]}>
      <View style={{flex: 1, backgroundColor: 'red'}} />
      <View style={{flex: 2, backgroundColor: 'darkorange'}} />
      <View style={{flex: 3, backgroundColor: 'green'}} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
});

export default Flex;
```

2. in RN, every view is a flexbox by default
	1. Column is default (top to bottom)
	2. If width is not given, the box takes the minimum amount of space required
	3. `width: '80%', height: 300`
		1. Child elements stretch along the cross-axis
		2. Child elements do not stretch along the main axis
		4. `alignItems: 'stretch'` - default
	4. `flex: 1` - stretches to occupy all the space leaving other elements to take minimum space required
	5. `justifyContent: 'stretch'` - not allowed
3. Code: App.js

```javascript
import React from "react";
import { Text, View } from "react-native";

export default function App() {
  return (
    <View
      style={{
        padding: 50,
        flexDirection: "row",
        width: "80%",
        height: 300,
        justifyContent: "space-between",
        alignItems: "stretch",
      }}
    >
      <View
        style={{
          backgroundColor: "red",
          flex: 1,
          justifyContent: "center",
          alignItems: "center",
        }}
      >
        <Text>1</Text>
      </View>
      <View
        style={{
          backgroundColor: "blue",
          flex: 2,
          justifyContent: "center",
          alignItems: "center",
        }}
      >
        <Text>2</Text>
      </View>
      <View
        style={{
          backgroundColor: "green",
          justifyContent: "center",
          alignItems: "center",
        }}
      >
        <Text>3</Text>
      </View>
    </View>
  );
}
```

4. Flexbox is the tool to structure elements in RN
	1. Cannot turn off flexbox in `View`

### Quiz 1: Components, Styles, Layouts ###
### Improving the Layout ###
1. `Button` doesn't have `style` prop
2. Code: App.js

```javascript
import { Button, StyleSheet, Text, TextInput, View } from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  /* style prop */
  // First `View` - Users add text for the goal and click a button for the goal
  // Second `View` - List of goals rendered
  return (
    <View style={styles.appContainer}>
      <View style={styles.inputContainer}>
        <TextInput style={styles.textInput} placeholder="Your course goal!" />
        <Button title="Add Goal" />
      </View>
      <View style={styles.goalsContainer}>
        <Text>List of goals...</Text>
      </View>
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    paddingTop: 50,
    paddingHorizontal: 16,
  },
  inputContainer: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginBottom: 24,
    borderBottomWidth: 1,
    borderBottomColor: "#cccccc",
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#cccccc",
    width: "70%",
    marginRight: 8,
    padding: 8,
  },
  goalsContainer: {
    flex: 5,
  },
});
```

### Handling Events ###
1. Event handling is similar to the React Web application
	1. Handling events & managing state works exactly like in the Web app
2. Code: App.js

```javascript
import { useState } from "react";
import { Button, StyleSheet, Text, TextInput, View } from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  const [enteredGoalText, setEnteredGoalText] = useState("");

  function goalInputHandler(enteredText) {
    // console.log(enteredText);
    setEnteredGoalText(enteredText);
  }

  function addGoalHandler() {
    console.log(enteredGoalText);
  }

  return (
    <View style={styles.appContainer}>
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.textInput}
          placeholder="Your course goal!"
          onChangeText={goalInputHandler}
        />
        <Button title="Add Goal" onPress={addGoalHandler} />
      </View>
      <View style={styles.goalsContainer}>
        <Text>List of goals...</Text>
      </View>
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    paddingTop: 50,
    paddingHorizontal: 16,
  },
  inputContainer: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginBottom: 24,
    borderBottomWidth: 1,
    borderBottomColor: "#cccccc",
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#cccccc",
    width: "70%",
    marginRight: 8,
    padding: 8,
  },
  goalsContainer: {
    flex: 5,
  },
});
```

### Managing a List of Course Goals (in our Demo App) ###
1. Code: App.js

```javascript
import { useState } from "react";
import { Button, StyleSheet, Text, TextInput, View } from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  const [enteredGoalText, setEnteredGoalText] = useState("");
  const [courseGoals, setCourseGoals] = useState([]);

  function goalInputHandler(enteredText) {
    // console.log(enteredText);
    setEnteredGoalText(enteredText);
  }

  function addGoalHandler() {
    // console.log(enteredGoalText);
    // setCourseGoals([...courseGoals, enteredGoalText]); // not a good approach
    setCourseGoals((currentCourseGoals) => [
      ...currentCourseGoals,
      enteredGoalText,
    ]);
  }

  return (
    <View style={styles.appContainer}>
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.textInput}
          placeholder="Your course goal!"
          onChangeText={goalInputHandler}
        />
        <Button title="Add Goal" onPress={addGoalHandler} />
      </View>
      <View style={styles.goalsContainer}>
        {courseGoals.map((goal) => (
          <Text key={goal}>{goal}</Text>
        ))}
      </View>
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    paddingTop: 50,
    paddingHorizontal: 16,
  },
  inputContainer: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginBottom: 24,
    borderBottomWidth: 1,
    borderBottomColor: "#cccccc",
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#cccccc",
    width: "70%",
    marginRight: 8,
    padding: 8,
  },
  goalsContainer: {
    flex: 5,
  },
});
```

### iOS & Android Styling Differences ###
1. `borderRadius` - works on Android, but not in iOS
	1. `Text` is translated into a native UI element
		1. Android: Element where corners can be rounded
		2. iOS: Element which doesn't support rounded corners
	2. Solution: Wrap in `View`
		1. Underlying elements support rounded corners in both platforms
2. Styles don't cascade as in CSS
	1. Style inheritance is not supported
		1. Solution: Styles have to be applied on the element
3. There are differences under the hood of different platforms
	1. We may have to write different code in some cases

### Making Content Scrollable with ScrollView ###
1. `<View>` is not scrollable (Scrolling is default in Browsers)
	1. Solution: `<ScrollView>`
		1. View that is scrollable
			1. The space it occupies depends on the parant
		2. More info in official docs
			1. Props
				1. `alwaysBounceVertical` - iOS
				2. Some are iOS specific and some are Android specific and some are common
2. Code: App.js

```javascript
import { useState } from "react";
import {
  Button,
  ScrollView,
  StyleSheet,
  Text,
  TextInput,
  View,
} from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  const [enteredGoalText, setEnteredGoalText] = useState("");
  const [courseGoals, setCourseGoals] = useState([]);

  function goalInputHandler(enteredText) {
    // console.log(enteredText);
    setEnteredGoalText(enteredText);
  }

  function addGoalHandler() {
    // console.log(enteredGoalText);
    // setCourseGoals([...courseGoals, enteredGoalText]); // not a good approach
    setCourseGoals((currentCourseGoals) => [
      ...currentCourseGoals,
      enteredGoalText,
    ]);
  }

  return (
    <View style={styles.appContainer}>
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.textInput}
          placeholder="Your course goal!"
          onChangeText={goalInputHandler}
        />
        <Button title="Add Goal" onPress={addGoalHandler} />
      </View>
      <View style={styles.goalsContainer}>
        <ScrollView>
          {courseGoals.map((goal) => (
            <View style={styles.goalItem} key={goal}>
              <Text style={styles.goalText}>{goal}</Text>
            </View>
          ))}
        </ScrollView>
      </View>
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    paddingTop: 50,
    paddingHorizontal: 16,
  },
  inputContainer: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginBottom: 24,
    borderBottomWidth: 1,
    borderBottomColor: "#cccccc",
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#cccccc",
    width: "70%",
    marginRight: 8,
    padding: 8,
  },
  goalsContainer: {
    flex: 5,
  },
  goalItem: {
    borderRadius: 6,
    backgroundColor: "#5e0acc",
    margin: 8,
    padding: 8,
  },
  goalText: {
    color: "white",
  },
});
```

### Optimizing Lists with FlatList ###
1. If lists are too long, `<ScrollView>` renders all items which is not efficient
	1. Rendering even if items are not visible to the user causes performance issues
		1. Solution: `FlatList` **(M)**
			1. It will render only the items that are visible, and will lazily load the other items as the user scrolls
			2. `FlatList` supports many of the props that `ScrollView` supports
				1. Similar implementation internally, but with optimization
				2. We don't manually loop through the list. `FlatList` takes control of looping through
2. Code: App.js

```javascript
  <View style={styles.goalsContainer}>
	<FlatList
	  data={courseGoals}
	  renderItem={(itemData) => {
		// itemData.index
		return (
		  <View style={styles.goalItem}>
			<Text style={styles.goalText}>{itemData.item}</Text>
		  </View>
		);
	  }}
	/>
  </View>
```

3. Two main ways to add keys
	1. Convert data into an object that has a key
	
			function addGoalHandler() {
			  // console.log(enteredGoalText);
			  // setCourseGoals([...courseGoals, enteredGoalText]); // not a good approach
			  setCourseGoals((currentCourseGoals) => [
			    ...currentCourseGoals,
				{ text: enteredGoalText, key: Math.random().toString() },
			  ]);
			}
			
		1. `FlatList` looks for the `key` property in the data objects
	2. If there is no `key` in the input
		1. `keyExtractor` - called on every item to get a `key`
4. Code: App.js

```javascript
import { useState } from "react";
import {
  Button,
  FlatList,
  ScrollView,
  StyleSheet,
  Text,
  TextInput,
  View,
} from "react-native";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  const [enteredGoalText, setEnteredGoalText] = useState("");
  const [courseGoals, setCourseGoals] = useState([]);

  function goalInputHandler(enteredText) {
    // console.log(enteredText);
    setEnteredGoalText(enteredText);
  }

  function addGoalHandler() {
    // console.log(enteredGoalText);
    // setCourseGoals([...courseGoals, enteredGoalText]); // not a good approach
    setCourseGoals((currentCourseGoals) => [
      ...currentCourseGoals,
      { text: enteredGoalText, id: Math.random().toString() },
    ]);
  }

  return (
    <View style={styles.appContainer}>
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.textInput}
          placeholder="Your course goal!"
          onChangeText={goalInputHandler}
        />
        <Button title="Add Goal" onPress={addGoalHandler} />
      </View>
      <View style={styles.goalsContainer}>
        <FlatList
          data={courseGoals}
          renderItem={(itemData) => {
            // itemData.index
            return (
              <View style={styles.goalItem}>
                <Text style={styles.goalText}>{itemData.item.text}</Text>
              </View>
            );
          }}
          keyExtractor={(item, index) => {
            return item.id;
          }}
        />
      </View>
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    paddingTop: 50,
    paddingHorizontal: 16,
  },
  inputContainer: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginBottom: 24,
    borderBottomWidth: 1,
    borderBottomColor: "#cccccc",
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#cccccc",
    width: "70%",
    marginRight: 8,
    padding: 8,
  },
  goalsContainer: {
    flex: 5,
  },
  goalItem: {
    borderRadius: 6,
    backgroundColor: "#5e0acc",
    margin: 8,
    padding: 8,
  },
  goalText: {
    color: "white",
  },
});
```

### Quiz 2: More Components & Lists ###
### Splitting Components Into Smaller Components ###
1. It is good practice to keep style code close to JSX code

### Utlizing Props ###
1. Code: GoalItem.js

```javascript
import { StyleSheet, Text, View } from "react-native";

function GoalItem(props) {
  return (
    <View style={styles.goalItem}>
      <Text style={styles.goalText}>{props.text}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  goalItem: {
    borderRadius: 6,
    backgroundColor: "#5e0acc",
    margin: 8,
    padding: 8,
  },
  goalText: {
    color: "white",
  },
});

export default GoalItem;
```

### Working on the "Goal Input" Component ###
1. `value={enteredGoalText}` - bound to the state. Whenever the state changes, the component is re-rendered
2. Code: App.js

```javascript
import { useState } from "react";
import { FlatList, StyleSheet, View } from "react-native";
import GoalInput from "./components/GoalInput";
import GoalItem from "./components/GoalItem";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  const [courseGoals, setCourseGoals] = useState([]);

  function addGoalHandler(enteredGoalText) {
    // console.log(enteredGoalText);
    // setCourseGoals([...courseGoals, enteredGoalText]); // not a good approach
    setCourseGoals((currentCourseGoals) => [
      ...currentCourseGoals,
      { text: enteredGoalText, id: Math.random().toString() },
    ]);
  }

  return (
    <View style={styles.appContainer}>
      <GoalInput onAddGoal={addGoalHandler} />
      <View style={styles.goalsContainer}>
        <FlatList
          data={courseGoals}
          renderItem={(itemData) => {
            return <GoalItem text={itemData.item.text} />;
          }}
          keyExtractor={(item, index) => {
            return item.id;
          }}
        />
      </View>
    </View>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    paddingTop: 50,
    paddingHorizontal: 16,
  },
  goalsContainer: {
    flex: 5,
  },
});
```

2. Code: GoalInput.js

```javascript
import { useState } from "react";
import { Button, StyleSheet, TextInput, View } from "react-native";

function GoalInput({ onAddGoal }) {
  const [enteredGoalText, setEnteredGoalText] = useState("");

  function goalInputHandler(enteredText) {
    setEnteredGoalText(enteredText);
  }

  function addGoalHandler() {
    onAddGoal(enteredGoalText);
    setEnteredGoalText("");
  }

  return (
    <View style={styles.inputContainer}>
      <TextInput
        style={styles.textInput}
        placeholder="Your course goal!"
        onChangeText={goalInputHandler}
        value={enteredGoalText}
      />
      <Button title="Add Goal" onPress={addGoalHandler} />
    </View>
  );
}

const styles = StyleSheet.create({
  inputContainer: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginBottom: 24,
    borderBottomWidth: 1,
    borderBottomColor: "#cccccc",
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#cccccc",
    width: "70%",
    marginRight: 8,
    padding: 8,
  },
});

export default GoalInput;
```

3. Code: GoalItem.js

```javascript
import { StyleSheet, Text, View } from "react-native";

function GoalItem(props) {
  return (
    <View style={styles.goalItem}>
      <Text style={styles.goalText}>{props.text}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  goalItem: {
    borderRadius: 6,
    backgroundColor: "#5e0acc",
    margin: 8,
    padding: 8,
  },
  goalText: {
    color: "white",
  },
});

export default GoalItem;
```

### Handling Taps with the Pressable Component ###
1. `Pressable` - Used to wrap items that are pressable

### Making Items Deletable & Using IDs ###
### Adding an Android Ripple Effect & an iOS Alternative ###
1. Code: GoalItem.js

```javascript
import { StyleSheet, Text, View, Pressable } from "react-native";

function GoalItem(props) {
  // style={({ pressed }) => pressed && styles.pressedItem} - Called whenever the press state changes
  return (
    <View style={styles.goalItem}>
      <Pressable
        android_ripple={{ color: "#210644" }}
        onPress={props.onDeleteItem.bind(this, props.id)}
        style={({ pressed }) => pressed && styles.pressedItem}
      >
        <Text style={styles.goalText}>{props.text}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  goalItem: {
    borderRadius: 6,
    backgroundColor: "#5e0acc",
    margin: 8,
  },
  pressedItem: {
    opacity: 0.5,
  },
  goalText: {
    color: "white",
    padding: 8,
  },
});

export default GoalItem;
```

### Adding a Modal Screen ###
1. `<Modal visible={visible} animationType="slide">`
	1. `slide`
	2. `none`
	3. `fade`

### Styling the Modal Overlay ###
### Opening & Closing the Modal ###
### Working with Images & Changing Colors ###
### App Finishing Touches ###
1. app.json

```
"backgroundColor": "#1e085a",
```

2. Applied to all screens that are not overlays
3. Styling status bar:

```
import { StatusBar } from "expo-status-bar";

...
<StatusBar style="light" />
...
```

### Module Summary ###
1. Code: App.js

```javascript
import { useState } from "react";
import { Button, FlatList, StyleSheet, View } from "react-native";
import GoalInput from "./components/GoalInput";
import GoalItem from "./components/GoalItem";
import { StatusBar } from "expo-status-bar";

// Component built using core components
// Root component rendered in the app. Expo takes the component and render it as the root component
export default function App() {
  const [modalIsVisible, setModalIsVisible] = useState(false);
  const [courseGoals, setCourseGoals] = useState([]);

  function startAddGoalHandler() {
    setModalIsVisible(true);
  }

  function endAddGoalHandler() {
    setModalIsVisible(false);
  }

  function addGoalHandler(enteredGoalText) {
    // console.log(enteredGoalText);
    // setCourseGoals([...courseGoals, enteredGoalText]); // not a good approach
    setCourseGoals((currentCourseGoals) => [
      ...currentCourseGoals,
      { text: enteredGoalText, id: Math.random().toString() },
    ]);
    endAddGoalHandler();
  }

  function deleteGoalHandler(id) {
    // console.log("DELETE");
    setCourseGoals((currentCourseGoals) => {
      return currentCourseGoals.filter((goal) => goal.id !== id);
    });
  }

  return (
    <>
      <StatusBar style="light" />
      <View style={styles.appContainer}>
        <Button
          title="Add New Goal"
          color="#a065ec"
          onPress={startAddGoalHandler}
        />
        {/* Uses Pressable internally */}
        <GoalInput
          onAddGoal={addGoalHandler}
          visible={modalIsVisible}
          onCancel={endAddGoalHandler}
        />
        <View style={styles.goalsContainer}>
          <FlatList
            data={courseGoals}
            renderItem={(itemData) => {
              return (
                <GoalItem
                  text={itemData.item.text}
                  id={itemData.item.id}
                  onDeleteItem={deleteGoalHandler}
                />
              );
            }}
            keyExtractor={(item, index) => {
              return item.id;
            }}
          />
        </View>
      </View>
    </>
  );
}

// Similar to CSS
const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    paddingTop: 50,
    paddingHorizontal: 16,
  },
  goalsContainer: {
    flex: 5,
  },
});
```

2. Code: GoalInput.js

```javascript
import { useState } from "react";
import {
  Button,
  Image,
  Modal,
  StyleSheet,
  TextInput,
  View,
} from "react-native";

function GoalInput({ onAddGoal, visible, onCancel }) {
  const [enteredGoalText, setEnteredGoalText] = useState("");

  function goalInputHandler(enteredText) {
    setEnteredGoalText(enteredText);
  }

  function addGoalHandler() {
    onAddGoal(enteredGoalText);
    setEnteredGoalText("");
  }

  return (
    <Modal visible={visible} animationType="slide">
      <View style={styles.inputContainer}>
        <Image
          style={styles.image}
          source={require("../assets/images/goal.png")}
        />
        <TextInput
          style={styles.textInput}
          placeholder="Your course goal!"
          onChangeText={goalInputHandler}
          value={enteredGoalText}
        />
        <View style={styles.buttonContainer}>
          <View style={styles.button}>
            <Button title="Add Goal" onPress={addGoalHandler} color="#b180f0" />
          </View>
          <View style={styles.button}>
            <Button title="Cancel" onPress={onCancel} color="#f31282" />
          </View>
        </View>
      </View>
    </Modal>
  );
}

const styles = StyleSheet.create({
  inputContainer: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    padding: 16,
    backgroundColor: "#311b6b",
  },
  image: {
    width: 100,
    height: 100,
    margin: 20,
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#e4d0ff",
    backgroundColor: "#e4d0ff",
    color: "#120438",
    borderRadius: 6,
    width: "100%",
    padding: 16,
  },
  buttonContainer: {
    flexDirection: "row",
    marginTop: 16,
  },
  button: {
    width: "30%",
    marginHorizontal: 8,
  },
});

export default GoalInput;
```

3. Code: GoalItem.js

```javascript
import { StyleSheet, Text, View, Pressable } from "react-native";

function GoalItem(props) {
  // style={({ pressed }) => pressed && styles.pressedItem} - Called whenever the press state changes
  return (
    <View style={styles.goalItem}>
      <Pressable
        android_ripple={{ color: "#210644" }}
        onPress={props.onDeleteItem.bind(this, props.id)}
        style={({ pressed }) => pressed && styles.pressedItem}
      >
        <Text style={styles.goalText}>{props.text}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  goalItem: {
    borderRadius: 6,
    backgroundColor: "#5e0acc",
    margin: 8,
  },
  pressedItem: {
    opacity: 0.5,
  },
  goalText: {
    color: "white",
    padding: 8,
  },
});

export default GoalItem;
```

## Section 3: Debugging React Native Apps (Introduction) ##
### Module Introduction ###
1. Debugging RN Apps
	1. Understanding & Handling Errors
	2. Using DevTools
		1. RN tools
		2. Expo tools

### Handling Errors ###
1. Error messages can appear
	1. On device
	2. In terminal
		1. Stack trace
			1. Where the error message is
				1. Shows components
	3. Fixing: Official documentation

### Logging to the Console ###
1. `console.log('GoalInput component rendered.')` - appears on terminal
	1. To understand flows

### Debugging JavaScript Remotely ###
1. On terminal
	1. `m` - Developer menu (on emulator)
		1. `ctrl + m` - Android
		2. `cmd + d` - iOS
		3. Debug Remote JS
			1. New tab in Chrome
				1. Developer Tools
					1. Network
					2. Console - `console.log` messages
		4. Stop Remote debugging

### Using the React DevTools ###
1. Terminal
	1. Install them globally on system
		1. `npm install -g react-devtools` - standalone version of React dev tools (browser extension doesn't work for RN)
		2. `react-devtools`
	2. Open Developer menu (`m`)
		1. Debug Remote JS
			1. Component tree
				1. State
					1. We can update state

### Using the Documentation ###
1. RN official documentation

## Section 4: Diving Deeper into Components, Layouts & Styling - Building a Mini-Game App ##
### Module Introduction & What We'll Build ###
1. Fundamentals Deep Dive
	1. Building Real Apps & Layouts
		1. Build a Complete Demo App ("Guess my number" Game)
			1. Gradiants
			2. Background images
			3. Multiple screens to navigate
			4. Complex layouts
		2. New Core Components
		3. Complex Layouts & Styles
		4. Adding Reusable Componnts & Styles

### Starting Setup & Analyzing the Target App ###
1. Pick 1-99
2. Reset input
3. Start game
4. Guess lower or higher
5. Log is scrollable
6. Game over screen
	1. Start new game

### Setting Up our Screen Components ###
1. Screen - a React component

### Constructing Custom Buttons ###
1. Github React Native
	1. Source Code
		1. Libraries
			1. Components
				1. Button.js
					1. It is a combination of `View` and `Text`

### Styling for Android & iOS ###
1. Shadow - different from Web development
	1. Two ways that varies in Android and iOS
		1. Android: `elevation` - Takes numbers
			1. It has no effect on iOS
		2. iOS: `shadow-x` properties
			1. `shadowColor`
			2. `shadowOffset` - how much should the shadow offset from the original component it belongs to the left or to the right
			
					shadowOffset: { width: 0, height: 2 },
					
				1. `width: 0` - not offset to left or right
				2. `height: 2` - pushed down by 2 pixels
			3. `shadowOpacity` - how transparent
			4. `shadowRadius` - how much the shadow expands (takes number)
2. Code: StartGameScreen.js

```javascript
import { StyleSheet, TextInput, View } from "react-native";
import PrimaryButton from "../components/PrimaryButton";

function StartGameScreen() {
  return (
    <View style={styles.inputContainer}>
      <TextInput />
      <PrimaryButton>Reset</PrimaryButton>
      <PrimaryButton>Confirm</PrimaryButton>
    </View>
  );
}

const styles = StyleSheet.create({
  inputContainer: {
    marginTop: 100,
    marginHorizontal: 24,
    padding: 16,
    backgroundColor: "#72063c",
    borderRadius: 8,
    elevation: 4,
    shadowColor: "black",
    shadowOffset: { width: 0, height: 2 },
    shadowRadius: 6,
    shadowOpacity: 0.25,
  },
});

export default StartGameScreen;
```

### Styling the "Number Input" Element ###
1. Code: StartGameScreen.js

```
<TextInput style={styles.numberInput} maxLength={2} />
```

### Configuring the TextInput Field ###
1. `keyboardType: "number-pad"`
	1. Some types are common, but some are supported by iOS or Android (official docs)
2. `autoCorrect={false}` - it is used for auto correction of input

### Adding Visual Feedback to the Buttons ###
1. Code: PrimaryButton.JS

```javascript
style={({ pressed }) =>
  pressed
	? [styles.buttonInnerContainer, styles.pressed]
	: styles.buttonInnerContainer
}
```

2. Code: PrimaryButton.js

```javascript
import { Text, View, Pressable, StyleSheet } from "react-native";

function PrimaryButton({ children }) {
  function pressHandler() {
    console.log("Pressed!");
  }

  return (
    <View style={styles.buttonOuterContainer}>
      <Pressable
        style={({ pressed }) =>
          pressed
            ? [styles.buttonInnerContainer, styles.pressed]
            : styles.buttonInnerContainer
        }
        onPress={pressHandler}
        android_ripple={{ color: "#640233" }}
      >
        <Text style={styles.buttonText}>{children}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonOuterContainer: {
    borderRadius: 28,
    margin: 4,
    overflow: "hidden",
  },
  buttonInnerContainer: {
    backgroundColor: "#72063c",
    paddingVertical: 8,
    paddingHorizontal: 16,
    elevation: 2,
  },
  buttonText: {
    color: "white",
    textAlign: "center",
  },
  pressed: {
    opacity: 0.75,
  },
});

export default PrimaryButton;

```

### Improving the Buttons ###
1. Every new `View` constructs a flexbox container
2. `View`s take up only as much space as they need to fit the content

### Coloring the Components & The Overall App ###
3. Code: App.js

```javascript
import { StyleSheet, View } from "react-native";
import StartGameScreen from "./screens/StartGameScreen";

export default function App() {
  return (
    <View style={styles.rootScreen}>
      <StartGameScreen />
    </View>
  );
}

const styles = StyleSheet.create({
  rootScreen: {
    flex: 1,
    backgroundColor: "#ddb52f",
  },
});
```

### Adding a Linear Gradient ###
1. `expo-linear-gradiant`
	1. `expo install expo-linear-gradient` - installs fitting version (checks expo version and installs dependencies)
		1. Newer version: `npx expo expo-linear-gradient`
2. Code: App.js

```javascript
import { StyleSheet, View } from "react-native";
import StartGameScreen from "./screens/StartGameScreen";
import { LinearGradient } from "expo-linear-gradient";

export default function App() {
  return (
    <LinearGradient colors={["#4e0329", "#ddb52f"]} style={styles.rootScreen}>
      <StartGameScreen />
    </LinearGradient>
  );
}

const styles = StyleSheet.create({
  rootScreen: {
    flex: 1,
  },
});
```

### Adding a Background Image ###
1. Unsplash - image repository
2. `ImageBackground` - internally, it is a combination of `View` and `Image`
	1. `style` - added to `View`
	2. `Image` - receives `imageStyle`
3. Code: App.js

```javascript
import { LinearGradient } from "expo-linear-gradient";
import { StyleSheet, ImageBackground } from "react-native";
import StartGameScreen from "./screens/StartGameScreen";

export default function App() {
  return (
    <LinearGradient colors={["#4e0329", "#ddb52f"]} style={styles.rootScreen}>
      <ImageBackground
        source={require("./assets/images/background.png")}
        resizeMode="cover"
        style={styles.rootScreen}
        imageStyle={styles.backgroundImage}
      >
        <StartGameScreen />
      </ImageBackground>
    </LinearGradient>
  );
}

const styles = StyleSheet.create({
  rootScreen: {
    flex: 1,
  },
  backgroundImage: {
    opacity: 0.15,
  },
});
```

### Getting Started with the Game Logic ###
1. `TextInput` always returns a string

### Handling User Input & Showing an Alert Dialog ###

### Switching Screens Programmatically ###
### Starting Work on the Game Screen ###
### Respecting Device Screen Restrictions with the SafeAreaView ###
1. Adding appropriate amount of spacing based on the notch or other content around.
	1. Solution: `SafeAreaView` - wrap it arround the main content
2. Code: App.js

```javascript
import { StyleSheet, ImageBackground, SafeAreaView } from "react-native";
...

export default function App() {
  ...

  return (
    <LinearGradient colors={["#4e0329", "#ddb52f"]} style={styles.rootScreen}>
      <ImageBackground
        source={require("./assets/images/background.png")}
        resizeMode="cover"
        style={styles.rootScreen}
        imageStyle={styles.backgroundImage}
      >
        <SafeAreaView style={styles.rootScreen}>{screen}</SafeAreaView>
      </ImageBackground>
    </LinearGradient>
  );
}

const styles = StyleSheet.create({
  rootScreen: {
    flex: 1,
  },
  backgroundImage: {
    opacity: 0.15,
  },
});
```

### Constructing a Title Component ###
1. Code: Title.js

```javascript 
import { StyleSheet, Text } from "react-native";

function Title({ children }) {
  return <Text style={styles.title}>{children}</Text>;
}

const styles = StyleSheet.create({
  title: {
    fontSize: 24,
    fontWeight: "bold",
    color: "#ddb52f",
    textAlign: "center",
    borderWidth: 2,
    borderColor: "#ddb52f",
    padding: 12,
  },
});

export default Title;
```

### Managing Colors Globally ###
1. Code: colors.js

```javascript
const Colors = {
  primary500: "#72063c",
  primary600: "#640233",
  primary700: "#4e0329",
  primary800: "#3b021f",
  accent500: "#ddb52f",
};

export default Colors;
```

### Constructing, Using & Displaying Random Numbers ###
1. Code: NumberContainer.js

```javascript
import { Text, View, StyleSheet } from "react-native";
import Colors from "../../constants/colors";

function NumberContainer({ children }) {
  return (
    <View style={styles.container}>
      <Text style={styles.numberText}>{children}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    borderWidth: 4,
    borderColor: Colors.accent500,
    padding: 24,
    margin: 24,
    borderRadius: 8,
    alignItems: "center",
    justifyContent: "center",
  },
  numberText: {
    color: Colors.accent500,
    fontSize: 36,
    fontWeight: "bold",
  },
});

export default NumberContainer;
```

### Adding Game Control Buttons ("+" & "-") to the App ###
### Checking for "Game Over" ###
### Improving the Game Screen Visuals ###
### Using "Cascading Styles" ###
1. Code: InstructionText.js

```javascript
import { Text, StyleSheet } from "react-native";
import Colors from "../../constants/colors";

function InstructionText({ children, style }) {
  return <Text style={[styles.instructionText, style]}>{children}</Text>;
}

const styles = StyleSheet.create({
  instructionText: {
    color: Colors.accent500,
    fontSize: 24,
  },
});

export default InstructionText;
```

1. The styles passed in `style` object will override the styles in the `instructText`.

### Working with Icons (Button Icons) ###
1. `@expo/vector-icons` - Documentation

```javascript
import { Ionicons } from "@expo/vector-icons";

<Ionicons name="remove" size={24} color="white" />
...
<Ionicons name="add" size={24} color="white" />
```

### Adding & Using Custom Fonts with React Native Apps ###
1. Custom fonts
	1. Expo
		1. Set up in the root components (we want to load when app starts)
		
		```bash
		expo install expo-font
		```
		
		2. Expo fonts documentation
		3. Load the fonts: App.js
		
		```javascript
		import { useFonts } from "expo-font";
		...
		  const [fontsLoaded] = useFonts({
			"open-sans": require("./assets/fonts/OpenSans-Regular.ttf"),
			"open-sans-bold": require("./assets/fonts/OpenSans-Bold.ttf"),
		  });
		...
		```
		
		4. App loading screen until fonts are initialized
		
		```bash
		expo install expo-app-loading
		
		# utility that can render which will prolong the splash screen until some condition is met
		```
		
		5. Returning `AppLoading` component when fonts are loading
		
		```javascript
		...
		  if (!fontsLoaded) {
			return <AppLoading />;
		  }
		...
		```
		
		6. Using the fonts:
		
		```javascript
		...
		const styles = StyleSheet.create({
		  instructionText: {
			...
			fontFamily: "open-sans",
			...
		  },
		});
		...
		```

### Adding a (Foreground) Image ###
1. `%` - wrt the container in which the current element is placed.

### Using & Styling Nested Text ###
1. Nested `<Text>` components is allowed
	1. A nested `<Text>` element gets the font-size of the outer `<Text>` (because that is how they are compiled to native components)

### Adding Logic to (Re-)Started Games & Displaying a Summary Screen ###
### Logging Game Rounds ###
### Outputting Log Data with FlatList ###
1. Code: GameScreen.js

```javascript
<FlatList
  data={guessRounds}
  renderItem={(itemData) => <Text>{itemData.item}</Text>}
  keyExtractor={(item) => item}
/>
```

### Styling the Game Round Logs ###
### Finishing Touches ###
1. Code: [https://github.com/bmutthoju/mini-game-app](https://github.com/bmutthoju/mini-game-app)

### Module Summary ###
1. Can fine-tune
	1. Styling
	2. Layout
2. Built-in core components
3. Styling
4. Own components
5. General UI components
6. App specific components
7. Switching between multiple screens
8. Core react features
	1. State
	2. `useEffect`
9. Tips & Tricks - styling, Custom buttons, ...
10. Get into official docs
11. More:
	1. Extract more components
	2. Build more reusable components
	4. Style-cascading effect in other components
12. Next:
	1. Adapting to different screen sizes 
		1. Rotate and use the app in landscape mode

## Section 5: Building Adaptive User Interfaces (Adapt to Platform & Device Sizes) ##
### Module Introduction ###
1. Adaptive & Responsive UIs
	1. Building Cross-Platform & Device User Interfaces
		1. Execute platform-specific Code
			1. In some cases we can differentiate between the platforms and execute slightly different code based on platform we are running
		2. Adjust to Different Device Sizes
			1. Update styling or layout based on available width and height
			2. React to screen orientation
	2. Build Adaptive Components
		1. They live in the same code base & adapt to different environments

### Setting Dynamic Widths ###
1. `maxWidth` - it is upto 80%

```javascript
maxWidth: "80%",
width: 300,
```

2. Width is 300px unless it is more than 80% of the screen width, in which case only 80% of the width is taken.

		min(300, 80%)

### Introducing the Dimenstions API ###
1. Smaller font size, less margin, ...
	1. `Dimensions` API
		1. `screen` - entire screen on Android (including status bar)
		2. `window` - excluding the status bar (where UI should be painted) on Android
2. Code: NumberContainer.js

```javascript
import { Text, View, StyleSheet, Dimensions } from "react-native";
import Colors from "../../constants/colors";

function NumberContainer({ children }) {
  return (
    <View style={styles.container}>
      <Text style={styles.numberText}>{children}</Text>
    </View>
  );
}

const deviceWidth = Dimensions.get("window").width;

const styles = StyleSheet.create({
  container: {
    borderWidth: 4,
    borderColor: Colors.accent500,
    padding: deviceWidth < 380 ? 12 : 24,
    margin: deviceWidth < 380 ? 12 : 24,
    borderRadius: 8,
    alignItems: "center",
    justifyContent: "center",
  },
  numberText: {
    color: Colors.accent500,
    fontFamily: "open-sans-bold",
    fontSize: deviceWidth < 380 ? 28 : 36,
  },
});

export default NumberContainer;
```

### Adjusting Image Sizes with the Dimensions API ###
### Understanding Screen Orientation Problems ###
1. app.json

```json
"orientation": "portrait", // locked to portrait mode
```

```json
"orientation": "default", // portrait or landscape mode
```

2. Android: Ensure `Auto-rotate` is on

### Setting Sizes Dynamically (for different Orientations) ###
1. Code: StartGameScreen.js

```javascript
import {
  ...,
  useWindowDimensions,
  ...
} from 'react-native';

...
function StartGameScreen({...}) {
  ...
  const { width, height } = useWindowDimensions();
  ...
  const marginTopDistance = height < 380 ? 30 : 100;
  ...
  return (
    <View style={[..., { marginTop: marginTopDistance }]}>
		...
  ...
}
```

### Managing Screen Content with KeyboardAvoidingView ###
1. Keyboard: `KeyboardAvoidingView`
	1. Component
	2. To wrap other content that contains an input field
	3. Whenever the keyboard opens, the content moves up if keyboard is open
2. Code: StartGameScreen.js

```javascript
...
return <ScrollView style={styles.screen}>
      {/* We should get all the space */}
         <KeyboardAvoidingView style={styles.screen} behavior="position">
           <View style={[styles.rootContainer, { marginTop: marginTopDistance }]}>
...
```

### Improving the Landscape Mode UI ###
1. Code: GameScreen.js

```javascript
  const { width, height } = useWindowDimensions();
  ...
  let content = (
    <>
      <NumberContainer>{currentGuess}</NumberContainer>
      <Card>
        <InstructionText style={styles.instructionText}>
          Higher or lower?
        </InstructionText>
        <View style={styles.buttonsContainer}>
          <View style={styles.buttonContainer}>
            <PrimaryButton onPress={nextGuessHandler.bind(this, "lower")}>
              <Ionicons name="remove" size={24} color="white" />
            </PrimaryButton>
          </View>
          <View style={styles.buttonContainer}>
            <PrimaryButton onPress={nextGuessHandler.bind(this, "greater")}>
              <Ionicons name="add" size={24} color="white" />
            </PrimaryButton>
          </View>
        </View>
      </Card>
    </>
  );

  if (width > 500) {
    content = (
      <>
        <View style={styles.buttonsContainerWide}>
          <View style={styles.buttonContainer}>
            <PrimaryButton onPress={nextGuessHandler.bind(this, "lower")}>
              <Ionicons name="remove" size={24} color="white" />
            </PrimaryButton>
          </View>
          <NumberContainer>{currentGuess}</NumberContainer>
          <View style={styles.buttonContainer}>
            <PrimaryButton onPress={nextGuessHandler.bind(this, "greater")}>
              <Ionicons name="add" size={24} color="white" />
            </PrimaryButton>
          </View>
        </View>
      </>
    );
  }
  ...
  return (
    <View style={styles.screen}>
      <Title>Opponent's Guess</Title>
      {content}
	...
```

### Quiz 3: The Dimensions API & Responsive UIs ###
### Further Improvements with useWindowDimensions ###
1. Code: GameOverScreen.js

```javascript
function GameOverScreen({ roundsNumber, userNumber, onStartNewGame }) {
  const { width, height } = useWindowDimensions();

  let imageSize = 300;

  if (width < 380) {
    imageSize = 150;
  }

  if (height < 380) {
    imageSize = 80;
  }

  const imageStyle = {
    width: imageSize,
    height: imageSize,
    borderRadius: imageSize / 2,
  };

  return (
    <ScrollView style={styles.screen}>
      <View style={styles.rootContainer}>
        <Title>GAME OVER!</Title>
        <View style={styles.imageContainer}>
		...
```

### Writing Platform-specific Code with the Platform API ###
1. Code: Title.js

```
import { StyleSheet, Text, Platform } from "react-native";
...
const styles = StyleSheet.create({
  title: {
    ...
    // borderWidth: 2,
    // borderWidth: Platform.OS === "android" ? 2 : 0,
    borderWidth: Platform.select({ ios: 0, android: 2 }),
...
```

#### Different files for different platforms ####
1. We just have to append `.android.js` and `.ios.js` that are automatically picked up by RN.
2. Title.android.js

```
import { StyleSheet, Text, Platform } from "react-native";

// Platform is the same throughout the lifestyle of the app

function Title({ children }) {
  return <Text style={styles.title}>{children}</Text>;
}

const styles = StyleSheet.create({
  title: {
    fontFamily: "open-sans-bold",
    fontSize: 24,
    color: "white",
    textAlign: "center",
    borderWidth: 2,
    borderColor: "white",
    padding: 12,
    maxWidth: "80%",
    width: 300,
  },
});

export default Title;
```

3. Title.ios.js

```javascript
import { StyleSheet, Text, Platform } from "react-native";

// Platform is the same throughout the lifestyle of the app

function Title({ children }) {
  return <Text style={styles.title}>{children}</Text>;
}

const styles = StyleSheet.create({
  title: {
    fontFamily: "open-sans-bold",
    fontSize: 24,
    color: "white",
    textAlign: "center",
    borderColor: "white",
    padding: 12,
    maxWidth: "80%",
    width: 300,
  },
});

export default Title;
```

### Styling the Status Bar ###
1. StatusBar - Component exposed by expo that controls how status bar looks like
2. Code: App.js

```javascript
import { StatusBar } from "expo-status-bar";
...
 return (
    <>
      <StatusBar style="light" />
      <LinearGradient
        colors={[Colors.primary700, Colors.accent500]}
        style={styles.rootScreen}
      >
        <ImageBackground
          source={require("./assets/images/background.png")}
          resizeMode="cover"
          style={styles.rootScreen}
          imageStyle={styles.backgroundImage}
        >
          <SafeAreaView style={styles.rootScreen}>{screen}</SafeAreaView>
        </ImageBackground>
      </LinearGradient>
    </>
  );
```

## Section 6: React Native Navigation with React Navigation [MEALS APP] ##
### Module Introduction ###
1. Topics:
	1. Navigation between screens
		1. Previous approach
			1. No animation
			2. No forwards or backwards
		2. What is "Navigation"?
		3. Using Stack Navigation
		4. Drawers & Tabs

### What is Navigation? ###
1. What is it?
	1. We don't have URLs to navigate as in the Web
2. App details:
	1. Meals app
		1. Users can choose among categories
		2. View details about a meal
	2. Dummy Data JS file

### Getting Started with the App & Outputting Meal Categories ###
### Displaying Items in a Grid ###
### Getting Started with the React Navigation Package ###
1. React Navigation - 3rd party package
	1. Routing and navigation for Expo and React Native apps
		1. Easy to integrate with Expo
			1. Docs - look up for more features
2. Steps:
	1. `npm i @react-navigation/native`
	2. `expo install react-native-screens react-native-safe-area-context`
	3. Component-based library
		1. Code: NavigationContainer
		
		```javascript
		import { NavigationContainer } from "@react-navigation/native";
		...
		<NavigationContainer>
          <CategoriesScreen />
        </NavigationContainer>
		```
		
		2. Navigators: They implement different navigation behaviors
			1. Types:
				1. Stack
				2. Native Stack
				3. Drawer
				4. xxx Tabs
			2. `npm i @react-navigation/native-stack`
		4. Working Code: App.js
		
		```javascript
		import { createStaticNavigation } from "@react-navigation/native";
		import { createNativeStackNavigator } from "@react-navigation/native-stack";
		import { StyleSheet } from "react-native";
		import CategoriesScreen from "./screens/CategoriesScreen";
		import { StatusBar } from "expo-status-bar";

		const Stack = createNativeStackNavigator({
		  screens: {
			MealsCategories: CategoriesScreen,
		  },
		}); // Object with 2 properties. Every property acts as a component

		const Navigation = createStaticNavigation(Stack);

		export default function App() {
		  return (
			<>
			  <StatusBar style="dark" />
			  <Navigation />
			</>
		  );
		}

		const styles = StyleSheet.create({
		  container: {
			flex: 1,
			backgroundColor: "#fff",
			alignItems: "center",
			justifyContent: "center",
		  },
		});
		```
		
	1. We get default wrapper layout

### Implementing Navigation Between Two Screens ###
1. Working Code: App.js

```javascript
import { createStaticNavigation } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import { StyleSheet } from "react-native";
import CategoriesScreen from "./screens/CategoriesScreen";
import { StatusBar } from "expo-status-bar";
import MealsOverviewScreen from "./screens/MealsOverviewScreen";

const Stack = createNativeStackNavigator({
  screens: {
    MealsCategories: CategoriesScreen,
    MealsOverview: MealsOverviewScreen,
  },
}); // Object with 2 properties. Every property acts as a component

const Navigation = createStaticNavigation(Stack);

export default function App() {
  return (
    <>
      <StatusBar style="dark" />
      <Navigation />
    </>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

2. Working Code: CategoriesScreen.js

```javascript
import { FlatList } from "react-native";
import { CATEGORIES } from "../data/dummy-data";
import CategoryGridTile from "../components/CategoryGridTile";
import { useNavigation } from "@react-navigation/native";

// `navigation` is provided by navigation
function CategoriesScreen() {
  const navigation = useNavigation();

  function renderCategoryItem(itemData) {
    function pressHandler() {
      navigation.navigate("MealsOverview");
    }

    return (
      <CategoryGridTile
        title={itemData.item.title}
        color={itemData.item.color}
        onPress={pressHandler}
      />
    );
  }

  return (
    <FlatList
      data={CATEGORIES}
      keyExtractor={(item) => item.id}
      renderItem={renderCategoryItem}
      numColumns={2}
    />
  );
}

export default CategoriesScreen;
```

### Setting the Default Screen ###
1. We can decide which screen will be shown as default when the app starts
	1. top-most screen (first child inside `screens`) is used as initial screen
	2. Alternatively, there is `initialRouteName` prop that can be set to navigator component
	
	```javascript
	<Stack.Navigator initialRouteName="ProductDetails">
	  <Stack.Screen name="AllProducts" component={AllProducts} /> 
	  <Stack.Screen name="ProductDetails" component={ProductDetails} /> // initial screen
	</Stack.Navigator>
	```

### Understanding the useNavigation Hook ###
1. `Stack` vs `NativeStack`
	1. `NativeStack` - uses native platform elements for animation for the screens
		1. It can be more performant than Stack that emulates the native behaviors
			1. It can be used as a fall-back
2. Hook: `useNavigation()` - can be used in a nested component (even if it is not registered as a screen)

```javascript
import { useNavigation } from '@react-navigation/native';
...
const navigation = useNavigation();
...
```

### Working with Route Parameters to Pass Data Between Screens ###
1. Route: Used to get parameters passed from previous screen

```javascript
import { useRoute } from "@react-navigation/native";
...
const route = useRoute();
const catId = route.params.categoryId;
...
```

### Displaying Meals ###
### Adding Images & Styling ###
1. Code: MealItem.js

```javascript
import {
  Image,
  Platform,
  Pressable,
  StyleSheet,
  Text,
  View,
} from "react-native";

function MealItem({ title, imageUrl, duration, complexity, affordability }) {
  return (
    <View style={styles.mealItem}>
      <Pressable
        android_ripple={{ color: "#ccc" }}
        style={({ pressed }) => (pressed ? styles.buttonPressed : null)}
      >
        <View style={styles.innerContainer}>
          <View>
            {/* For remote image width and height must be defined because they cannot be inferred. For local images, the defaults are used */}
            <Image source={{ uri: imageUrl }} style={styles.image} />
            <Text style={styles.title}>{title}</Text>
          </View>
          <View style={styles.details}>
            <Text style={styles.detailItem}>{duration}m</Text>
            <Text style={styles.detailItem}>{complexity.toUpperCase()}</Text>
            <Text style={styles.detailItem}>{affordability.toUpperCase()}</Text>
          </View>
        </View>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  mealItem: {
    margin: 16,
    borderRadius: 8,
    overflow: Platform.OS === "android" ? "hidden" : "visible",
    backgroundColor: "white",
    elevation: 4,
    shadowColor: "black",
    shadowOpacity: 0.35,
    shadowOffset: { width: 0, height: 2 },
    shadowRadius: 8,
  },
  buttonPressed: {
    opacity: 0.5,
  },
  innerContainer: {
    borderRadius: 8,
    overflow: "hidden",
  },
  image: {
    width: "100%",
    height: 200,
  },
  title: {
    fontWeight: "bold",
    textAlign: "center",
    fontSize: 18,
    margin: 8,
  },
  details: {
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "center",
    padding: 8,
  },
  detailItem: {
    marginHorizontal: 4,
    fontSize: 12,
  },
});

export default MealItem;
```

### Styling Screen Headers & Backgrounds ###
1. Fine-tuning navigation header

### Setting Navigation Options Dynamically ###
1. Code: App.js

```javascript
import { createStaticNavigation } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import { StyleSheet } from "react-native";
import CategoriesScreen from "./screens/CategoriesScreen";
import { StatusBar } from "expo-status-bar";
import MealsOverviewScreen from "./screens/MealsOverviewScreen";

const Stack = createNativeStackNavigator({
  screenOptions: {
    headerStyle: {
      backgroundColor: "#351401",
    },
    headerTintColor: "white",
    contentStyle: {
      backgroundColor: "#3f2f25",
    },
  },
  screens: {
    MealsCategories: {
      screen: CategoriesScreen,
      options: {
        title: "Meals Categories",
      },
    },
    MealsOverview: {
      screen: MealsOverviewScreen,
      // options: ({ route, navigation }) => {
      //   // Executed whenever screen becomes active
      //   const catId = route.params.categoryId;
      //   return {
      //     title: catId,
      //   };
      // },
    },
  },
}); // Object with 2 properties. Every property acts as a component

const Navigation = createStaticNavigation(Stack);

export default function App() {
  return (
    <>
      <StatusBar style="light" />
      <Navigation />
    </>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

2. Code: MealsOverviewScreen.js

```javascript
import { useNavigation, useRoute } from "@react-navigation/native";
import { StyleSheet, FlatList, View, Text } from "react-native";
import MealItem from "../components/MealItem";
import { CATEGORIES, MEALS } from "../data/dummy-data";
import { useLayoutEffect } from "react";

function MealsOverviewScreen() {
  const navigation = useNavigation();
  const route = useRoute();
  const catId = route.params.categoryId;

  const displayedMeals = MEALS.filter((mealItem) => {
    return mealItem.categoryIds.indexOf(catId) >= 0;
  });

  // console.log(catId);

  // We have ongoing animation, so we want to execute a side effect while this animation is happening and before the component has been rendered (`useEffect` runs after the component is rendered)
  useLayoutEffect(() => {
    const categoryTitle = CATEGORIES.find(
      (category) => category.id === catId
    ).title;
    navigation.setOptions({
      title: categoryTitle,
    });
  }, [catId, navigation]);

  function renderMealItem(itemData) {
    const item = itemData.item;
    const mealItemProps = {
      title: item.title,
      imageUrl: item.imageUrl,
      affordability: item.affordability,
      complexity: item.complexity,
      duration: item.duration,
    };

    return <MealItem {...mealItemProps} />;
  }

  return (
    <View style={styles.container}>
      <FlatList
        data={displayedMeals}
        keyExtractor={(item) => item.id}
        renderItem={renderMealItem}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
  },
});

export default MealsOverviewScreen;
```

### Adding & Configuring the Meal Details Screen ###
1. RN Documentation
	1. Navigators
		1. Drawer
		2. xxx Tabs

### Outputting Content in the Meal Detail Screen ###
### Finishing the Meal Detail Screen ###
### Adding Header Buttons ###
### Adding an Icon Button to a Header ###
### Adding Drawer Navigation & Constructing a Drawer ###
#### Drawer ####
1. Installation:

```
npm install @react-navigation/drawer
npx expo install react-native-gesture-handler react-native-reanimated
```

2. Code: App.js

```javascript
import { createDrawerNavigator } from "@react-navigation/drawer";
import { createStaticNavigation } from "@react-navigation/native";
import {
  default as UserScreen,
  default as WelcomeScreen,
} from "./screens/WelcomeScreen";

const MyDrawer = createDrawerNavigator({
  // initialRouteName: "UserScreen",
  screens: {
    Welcome: WelcomeScreen,
    User: UserScreen,
  },
}); // Two properties for drawer and screens to be served

const Navigation = createStaticNavigation(MyDrawer);

export default function App() {
  return <Navigation />;
}
```

### Configuring the Drawer Navigator & The Drawer ###
1. We can render custom component inside the drawer instead of configuring the pre-built items added automatically
2. Code: App.js

```javascript
import { createDrawerNavigator } from "@react-navigation/drawer";
import { createStaticNavigation } from "@react-navigation/native";
import WelcomeScreen from "./screens/WelcomeScreen";
import UserScreen from "./screens/UserScreen";
import { Ionicons } from "@expo/vector-icons";

const Drawer = createDrawerNavigator({
  screenOptions: {
    headerStyle: {
      backgroundColor: "#3c0a6b",
    },
    headerTintColor: "white",
    drawerActiveBackgroundColor: "#f0e1ff",
    drawerActiveTintColor: "#3c0a6b",
    // drawerStyle: {
    //   backgroundColor: "#ccc",
    // },
  },
  screens: {
    Welcome: {
      screen: WelcomeScreen,
      options: {
        drawerLabel: "Welcome Screen",
        // color - it is provided by the navigator. It is different based on whether the item is selected or not.
        // size - provided by the navigator
        // A boolean that tells us whether the item is selected or not
        drawerIcon: ({ color, size }) => (
          <Ionicons name="home" color={color} size={size} />
        ),
      },
    },
    User: {
      screen: UserScreen,
      options: {
        drawerLabel: "User Screen",
        drawerIcon: ({ color, size }) => (
          <Ionicons name="person" color={color} size={size} />
        ),
      },
    },
  },
}); // Two properties for drawer and screens to be served

const Navigation = createStaticNavigation(Drawer);

export default function App() {
  return <Navigation />;
}
```

3. Code: UserScreen.js

```javascript
import { useNavigation } from "@react-navigation/native";
import { View, Text, Button, StyleSheet } from "react-native";

function UserScreen() {
  const navigation = useNavigation();

  function openDrawerHandler() {
    navigation.toggleDrawer();
  }

  return (
    <View style={styles.rootContainer}>
      <Text>
        This is the <Text style={styles.highlight}>"User"</Text> screen!
      </Text>
      <Button title="Open Drawer" onPress={openDrawerHandler} />
    </View>
  );
}

export default UserScreen;

const styles = StyleSheet.create({
  rootContainer: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  highlight: {
    fontWeight: "bold",
    color: "#eb1064",
  },
});
```

### Adding, Configuring & Using Bottom Tabs ###
1. Tabs:
	1. Bottom Tabs - Good for iOS and Android
	2. Material Bottom Tabs - Android specific or android like look
	3. Material Top Tabs
2. Code: App.js

```javascript
import { Ionicons } from "@expo/vector-icons";
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";
import { createStaticNavigation } from "@react-navigation/native";
import UserScreen from "./screens/UserScreen";
import WelcomeScreen from "./screens/WelcomeScreen";

const BottomTab = createBottomTabNavigator({
  screenOptions: {
    headerStyle: {
      backgroundColor: "#3c0a6b",
    },
    headerTintColor: "white",
    tabBarActiveTintColor: "#3c0a6b",
  },
  screens: {
    Welcome: {
      screen: WelcomeScreen,
      options: {
        tabBarIcon: ({ color, size }) => (
          <Ionicons name="home" color={color} size={size} />
        ),
      },
    },
    User: {
      screen: UserScreen,
      options: {
        tabBarIcon: ({ color, size }) => (
          <Ionicons name="person" color={color} size={size} />
        ),
      },
    },
  },
});

// const Navigation = createStaticNavigation(Drawer);
const Navigation = createStaticNavigation(BottomTab);

export default function App() {
  return <Navigation />;
}
```

### Nesting Navigators ###
1. Nested Navigators
	1. Root Navigation Container
		1. Drawer Navigator
			1. Screen A (Welcome Screen) -> Screen B (User Screen) (stack navigator)
			2. Screen C (Settings Screen)
2. Code: App.js

```javascript
import { createStaticNavigation } from "@react-navigation/native";
import { createDrawerNavigator } from "@react-navigation/drawer";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import { StatusBar } from "expo-status-bar";
import { StyleSheet } from "react-native";
import CategoriesScreen from "./screens/CategoriesScreen";
import MealDetailScreen from "./screens/MealDetailScreen";
import MealsOverviewScreen from "./screens/MealsOverviewScreen";
import FavoritesScreen from "./screens/FavoritesScreen";

const Drawer = createDrawerNavigator({
  screenOptions: {
    headerStyle: {
      backgroundColor: "#351401",
    },
    headerTintColor: "white",
    sceneStyle: {
      backgroundColor: "#3f2f25",
    },
  },
  screens: {
    CategoriesScreen: {
      screen: CategoriesScreen,
      options: {
        title: "All Categories",
      },
    },
    Favorites: {
      screen: FavoritesScreen,
      options: {
        title: "Favorites",
      },
    },
  },
});

const Stack = createNativeStackNavigator({
  screenOptions: {
    headerStyle: {
      backgroundColor: "#351401",
    },
    headerTintColor: "white",
    contentStyle: {
      backgroundColor: "#3f2f25",
    },
  },
  screens: {
    MealsCategories: {
      screen: Drawer,
      options: {
        title: "About the Meal",
        headerShown: false,
      },
    },
    MealsOverview: {
      screen: MealsOverviewScreen,
      // options: ({ route, navigation }) => {
      //   // Executed whenever screen becomes active
      //   const catId = route.params.categoryId;
      //   return {
      //     title: catId,
      //   };
      // },
    },
    MealDetail: {
      screen: MealDetailScreen,
      options: {
        title: "Meal Detail",
        // headerRight: () => {
        //   return <Button title="Tap me!" onPress={} />;
        // },
        // good if it doesn't need direct interaction with the screen
      },
    },
  },
}); // Object with 2 properties. Every property acts as a component

const Navigation = createStaticNavigation(Stack);

function DrawerNavigator() {}

export default function App() {
  return (
    <>
      <StatusBar style="light" />
      <Navigation />
    </>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

### Bottom Tabs & App Finishing Touches ###
1. Code: App.js

```javascript
const Drawer = createDrawerNavigator({
  screenOptions: {
    headerStyle: {
      backgroundColor: "#351401",
    },
    headerTintColor: "white",
    sceneStyle: {
      backgroundColor: "#3f2f25",
    },
    drawerContentStyle: { backgroundColor: "#351401" },
    drawerInactiveTintColor: "white",
    drawerActiveTintColor: "#351401",
    drawerActiveBackgroundColor: "#e4baa1",
  },
  screens: {
    CategoriesScreen: {
      screen: CategoriesScreen,
      options: {
        title: "All Categories",
        drawerIcon: ({ color, size }) => (
          <Ionicons name="list" color={color} size={size} />
        ),
      },
    },
    Favorites: {
      screen: FavoritesScreen,
      options: {
        title: "Favorites",
        drawerIcon: ({ color, size }) => (
          <Ionicons name="star" color={color} size={size} />
        ),
      },
    },
  },
});
```

### Module Summary ###
1. [https://reactnavigation.org/](https://reactnavigation.org/)

## Section 7: App-wide State Management with Redux & Context API ##
### Module Introduction ###
1. Requirement
	1. When we favorite a meal, it shows in the favorites screen
		1. It needs state managed app-wide
2. Topics:
	1. Managing App-Wide State
		1. React Native + React Context Example
		2. React Native + Redux Example
3. Prerequisites:
	1. Redux
	2. Context
4. [Redux vs React's Context API](https://academind.com/tutorials/reactjs-redux-vs-context-api)

### Getting Started with React's Context API ###
1. `store` - app wise state related logic. Convension
2. Code: favorites-context.js

```javascript
import { createContext, useState } from "react";

const FavoritesContext = createContext({
  ids: [],
  addFavorite: (id) => {},
  removeFavorite: (id) => {},
});

function FavoritesContextProvider({ children }) {
  const [favoriteMealIds, setFavoriteMealIds] = useState([]);

  function addFavorite(id) {
    setFavoriteMealIds((currentFavIds) => [...currentFavIds, id]);
  }

  function removeFavorite(id) {
    setFavoriteMealIds((currentFavIds) =>
      currentFavIds.filter((mealId) => mealId !== id)
    );
  }

  const value = { ids: favoriteMealIds, addFavorite, removeFavorite };

  return (
    <FavoritesContext.Provider value={value}>
      {children}
    </FavoritesContext.Provider>
  );
}

export default FavoritesContextProvider;
```

### Managing App-wide State with Context ###
1. Navigation
	1. As long as we are on the same navigation setup, we can navigate to the screen we want (it doesn't have to be in the order of the stack)
		1. We can navigate to details screen from favorites screen

### Using the Constructed Context with useContext ###
### Managing Favorite Meals with the Context API ###
1. Code: FavoritesScreen.js

```javascript
import { StyleSheet, Text, View } from "react-native";
import MealsList from "../components/MealsList/MealsList";
import { useContext } from "react";
import { FavoritesContext } from "../store/context/favorites-context";
import { MEALS } from "../data/dummy-data";

function FavoritesScreen() {
  const favoriteMealsCtx = useContext(FavoritesContext);

  const favoriteMeals = MEALS.filter((meal) =>
    favoriteMealsCtx.ids.includes(meal.id)
  );

  if (favoriteMeals.length === 0) {
    return (
      <View style={styles.rootContainer}>
        <Text style={styles.text}>You have no favorite meals yet.</Text>
      </View>
    );
  }

  return <MealsList items={favoriteMeals} />;
}

const styles = StyleSheet.create({
  rootContainer: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 18,
    fontWeight: "bold",
    color: "white",
  },
});

export default FavoritesScreen;
```

2. Code: MealDetailScreen.js

```javascript
import { useNavigation, useRoute } from "@react-navigation/native";
import { useContext, useLayoutEffect } from "react";
import { Image, ScrollView, StyleSheet, Text, View } from "react-native";
import IconButton from "../components/IconButton";
import List from "../components/MealDetail/List";
import Subtitle from "../components/MealDetail/Subtitle";
import MealDetails from "../components/MealDetails";
import { MEALS } from "../data/dummy-data";
import { FavoritesContext } from "../store/context/favorites-context";

function MealDetailScreen() {
  const favoriteMealsCtx = useContext(FavoritesContext);
  const route = useRoute();
  const navigation = useNavigation();
  const mealId = route.params.mealId;

  const selectedMeal = MEALS.find((meal) => meal.id === mealId);

  const mealIsFavorite = favoriteMealsCtx.ids.includes(mealId);

  function changeFavoriteStatusHandler() {
    if (mealIsFavorite) {
      favoriteMealsCtx.removeFavorite(mealId);
    } else {
      favoriteMealsCtx.addFavorite(mealId);
    }
  }

  useLayoutEffect(() => {
    navigation.setOptions({
      headerRight: () => {
        return (
          <IconButton
            icon={mealIsFavorite ? "star" : "star-outline"}
            color="white"
            onPress={changeFavoriteStatusHandler}
          />
        );
      },
    });
  }, [navigation, changeFavoriteStatusHandler]);

  return (
    <ScrollView style={styles.rootContainer}>
      <Image source={{ uri: selectedMeal.imageUrl }} style={styles.image} />
      <Text style={styles.title}>{selectedMeal.title}</Text>
      <MealDetails
        duration={selectedMeal.duration}
        complexity={selectedMeal.complexity}
        affordability={selectedMeal.affordability}
        textStyle={styles.detailText}
      />
      <View style={styles.listOuterContainer}>
        <View style={styles.listContainer}>
          <Subtitle>Ingredients</Subtitle>
          <List data={selectedMeal.ingredients} />
          <Subtitle>Steps</Subtitle>
          <List data={selectedMeal.steps} />
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  rootContainer: {
    marginBottom: 32,
  },
  image: {
    width: "100%",
    height: 350,
  },
  title: {
    fontWeight: "bold",
    fontSize: 24,
    margin: 8,
    textAlign: "center",
    color: "white",
  },
  detailText: {
    color: "white",
  },
  listOuterContainer: {
    alignItems: "center",
  },
  listContainer: {
    maxWidth: "80%",
  },
});

export default MealDetailScreen;
```

3. Code: MealList.js

```javascript
import { FlatList, StyleSheet, View } from "react-native";
import MealItem from "./MealItem";

function MealsList({ items }) {
  function renderMealItem(itemData) {
    const item = itemData.item;
    const mealItemProps = {
      mealId: item.id,
      title: item.title,
      imageUrl: item.imageUrl,
      affordability: item.affordability,
      complexity: item.complexity,
      duration: item.duration,
    };

    return <MealItem {...mealItemProps} />;
  }

  return (
    <View style={styles.container}>
      <FlatList
        data={items}
        keyExtractor={(item) => item.id}
        renderItem={renderMealItem}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
  },
});

export default MealsList;
```

### Getting Started with Redux & Redux Toolkit ###
1. Redux Toolkit: [https://redux-toolkit.js.org/introduction/getting-started](https://redux-toolkit.js.org/introduction/getting-started)

```bash
npm install @reduxjs/toolkit
npm install react-redux
```

### Working with Redux Slices ###
### Managing Redux State & Dispatching Actions ###
### Using Redux State in Components ###
1. Code: store/redux/store.js

```javascript
import { configureStore } from "@reduxjs/toolkit";
import favoritesReducer from "./favorites";

export const store = configureStore({
  reducer: {
    favoriteMeals: favoritesReducer,
  },
});
```

2. Code: store/redux/favorites.js

```javascript
import { createSlice } from "@reduxjs/toolkit";

const favoritesSlice = createSlice({
  name: "favorites",
  initialState: {
    ids: [],
  },
  reducers: {
    addFavorite: (state, action) => {
      state.ids.push(action.payload.id);
    },
    removeFavorite: (state, action) => {
      state.ids.splice(state.ids.indexOf(action.payload.id), 1);
    },
  },
});

export const addFavorite = favoritesSlice.actions.addFavorite;
export const removeFavorite = favoritesSlice.actions.removeFavorite;
export default favoritesSlice.reducer;
```

3. Code: FavoriteScreen.js

```javascript
import { StyleSheet, Text, View } from "react-native";
import MealsList from "../components/MealsList/MealsList";
// import { useContext } from "react";
// import { FavoritesContext } from "../store/context/favorites-context";
import { useSelector } from "react-redux";
import { MEALS } from "../data/dummy-data";

function FavoritesScreen() {
  // const favoriteMealsCtx = useContext(FavoritesContext);
  const favoriteMealIds = useSelector((state) => state.favoriteMeals.ids); // `favoriteMeals` - object that contains the state

  // const favoriteMeals = MEALS.filter((meal) =>
  //   favoriteMealsCtx.ids.includes(meal.id)
  // );

  const favoriteMeals = MEALS.filter((meal) =>
    favoriteMealIds.includes(meal.id)
  );

  if (favoriteMeals.length === 0) {
    return (
      <View style={styles.rootContainer}>
        <Text style={styles.text}>You have no favorite meals yet.</Text>
      </View>
    );
  }

  return <MealsList items={favoriteMeals} />;
}

const styles = StyleSheet.create({
  rootContainer: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 18,
    fontWeight: "bold",
    color: "white",
  },
});

export default FavoritesScreen;
```

4. Code: MealDetailScreen.js

```javascript
import { useNavigation, useRoute } from "@react-navigation/native";
// import { useContext, useLayoutEffect } from "react";
import { useLayoutEffect } from "react";
import { Image, ScrollView, StyleSheet, Text, View } from "react-native";
import IconButton from "../components/IconButton";
import List from "../components/MealDetail/List";
import Subtitle from "../components/MealDetail/Subtitle";
import MealDetails from "../components/MealDetails";
import { MEALS } from "../data/dummy-data";
import { useDispatch, useSelector } from "react-redux";
import { addFavorite, removeFavorite } from "../store/redux/favorites";
// import { FavoritesContext } from "../store/context/favorites-context";

function MealDetailScreen() {
  // const favoriteMealsCtx = useContext(FavoritesContext);
  const favoriteMealIds = useSelector((state) => state.favoriteMeals.ids); // We use a reducer name and get the items in the state
  const dispatch = useDispatch();

  const route = useRoute();
  const navigation = useNavigation();
  const mealId = route.params.mealId;

  const selectedMeal = MEALS.find((meal) => meal.id === mealId);

  // const mealIsFavorite = favoriteMealsCtx.ids.includes(mealId);
  const mealIsFavorite = favoriteMealIds.includes(mealId);

  function changeFavoriteStatusHandler() {
    if (mealIsFavorite) {
      // favoriteMealsCtx.removeFavorite(mealId);
      dispatch(removeFavorite({ id: mealId })); // an action object is created
    } else {
      // favoriteMealsCtx.addFavorite(mealId);
      dispatch(addFavorite({ id: mealId }));
    }
  }

  useLayoutEffect(() => {
    navigation.setOptions({
      headerRight: () => {
        return (
          <IconButton
            icon={mealIsFavorite ? "star" : "star-outline"}
            color="white"
            onPress={changeFavoriteStatusHandler}
          />
        );
      },
    });
  }, [navigation, changeFavoriteStatusHandler]);

  return (
    <ScrollView style={styles.rootContainer}>
      <Image source={{ uri: selectedMeal.imageUrl }} style={styles.image} />
      <Text style={styles.title}>{selectedMeal.title}</Text>
      <MealDetails
        duration={selectedMeal.duration}
        complexity={selectedMeal.complexity}
        affordability={selectedMeal.affordability}
        textStyle={styles.detailText}
      />
      <View style={styles.listOuterContainer}>
        <View style={styles.listContainer}>
          <Subtitle>Ingredients</Subtitle>
          <List data={selectedMeal.ingredients} />
          <Subtitle>Steps</Subtitle>
          <List data={selectedMeal.steps} />
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  rootContainer: {
    marginBottom: 32,
  },
  image: {
    width: "100%",
    height: 350,
  },
  title: {
    fontWeight: "bold",
    fontSize: 24,
    margin: 8,
    textAlign: "center",
    color: "white",
  },
  detailText: {
    color: "white",
  },
  listOuterContainer: {
    alignItems: "center",
  },
  listContainer: {
    maxWidth: "80%",
  },
});

export default MealDetailScreen;
```

5. Code: App.js

```javascript
import { createStaticNavigation } from "@react-navigation/native";
import { createDrawerNavigator } from "@react-navigation/drawer";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import { StatusBar } from "expo-status-bar";
import { StyleSheet } from "react-native";
import CategoriesScreen from "./screens/CategoriesScreen";
import MealDetailScreen from "./screens/MealDetailScreen";
import MealsOverviewScreen from "./screens/MealsOverviewScreen";
import FavoritesScreen from "./screens/FavoritesScreen";
import { Ionicons } from "@expo/vector-icons";
// import FavoritesContextProvider from "./store/context/favorites-context";
import { Provider } from "react-redux";
import { store } from "./store/redux/store";

const Drawer = createDrawerNavigator({
  screenOptions: {
    headerStyle: {
      backgroundColor: "#351401",
    },
    headerTintColor: "white",
    sceneStyle: {
      backgroundColor: "#3f2f25",
    },
    drawerContentStyle: { backgroundColor: "#351401" },
    drawerInactiveTintColor: "white",
    drawerActiveTintColor: "#351401",
    drawerActiveBackgroundColor: "#e4baa1",
  },
  screens: {
    CategoriesScreen: {
      screen: CategoriesScreen,
      options: {
        title: "All Categories",
        drawerIcon: ({ color, size }) => (
          <Ionicons name="list" color={color} size={size} />
        ),
      },
    },
    Favorites: {
      screen: FavoritesScreen,
      options: {
        title: "Favorites",
        drawerIcon: ({ color, size }) => (
          <Ionicons name="star" color={color} size={size} />
        ),
      },
    },
  },
});

const Stack = createNativeStackNavigator({
  screenOptions: {
    headerStyle: {
      backgroundColor: "#351401",
    },
    headerTintColor: "white",
    contentStyle: {
      backgroundColor: "#3f2f25",
    },
  },
  screens: {
    MealsCategories: {
      screen: Drawer,
      options: {
        title: "About the Meal",
        headerShown: false,
      },
    },
    MealsOverview: {
      screen: MealsOverviewScreen,
      // options: ({ route, navigation }) => {
      //   // Executed whenever screen becomes active
      //   const catId = route.params.categoryId;
      //   return {
      //     title: catId,
      //   };
      // },
    },
    MealDetail: {
      screen: MealDetailScreen,
      options: {
        title: "Meal Detail",
        // headerRight: () => {
        //   return <Button title="Tap me!" onPress={} />;
        // },
        // good if it doesn't need direct interaction with the screen
      },
    },
  },
}); // Object with 2 properties. Every property acts as a component

const Navigation = createStaticNavigation(Stack);

function DrawerNavigator() {}

export default function App() {
  return (
    <>
      <StatusBar style="light" />
      {/* <FavoritesContextProvider> */}
      <Provider store={store}>
        <Navigation />
      </Provider>
      {/* </FavoritesContextProvider> */}
    </>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

### Module Summary ###

## Section 8: Time to Practice - The Expense Tracker App ##
### Module Introduction & What We'll Build ###
1. Expense tracker app - requirements
	1. Register Expenses
	2. Add expeses
	3. View expenses
	4. Delete expenses
	5. Edit expenses
	6. Switch between screens
		1. Recent expenses
		2. ...
2. Topics:
	1. Add Navigation & Screens
	2. Layouts & Styles
	3. Manage Local & App-wide state
		1. Local - specific to components
		2. App-wide state - multiple components share it

### The Starting Setup ###
1. Bottom Tabs navigator:

```bash
npm install @react-navigation/bottom-tabs
```

### Adding Navigation (with React Navigation) & Configuring Navigation ###
### Adding Global Colors & Editing Navigation Configuration ###
### Constructing Key App Components to Display Expenses ###
### Continuing Work on the Expense-Related Components ###
### Adding Dummy Expense Data ###
### Outputting a List of Expenses ###
### Improving App Layout & Styling ###
### Working on Expense List Items ###
### Formatting Dates ###
### Adding a Header Button & Making Expense Items Tappable ###
### Navigating Programmatically Between Screens ###
### Styling The Expense Management Screen ###
### Supporting Different Editing Modes & Using Route Parameters ###
### Adding a "Delete" Button ###
### Adding Custom Buttons ###
### Closing a Modal Programmatically ###
1. App-wide data?
	1. Context API
	2. Redux

### Managing App-wide State with Context ###
### Using Context From Inside Components ###
### Deleting & Updating Expenses ###
### Finishing Touches ###

## Section 9: Handling User Input ##
### Module Introduction ###
1. Topics:
	1. Fetching & Validating User Input
		1. Working with TextInput
		2. Validating User Input & Providing Feedback (in UI)
		3. User Input & Components

### Building a Custom Input Component ###
### Constructing an Overall Form ###
### Configuring the Form Input Elements ###
### Adding Styling ###
### Setting the Form Layout ###
### Handling User Input in a Generic Way ###
### Managing Form State & Submission ###
### Working with Entered Data ###
### Setting & Using Default Values ###
### Adding Validation ###
### Poviding Visual Validation Feedback ###
### Adding Error Styling ###
### Module Summary ###
1. https://github.com/bmutthoju/expense_app.git](https://github.com/bmutthoju/expense_app.git)

## Section 10: Sending Http Requests ##
### Module Introduction ###
1. Topics:
	1. Connecting a Backend & Working with Romote Data (to API or DB)
		1. Setting up a Dummy Backend (Firebase)
		2. Sending Http Requests
			1. CRUD
		3. Handling Loading & Error States
			1. Loading spinner
			2. ...

### Backend Setup (Firebase) ###
1. Firebase: [https://firebase.google.com](https://firebase.google.com)
	1. Login
	2. New project
		1. Name: react-native-course
	3. Continue
	4. Analytics is not required
2. Firebase features
	1. Authentication
	2. Backend
	3. Databases
	4. Functions
3. We will use Realtime Database - has easy to use REST API
	1. Create Database
		1. REST API sits in front of the DB
		2. Start in test mode (no authentication)
		3. URL - We will send requests to it

### Installing Axios ###
1. Axios - makes sending HTTP requests very easy
	1. It is 3rd party API
	2. Installation: `npm i axios`

### Sending POST Http Requests ###
1. Code: http.js

```javascript
import axios from "axios";

export function storeExpense(expenseData) {
  axios.post(
    "https://react-native-course-658e5-default-rtdb.firebaseio.com/expenses.json",
    expenseData
  ); // json - Firebase needs it. It targets specific nodes in DB. Unique ID is generated by Firebase
}
```

### Fetching Backend Data (GET Requests) ###
1. We can continue to use context
	1. Saves extra HTTP requests (because the data that is stored from the app is already available in the context)

### Transforming & Using Fetched Data ###
### Using Response Data from POST Requests ###
### Updating & Deleting Backend Data (UPDATE & DELETE Requests) ###
### Managing the Loading State ###
### Handling Request Errors ###
### Module Summary ###
1. [https://github.com/bmutthoju/expense_app.git](https://github.com/bmutthoju/expense_app.git)

## Section 11: User Authentication ##
### Module Introduction ###
1. Topics:
	1. Login, Signup & Auth State Management
		1. Signing User Up & Logging In
			1. Example app - starting point
				1. We add to it
		2. Managing Authentication Status
			1. Logged in or not
			2. To use it to access protected resources in the backend
		3. Storing Authentication Status on the Device
			1. Retrieved from device
			2. Autologin user if user closes the app and re-opens the app

### Demo App Walkthrough ###
### How Does Authentication Work? ###
1. Backend API
	1. To validate credentials
		1. User data is stored on the database
	2. Credentials are sent to Backend API (Http request)
	3. Validate Credentials & Generate Auth Token
		1. Token - created and signed by backend (just a string)
			1. It cannot be faked
			2. The auth token identifies an authenticated user. It is sent along with future Http requests to protected resources.
			3. The token is required to be sent with the request to resources (endpoiints) that require secure access.
			4. Backend validates the token and grants access to the Http requests
			5. Token is stored on the device (proves the user is logged in)

### Backend Setup ###
1. User details are stored on backend
2. It is used to validate and generate token (for future requests)
3. Firebase:
	1. Authentication
		1. Enable and implemented - (for creation of users)
		2. Get started (same or new firebase project)
			1. Authentication providers (Apple, Facebook, ...)
				1. Email/Password
					1. Email/Password - Enable 
	2. Options
		1. Firebase SDK - convenient
		2. Firebase REST API - (documentation)
			1. Sign up with email / password 
				1. 
			2. Sign in with email / password

### Controlling Signup & Login Screens ###
### Sending Authentication Requests to the Backend ###
1. API_KEY
	1. Project Settings (gear icon)
		1. Web API key
2. Code: util/auth.js

```javascript
import axios from "axios";

const API_KEY = "AIzaSyDHX5BfLjZny6yhw4xrw94qK2KcKxF28xo";

async function createUser(email, password) {
  const response = await axios.post(
    `https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=${API_KEY}`,
    {
      email,
      password,
      returnSecureToken: true,
    }
  );
}
```

### Defining New Users ###
### Logging Users in ###
### Authentication Error Handling ###
### Storing & Managing the User Authentication State (with Context) ###
### Extracting the Authentication Token ###
### Protecting Screens ###
1. Screen protection
	1. Ensures certain screens are not reached if a certain condition is not met
		1. Put the screens in their own navigator and not render screens if a certain condition is not met.

### Adding a Logout Functionality ###
### Accessing Protected Resources ###
1. Token can give access to protected resources on the backend.
	1. Realtime database
		1. New Node
			1. Name: message
			2. Value: Hello World!
2. To fetch the string from welcome string
	1. Rules
		1. `"read": "auth.uid != null"` - `uid` is part of a token
		2. `"write": "auth.id != null"`
	2. We need to attach the token with the request
	
	```
	<url>?auth=<token>
	```

### Storing Auth Tokens on the Device & Logging Users in Automatically ###
1. The state is stored in memory and is lost when app is restarted
	1. Solution: We can store the token in device and automatically login.
		1. React Native `AsyncStorage` - built into RN
		2. `@react-native-async-storage` - documentation ([https://react-native-async-storage.github.io/async-storage/docs/install/](https://react-native-async-storage.github.io/async-storage/docs/install/))
			1. It stores data differently on Android and iOS.
			2. Does heavy lifting.
			3. Simple to use.
2. Installation:

```
npm install @react-native-async-storage/async-storage
```

### A Note About Token Expiration ###
1. A token expires if configured for it
	1. Firebase - 1h timer is set on each token
		1. If a token is sent to Firebase after 1 hour to access a protected resource, it will not work
			1. Solution: Do one of the two things
				1. **Automatically log the user out**
					1. After 1 hour (to avoid that the user things he or she is logged in)
					2. Can be achieved with the help of `setTimeout()`
						1. Set a timer which runs in the background and logs the user out after 1h.
						2. If we logged a user in because token was stored on device, remaining duration is likely less than 1 hour.
							1. We might need to calculate the remaining duration by subtracting current time from expiration time to determine when the token was first recived.
								1. Hence, the expiration time must also be derived and stored whenever a token is received.
				2. **Refresh the token**
					1. Get a new auth token
					2. Can be done using auth API endpoint provided by Firebase.
						1. [https://firebase.google.com/docs/reference/rest/auth#section-refresh-token](https://firebase.google.com/docs/reference/rest/auth#section-refresh-token)
					3. When we get an auth token, we also get a refresh token
						1. `refreshToken` field in the response.
							1. This can be sent to refresh token API: [https://firebase.google.com/docs/reference/rest/auth#section-refresh-token](https://firebase.google.com/docs/reference/rest/auth#section-refresh-token)
							2. The token needs to be stored in Context and on the device.
							3. Set a timer to refresh the token periodically (or refresh it whenever it expired)
				3. Firebase SDK:
					1. Handles token management (and refreshing the token) for us

### Module Summary ###
1. Firebase SDK
	1. Makes things simpler
		1. Many things are managed behind the scenes

## Section 12: Using Native Device Features (Camera, Location & More) ##
### Module Introduction ###
1. Using Native Device Features
	1. Using the Camera, User Location & Device Storage
		1. Simple to use in RN apps
	2. Using the Device Camera
	3. User Location & Maps
		1. Google Maps
	4. Storage Data on the Device
		1. More complex data
2. Favorite places app
	1. New places
	2. Take picture
	3. We can attach location
		1. Get current location
		2. Picking on a map
	4. Storage on device

### Adding a "Favorite Places" List ###
1. New expo project

### Editing the Favorite Place Items ###
1. `npm i @react-navigation/native @react-navigation/native-stack`

### Adding an "Add Place" Screen + Navigation ###
### Adding a Header Button ###
### Global Colors & Styling ###
### Getting Started with a Custom Form ###
### Adding & Configuring the Camera Package (for Native Camera Access) ###
1. How to use device camera
	1. Camera - Expo Documentation (search for expo camera)
		1. Other features
			1. Expo storage
			2. Expo location
			3. ...
	2. Expo Camera
		1. Allows us to customize the camera screen
			1. Auto focus
			2. Zoom
			3. Own camera based UI
		2. Go through the documentation
2. Another package (simpler to use)
	1. `ImagePicker` - Allows selecting a photo or open on-device camera
		1. `expo install expo-image-picker`
	2. We need to set permissions properly
		1. Native features want permission from user
		2. Need to register permissions the app will use ahead of time
			1. Expo makes registering permissions easy
				1. `app.json` - add plugins entry
				
				```json
				{
				  "expo": {
					"plugins": [
					  [
						"expo-image-picker",
						{
						  "photosPermission": "The app accesses your photos to let you share them with your friends."
						}
					  ]
					]
				  }
				}
				```

### Taking Photos on Android ###
1. Code: ImagePicker.js

```javascript
import { Button, View } from "react-native";
import { launchCameraAsync } from "expo-image-picker";

function ImagePicker() {
  async function takeImageHandler() {
    const image = await launchCameraAsync({
      allowsEditing: true,
      aspect: [16, 9],
      quality: 0.5, // we don't want large images
    }); // It waits for user to take a photo. Check the docs
    console.log(image);
  }

  return (
    <View>
      <View></View>
      <Button title="Take Image" onPress={takeImageHandler} />
    </View>
  );
}

export default ImagePicker;
```

### Taking Photos on iOS + Managing Permissions ###
1. Open the app in real iOS device
2. Code: ImagePicker.js

```javascript
import { Alert, Button, View } from "react-native";
import {
  launchCameraAsync,
  useCameraPermissions,
  PermissionStatus,
} from "expo-image-picker";

function ImagePicker() {
  const [cameraPermissionInformation, requestPermission] =
    useCameraPermissions();

  async function verifyPermissions() {
    if (cameraPermissionInformation.status === PermissionStatus.UNDETERMINED) {
      const permissionResponse = await requestPermission();
      return permissionResponse.granted; // true or false
    }

    if (cameraPermissionInformation.status === PermissionStatus.DENIED) {
      Alert.alert(
        "Insufficient Permissions!",
        "You need to grant camera permissions to use this app."
      );
      return false;
    }

    return true;
  }

  async function takeImageHandler() {
    const hasPermission = await verifyPermissions();

    if (!hasPermission) {
      return;
    }

    const image = await launchCameraAsync({
      allowsEditing: true,
      aspect: [16, 9],
      quality: 0.5, // we don't want large images
    }); // It waits for user to take a photo. Check the docs
    console.log(image);
  }

  return (
    <View>
      <View></View>
      <Button title="Take Image" onPress={takeImageHandler} />
    </View>
  );
}

export default ImagePicker;
```

### Showing an Image Preview ###
### Constructing a Custom Button ###
### Getting Started with the Location Picker ###
### Locating Users ###
1. Search `expo location`
	1. `npx expo i expo-location`
2. Permissions
	1. Feature: Can get location whilst running in the background
	2. Takes care of permissions automatically
	3. app.json
	
	```json
	{
	  "expo": {
		"plugins": [
		  [
			"expo-location",
			{
			  "locationAlwaysAndWhenInUsePermission": "Allow $(PRODUCT_NAME) to use your location."
			}
		  ]
		]
	  }
	}
	```
	
	4. Permissions are required for both Android and iOS.

### Adding a Location Preview Map ###
1. search: google maps static api
	1. Need account + credit card
		1. APIs
			1. Static Maps API
		2. Credentials
			1. API key creation
				1. Can be restricted

### Adding an Interactive Map (Google Maps & Apple Maps) ###
1. Expo: `MapView` package
	1. Helps rendering maps
		1. Apple Maps
		2. Google Maps
	2. It can be used in non-Expo apps, too
	3. Installation: `npx expo install react-native-maps`
	4. Go through the documentation
2. Configuration options
	1. When publishing to app stores

### Allowing Map Interaction & Adding Markers ###
### Confirming Picked Locations ###
### Previewing Picked Locations ###
1. When we go back to another screen (using stack navigator). The screen and child are not re-created. The rest of the screens on the stack are preserved.
	1. `useEffect` doesn't run again
		1. Solution: `useIsFocused()`
			1. This hook returns `true` if the screen is focused, `false` otherwise

### Adding a Form Submit Button ###
### Managing Location & Image State in the Form ###
### Converting Picked Locations to Human-Readable Addresses ###
1. Geocoding API - Google
	1. Addresses to coordinates
	2. Coordinates to Addresses (reverse geocoding)
	3. Enable Geocoding API
		1. Re-use the same API key
			1. Credentials
				1. API Key

### Passing Entered Data to the "AllPlaces" Screen ###
### Outputting a List of Places ###
### Styling Place Items ###
### SQLite: Getting Started & Initialization ###
1. Native device storage
	1. Usually we send the data to the backend to store on the database
		1. Alternative - We can store database that is on the device
			1. Use-case: It can be personal
				1. Solution: expo SQLite
					1. SQLite - SQL DB that can run on Android and iOS.
					2. Go through the documentation
2. Installation:
	1. `npx expo install expo-sqlite`

### Preparing Code to Insert Data into the SQLite Database ###
### Inserting Places into the Database ###
### Fetching Places from the Database ###
### Adding the Place Details Screen ###
### Fetching Place Detail Data from the Database ###
### Showing a Readonly Map ###
### Module Summary ###
1. Explore expo packages
	1. Maps
	2. Date pickers
	3. Payments
	4. ...
2. [https://github.com/bmutthoju/native__features_app/tree/main](https://github.com/bmutthoju/native__features_app/tree/main)

## Section 13: Building React Native Apps Without Expo ##
### Module Introduction ###
1. React Native Without Expo
	1. How Does Expo Work?
		1. What it did for us
		2. Switching away from expo
			1. Vanilla RN project
	2. Building a "Vanilla" React Native Project
	3. Advantags & Disadvantages
		1. Which approach is best for future projects

### How Exactly Does Expo Work? ###
1. Expo
	1. Expo Go App (shared native runtime)
		1. Installs on emulator or device
	2. Your code is loaded by Expo into the Expo Go app and executed
		1. No installation & installation & publishing
		2. Helps preview code
	3. Disadvantages
		1. You don't build real app executables during development. (not standalone apps installed on emulators or devices)
			1. Instead, your source code is injected into the Expo Go client app (and executed there)
	4. We can still build & publish standalone apps though!
		1. As a standalone app
			1. Users wont need Expo Go app
	5. You can still build standalone apps (independent of Expo Go!)
		1. Use EAS Build Service
			1. During Development
				1. Move fast with Expo Go app - instant preview
				2. Shared runtime (expo go) loads your code and reflects changes instantly
			2. For Production
				1. Build lean, independent standalone apps that don't need Expo Go
				2. Use EAS (cloud service) to build for all platforms (even on Windows machine)

### Expo Alternatives ###
1. Expo Managed Workflow
	1. We used managed workflow template
		1. Has configuration
			1. Made using native features easier
				1. Takes control away
		2. Advantages:
			1. Easy to set up & work with
			2. Quick & frictionless development
			3. No or very little configuration required (especially 3rd party packages)
			4. You can build (cross-platform) standalone apps
				1. No restriction
2. Expo "Bare Workflow" - more control
	1. To write own native code (in Swift, ...) and mix with RN code, we can use this workflow
		1. Still expo - less expo features
	2. Relatively easy to set up & work with
	3. Convenient development
		1. No expo go app
			1. If custom code is mixed
	4. Some configuration required
		1. More than expo managed
	5. You can build (cross-platform) standalone apps
3. React Native CLI - Provided by RN team
	1. More complex setup
	2. Convenient development 
	3. Can require more configuration effort (for 3rd party packages)
		1. More control
		2. 3rd party cloud providers for building platform specific builds
	4. Standalone apps are built locally
		1. Cannot build iOS apps on Windows machine (restricted by apple)

### Setting Up Our System ###
1. Expo bare workflow - documentation
	1. We can also use Expo Go app - there are restrictions
		1. If native code, expo go doesn't support (hence may not be able to support it)
			1. Solution: iOS or Android needs building standalone apps on local machine and preview on emulator or simulator
				1. [reactnative.dev](reactnative.dev)
					1. Setting up the development environment
						1. React Native Cli Quickstart
					2. Configuration is required for Android Studio (the first time at-least)
					3. Additional steps and installations are required

### Using Expo's Bare Workflow ###
1. New project: `expo init --npm`
	1. Name: RNCourseBare
	2. template: minimal
	3. Open in VS Code
		1. `android`
		2. `ios`
			1. RNCourseBare
				1. Info.plist - setting permissions
		3. `index.js` - registers `App` as root
		4. `app.json` - less shared management (they have to be done in individual folders)
	4. Some bare projects are not supported by expo go
		1. Solution: `package.json` has two scripts for Android and iOS.
		
		```
		npm run android
		```
		
		2. Installed automatically on the emulator
		3. To install a standalone application on the device, we need to connect the device.
		4. Initial build takes more time, but once it is built for development, there is internal code to receive updates quicker. Subsequent code changes will reflect quicker.
		5. We have to run the same command to install on a real device but when the emulator is not running.
	5. If a change is made, the change is automatically pushed to emulator (or real device)
		1. There is an internal process connected to our machine that will receive those changes (pushed to the process)
	6. iOS:
	
	```
	npm run ios # needs mac and xcode
	```
	
2. Fixing issues with Android
	1. `android/local.properties`
	
	```
	sdk.dir=C\:\\Users\\suppo\\AppData\\Local\\Android\\Sdk
	```

### Using Native Device Features with the Bare Workflow ###
1. expo location - documentation
	1. We can use the same but needs extra set up
		1. bare React Native App [https://github.com/expo/expo/tree/main/packages/expo-location](https://github.com/expo/expo/tree/main/packages/expo-location)
			1. Configuration steps
	2. Usage is the same as the managed workflow
	3. App must be rebuilt for every package added and configuration changed
	4. Once we ran `npm run android` and `npm run ios`, we can close one of them because one process watches both.

### Ejecting to the Bare Workflow ###
1. We want to switch to bare workflow from managed workflow
	1. Solution: Eject from managed workflow to bare workflow
2. `expo eject`
	1. We cannot go back. Hence we need to push to Github before doing this.
	2. Android package name: `com.academind.rncourse` (reverse domain name + project name) - identifier - important for app stores
	3. iOS package ame: same
	4. Generates `android` and `ios` folders + other adjustments
		1. We can run `npm run android` and `npm run ios`
		2. Installs standalone app
3. Different workflows: expo documentation
	1. Use API reference pages

### Constructing Projects with the React Native CLI (no Expo) ###
1. RN apps without expo
	1. RN documentation
		1. Setting p the development environment
			1. Go through all the steps
				1. `npx react-native-init RNNoExpo`
					1. Update:
					
					```
					npm uninstall -g react-native-cli @react-native-community/cli
					
					npx @react-native-community/cli@latest init RNNoExpo
					```
					
				1. Alternative:
				
				```
				npm i -g react-native-cli
				
				react-native init RNNoExpo
				```
				
2. Structure
	1. `App.js`
	2. `index.js` - code is slightly different
	3. `app.json` - even less options
	4. `android`
		1. Config
	5. `ios`
		1. Config
3. Differences
	1. External packages - more work
	2. Configuration - more work
4. Running:

```
npm run android

npm run ios
```

5. A process runs in the background and updates the standalone app
6. Open the app explicitly on the device if it didn't open automatically
7. Disadvantages:
	1. Cannot use expo go
	2. Cannot use expo packages

### Non-Expo Apps & Native Device Features ###
1. We can turn RN project into bare expo project (to use expo packages)
	1. expo bare workflow
		1. Add expo to project
		
		```
		npx install-expo-modules # core expo modules
		```
		
2. Other 3rd party packages
	1. Location: Search React Native Location
		1. Community packages - `react-native-geolocation-service`
			1. Install
			2. Setup steps
				1. A few steps to go through
		2. Go through examples to know how to use the package

### Module Summary ###

## Section 14: Publishing React Native Apps ##
### Module Introduction ###
1. Publishing React Native Apps
	1. From Development to Production
		1. Monetizing
		2. For other users
		3. Steps:
			1. Configuring for production
				1. Config settings
			2. Icons & Splash Screens (loading screens)
			3. Build process in action
				1. Expo managed app
				2. Pure RN app (no expo)

### Publishing Apps: An Overview ###
1. Publishing
	1. Putting into Google Play Store or Apple App Store
		1. With Expo (Managed or Bare Workflow)
			1. Configure the Project
				1. Settings
					1. Keys settings
						1. Adding icons
						2. ...
			2. Build App Binaries with Expo's Cloud Service
				1. For free
					1. Outsource build process - on cloud
				2. Advantage: No local resources used & you can build for all target platforms
					1. Mac Book is not required
					2. They will build both Android and iOS apps for us
			3. Submit to App stores
				1. Manually 
				2. Using expo - seamless
		2. Without Expo
			1. Configure the project
				1. Build App binaries locally (on our machine)
					1. Alternatives - Other 3rd party cloud services
			2. Submit to App Stores
				1. Manually

### Key Configuration Items & Considerations ###
1. Configuring for Production (to tweak before building the app)
	1. Permissions
		1. Device features
			1. Config must be setup
				1. Android: Control permissions requested & shown in app store
				2. iOS: Define permission request text snippets
	2. App Name & Identifier (unique)
		1. Set a visible app name, an app version and a unique app identiier (ID)
			1. Updating version - to show users that version changed
	3. Environment variables
		1. Store app-wide variables securely (e.g. API keys)
	4. Icons & Splash Screen (loading screen)
		1. Configure and generate fitting icons and loading screens

### Configuring App Names & Versions ###
1. meals_app
	1. We build with expo
		1. Expo Application Services - documentation (EAS)
			1. go through all the documents and instructions in detail (we can do a lot with EAS)
			2. We can build and submit to app store (seamless and easy process)
	2. Configuration
		1. app.json (check all the options in API Reference)
			1. name: (name of standalone app)
			2. slug: to publish in other expo go apps (not a standalone app)
			3. version: (versioning scheme)
				1. User facing version (users will see this version)
				2. `android.versionCode` - internal version
					1. Used by app-store to tell different versions apart (version as seen by app-store)
				3. `ios.buildNumber` - internal version
			4. Go through documentation for publishing

### A Quick Note About Environment Variables ###
1. EAS documentation
	1. Environment variables and secrets
		1. Global variables set at the time of building the apps or during development
		2. Secrets - Expo & EAS help us manage them
	2. Official documentation has the information

### Adding Icons & A Splash Screen ###
1. We can replace icons with same dimensions
	1. Expo icons splash
		1. How icons and splash screens can be added & dimensions
	2. Update paths in `app.json`
		1. Cloud produces different icons for different dimensions
			1. Expo takes input icons and generates different size icons

### Building Expo Apps with EAS ###
1. EAS documentation - Expo
	1. Expo user account
		1. [https://expo.dev](https://expo.dev)
	2. Install expo-cli
	
	```
	npm install --global eas-cli
	```
	
	3. Login
	
	```
	eas login
	```
	
	4. Configure project:
	
	```
	eas build:configure # adds eas.json - extra config for build process
	
	# All
	```
	
	5. Installables (to install on our devices)
		1. eas.json
		
		```
		    "preview": {
			  "android": {
				"buildType": "apk"
			  },
			  "distribution": "internal"
			},
		```
		
		2. Building:
		
		```
		eas build --platform android --profile preview
		```
		
			1. application id: com.academind.myrecipebook (uniquely identifiable)
				1. Gets added to app.json
				
				```
				"package": "com.academind.myrecipebook"
				```
				
			2. Android keystore: for signing the app and securing the app (to ensure that I am the only one publishing it and publishing updates to it)
				1. `yes` - expo manages signing on their servers
			3. EAS paid service - gives priority support
			4. A link is published to be used to download the apk for installation
				1. We can download the artifact from expo
					1. Fix if build fails:
					
					```
					npm i expo-splash-screen
					```
					
			5. Download the apk
			6. Drag and drop the apk file onto the device
			7. Scan QR code to install app on real device
			8. `apk` is not optimized for production use
				1. use `production` profile
					1. Gives `aab` file - can upload to Google playstore
				2. Default profile is `production`
			9. Submitting to playstore or app-store
		2. Submitting using EAS to store
			1. Using official documentation

### EAS for iOS (even on Windows Devices) ###
1. EAS iOS Build
	1. eas.json
	
	```
	"preview": {
		"ios": {
			"simulator": true
		}
		...
	}
	```
	
2. Building:

```
eas build --platform ios --profile preview
```

	1. iOS bundle identifier: `com.academind.myrecipebook`
	2. More needs to be done for production
	3. Gives a link
		1. A zipped file can be downloaded
			1. Extract it
			2. Execute on a simulator - Works on Mac OS
	4. Drag and drop into simulator
3. Distribution: Production build
	1. Apple developer program membership
	2. Apple account
		1. Appled Developer Program - $99 USD
	3. Generate certificates
		1. Needed as part of the build process
			1. Can be done from inside Apple Developer web page
	4. Production build:
	
	```
	eas build --platform ios
	```
	
		1. log in to Apple account
			1. They will set up certificates and documents (needed from Apple's side)
		2. Manual set up of certificates and profiles
			1. Distribution Certificate
				1. Log into Apple account
					1. Needs payment
				2. Certificates, Identifiers & Profiles
					1. iOS Distribution (App Store and Ad hoc)
					2. Continue
						1. Certificate Signing Request file
							1. Produce a file
						2. Upload
						3. Continue 
						4. Download the certificate
							1. Don't store it as part of store control
								1. `certs/ios` (add it to .gitignore - `certs`)
			2. Provisioning profile
				1. Certificates, Identifiers & Profiles
					1. Profiles
						1. Provisioning profile
							1. App Store
								1. App ID: 
									1. Back
										1. App Store Connect
											1. Go to App STore Connect (new apps are created)
												1. My Apps
												2. Add a new app
													1. Name: My Recipe Book
													2. iOS
													3. English
													4. Bundle ID: Certificates page:
														1. register an app id:
															1. `app.js` - `bundleIdentifier`
													5. Enable push notifications
													6. Description: Recepe book app
													7. Register
														1. Check more boxes if more features are required
												3. Add a new app
													1. Pick the bundle id
													2. full access
													3. Name: RN Recipe Book
													4. SKU - recipebook (internal id)
													5. Create
						2. App Store
							1. App ID: Recipe book app
							2. Continue
							3. Name
							4. Assign it to distribution
							5. Provisioning Profile Name
								1. RN Recipe Book
							6. Generate
							7. Download
							8. Drag it to `certs/ios`
						3. Make EAS aware of the files
							1. Documentation - copy in `production` profile
								1. Path: `certs/ios/...`
								2. provisioning profile name needs to be changed
							2. Execute certificate
								1. Add to keychain
									1. Add
								2. Search for certificate
									1. Export it as a p12 file
									2. Add it to `certs/ios`
									3. Assign a password (strong password)
							3. Copy the name in `eas.json`
							4. Copy the password in `eas.json`
						4. The above config should go to `credentials.json` (and not eas.json)
						
						```
						{
							"ios": {
								"provisioningProfilePath": "certs/ios/RN_Recipe_Book.mobileprovision",
								"distributionCertificate": {
									"path": "certs/ios/Certificates.p12",
									"password": "testers"
								}
							}
						}
						```
						
						5. `eas build --platform ios`
							1. Login
								1. Forcing eas to use local credentials
									1. `eas.json`
									
									```
									"production: {
										"credentialsSource": "local"
									}
									```
									
							2. Run: `eas build --platfor ios`
								1. We can enable push notifications
				3. Submitting using EAS - official docs
4. Alternative - EAS will do it for us

### Building for iOS Without Expo ###
1. New app:
	1. Official RN Docs
		1. Guides
			1. Running on Device
				1. Android
				2. iOS
					1. Apple developer account
	2. ios:
		1. open in xcode
			1. ID: inverse url + app name
		2. verion numbers 
		3. Build number
		4. Display name
		5. Automatically manage signing
		6. Team
			1. Apple developer account (required for autosigning)
		7. We need to setup icons on our own
			1. Assets catalog
				1. Provide icons in different sizes
					1. Drag and drop zip files
		8. Configure launch screen
			1. Lanch screen zip file
			2. Change text
			3. ...
		9. Choose a simulator
		10. Play
			1. Builds and runs on simulator
		11. Go through official docs in RN documentation

### Building for Android Without Expo ###
1. RN official docs
	1. Publishing to Google play store
		1. Windows: `keytool` - keystore is needed for signing app and updates to app

### Configuring Android Apps ###
1. AndroidManifest.xml - Used to manage aspects of Android app if adding native modules to non-Expo apps
	1. App name - as it appears on the home screen: [https://stackoverflow.com/questions/5443304/how-to-change-an-android-apps-name](https://stackoverflow.com/questions/5443304/how-to-change-an-android-apps-name)
	2. Bundle identifier & package name - [https://developer.android.com/studio/build/application-id](https://developer.android.com/studio/build/application-id)
	3. Permissions of the app: [https://developer.android.com/guide/topics/manifest/manifest-intro#perms](https://developer.android.com/guide/topics/manifest/manifest-intro#perms)
	4. App version: In `build.gradle` file - [https://developer.android.com/studio/publish/versioning](https://developer.android.com/studio/publish/versioning)

## Section 15: Push Notifications ##
### Module Introduction ###
1. Push Notifications
	1. Sending & Responding to Push Notifications
		1. Working with Local Notifications
		2. Understanding Push Notifications
			1. How they work and are added
		3. Example: Send + Handle Push Notifications

### What are (Local) Notifications? ###
1. Related to push notifications
	1. Local notifications: Notifications that are triggered by the installed app, for local device (pushed by the same app installed on the device)
		1. Not sent to any other users or devices!
		2. Notificiations are scheduled, delivered and handled on the same device (no server involved)
			1. Why?
				1. Reminder
				2. Alarm Clock
				3. Todo

### Adding the Expo Notification Package ###
1. New project
2. Expo Notifications package - documentation
	1. Makes handling notifications simple
		1. For both local and push notifications
	2. Many details can be configured
	3. We can test on emulators and real devices - local notifications
	4. We cannot test on emulators and simulators (we need real devices) - push notifications
3. Installation: `npx expo install expo-notifications`
4. Configuration:
	1. `"icon"` - Android only
	2. `"color"` - Android only
	3. `"sounds"`
5. Expo Go - no extra setup steps for push notifications
	1. Extra steps are required for standalone apps
6. Android: RECEIVE_BOOT_COMPLETED - permission set automatically
	1. Allows an application to receive the `intent.ACTION_BOOT_COMPLETED` that is broadcast after the system finishes booting.
7. iOS: Documentation 
	1. Fetch permissions in code

### Scheduling Notifications ###
### Configuring Scheduled Notifications ###
1. `scheduleNotificationAsync()` - to schedule local notifications
	1. Other properties
		1. `content`: [https://docs.expo.dev/versions/latest/sdk/notifications/#notificationcontentinput](https://docs.expo.dev/versions/latest/sdk/notifications/#notificationcontentinput)
		2. `trigger`: [https://docs.expo.dev/versions/latest/sdk/notifications/#notificationtriggerinput](https://docs.expo.dev/versions/latest/sdk/notifications/#notificationtriggerinput)
			1. Trigger times:
				1. Seconds
				2. Specific date
				3. Daily time
				4. Weekly
				5. Yearly
				6. Specific date (iOS only)

### Handling Incoming Notifications ###
### Local Notifications - Permissions ###
1. To ensure notifications work correctly, we need to ask for permissions.
	1. Android: No changes
	2. iOS: `getPermissionsAsync()` method ([https://docs.expo.dev/versions/latest/sdk/notifications/#getpermissionsasync-promisenotificationpermissionsstatus](https://docs.expo.dev/versions/latest/sdk/notifications/#getpermissionsasync-promisenotificationpermissionsstatus))
		1. `expo-notifications` - returns the current permission status
		2. [To request permissions](https://docs.expo.dev/versions/latest/sdk/notifications/#requestpermissionsasyncrequest-notificationpermissionsrequest-promisenotificationpermissionsstatus)
	3. [Full code example](https://docs.expo.dev/push-notifications/push-notifications-setup/)

### Reacting to Incoming Notifications ###
1. If we tap on notifications - nothing happens
	1. If we want to execute some code if
		1. Notification was received OR
		2. Notification was tapped
	2. We need to add event handlers to handle user taps 
2. Data that we can get out of notification
	1. `request.conent.data` node (it was set with the notification)

### Reacting to User Interaction with Incoming Notifications ###
1. `actionIdentifier` - extra metadata

### Understanding Push Notifications ###
1. We want to talk to other instances of apps used by other users
	1. Push notifications - important messages to other devices to notify users about something
		1. It could be a marketing message
2. Userstanding Push Notifications
	1. Your app - Data migt be sent to a custom backend (e.g. to store it in a database)
		1. This is not required to integrate push notification though! -> Your Backend
			1. Event on app - (chat app)
		2. Some event can occur on the backend
			1. Sending marketing messages say
		3. Sending notification to your app on other devices (one or more)
			1. Example: chat message can be sent to a friend's device as a push notification
				1. Can be sent to multiple friends on a chat group
		4. Push notification is sending a notification to a device different from the origin device.
		5. Push notification from backend to other devices
	2. It is not possible to directly send push notification from device to device
		1. Solution: Google & Apple force us to use backend provider to send push notifications to other devices (push notification servers)
			1. Push notifications are also provided by Expo (under the hood it is Apple and Google)
				1. We can use one server for Android and iOS
					1. We need to send HTTP request to push notification server which delivers to the other device(s)
	3. Options:
		1. Option 1: Custom backend code sends request to push notification server (an even on backend)
		2. Option 2: App sends request to push notification server
	4. Push Notification Server (e.g. provided by Expo)
		1. Sends push notification to registered devices (takes care of delivering messages to other devices)

### Push Notifications Setup ###
1. Official documentation
	1. Expo push notifications
		1. How to send and handle push notifications
			1. Examples
			2. Instructions (from backend code)
			3. API endpoint to send requests to deliver push notifications to other devices
2. Setup
	1. `expo-notifications` package
	2. Request permissions (ios especially)
	3. Expo push token
		1. A string unique to every device (address to send push notifications to)
	4. A real device is required for testing pushing notifications

### Using the Push Token ###
1. Permissions
	1. Code that asks user for permissions (if no expo go - standalone application - for production)

### Sending Push Notifications ###
1. Service for testing push notifications (expo docs)
	1. Push notification tool ([expo.dev/notifications](expo.dev/notifications))
		1. Token
		2. Body
		3. Send a Notification
2. We usually store push token into a database
	1. We can fetch it from DB and send push notifications

### Module Summary ###

## Section 16: Course Roundup ##
### Course Roundup ###
1. Use it in everyday projects

## Section 17: Bonus: JavaScript Refresher ##
### Module Introduction ###
### JavaScript - A Summary ###
### Project Setup ###
### Core Syntax Refresher ###
### let & const ###
### Arrow Functions ###
### Objects: Properties & Methods ###
### Arrays & Array Methods ###
### Arrays, Objects & Reference Types ###
### Spread Operator & Rest Parameters ###
### Destructuring ###
### Async Code & Promises ###
### Wrap Up ###
### Module Resources ###

## Section 18: Bonus: React.js Refresher ##
### Module Introduction ###
### What is React ###
### A Starting Project ###
### Understanding JSX ###
### Understanding Components ###
### Working with Multiple Components ###
### Working with Props ###
### Rendering Lists of Data ###
### Handling Events ###
### Parent-Child Communication ###
### Managing State ###
### More on State ###
### User Input & Two-Way Binding ###
### Wrap Up ###
### Module Resources ###

## Bonus ##
### Legacy Course Content ###
### This Course Was Updated | Update Information ###
### Course Update Information & FAQs ###
### Bonus: More Content! ###
1. [https://academind.com/courses](https://academind.com/courses) - Other courses
2. [Newsletter](https://academind.com/)
3. [Additional Tutorials](http://youtube.com/c/academind)
4. [https://twitter.com/maxedapps](https://twitter.com/maxedapps)
5. [https://twitter.com/academind_real](https://twitter.com/academind_real)