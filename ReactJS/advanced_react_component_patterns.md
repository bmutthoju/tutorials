# Advanced Ract Component Patterns #
## Introduction ##
### Getting Started with Advanced Patterns ###
### (Bonus) PDF: Advanced React Patterns in the Real World: Lessons from OS Libraries ###
1. [https://www.udemy.com/course/the-complete-guide-to-advanced-react-patterns/learn/lecture/19271202#overview](https://www.udemy.com/course/the-complete-guide-to-advanced-react-patterns/learn/lecture/19271202#overview)

### Why Advanced React Patterns ###
1. Design Patterns?
	1. Time-tested solutions to recurring design problems

### Design Patterns and React ###
1. Example task: To build a component library to be used by an entire company
	1. The components must satisfy:
		1. Reusability (across scenarios and use-cases)
		2. Style extensibility (or extensibility in general)
		3. Easy API
	2. It is faced by any engineer who is building re-usable components
2. Why advanced React patterns?
	1. Solve issues related to building reusable components using proven solutions
	2. Development of highly cohesive components with minimal coupling
	3. Better ways to share logic between components

### The Medium Clap ###
1. Medium's Clap Component
	1. Learning practically

## The Medium Clap: Real-World Component for Studying Advanced React... ##
### Why build the medium clap? ###
1. Medium clap component poses real-world challenges that are befitting to discuss teh advanced react patterns.
	1. Helps solidify many React principles (animations and working with imperative APIs) while building out the Medium clap component.
	2. Helps introduce each advanced React pattern.
2. Tips:
	1. Code along
		1. Active learning - more effective

### Setting up your local environment ###
1. [https://github.com/ohansemmanuel/advanced-react-patterns-ultrasimplified/tree/clean-slate](https://github.com/ohansemmanuel/advanced-react-patterns-ultrasimplified/tree/clean-slate)

### How the demo showcase works ###
1. `showcase/src/patterns/01.js` 

```javascript
import React from "react";

const Clap = () => {
  return <h1>Hello Clap Component</h1>;
};

export default Clap;
```

### Building and styling the medium clap ###
1. States:
	1. The default state of the component - unclicked.
	2. The clap count & burst shown
	3. The clap total count shown
2. Components:

```
<button>
  <ClapIcon />
  <ClapCount />
  <CountTotal />
</button>
```

3. Code:

```javascript
import React from "react";
import styles from "./index.css";

const MediumClap = () => {
  return (
    <button className={styles.clap}>
      <ClapIcon />
      <ClapCount />
      <CountTotal />
    </button>
  );
};

/**
 * subcomponents
 */
const ClapIcon = () => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={styles.icon}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count }) => {
  return <span className={styles.count}>+ {count}</span>;
};

const CountTotal = ({ countTotal }) => {
  return <span className={styles.total}>{countTotal}</span>;
};

export default MediumClap;
```

### Handling user interactivity ###
### Higher order components recap ###
1. It is a technique
	1. Why HOC?
		1. How was it done before?
	2. What is HOC?
		1. It is a function that takes a component and returns another component
			1. The component returned will have the original component's functionality and additional functionality
			2. Example: Logic - HOC -> Logic + Animation

### Beginning to animate the clap ###
1. Library: `mojs` - for learning purposes
	1. Animation timeline
2. `cd showcase`
	1. `yarn add mo-js`

### Constructing and updating the animation timeline ###
### Resolving wrong animated scale ###
1. Code:

```javascript
    componentDidMount() {
      const scaleButton = new mojs.Html({
        el: "#clap",
        duration: 300,
        scale: { 1.3: 1 },
        easing: mojs.easing.ease.out,
      });

      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";

      const newAnimationTimeline = this.animationTimeline.add([scaleButton]);
      this.setState({ animationTimeline: newAnimationTimeline });
    }
```

### Animating the clap count ###
1. Code:

```javascript
      const countAnimation = new mojs.Html({
        el: "#clapCount",
        opacity: { 0: 1 },
        y: { 0: -30 },
        duration: tlDuration,
      }).then({
        opacity: { 1: 0 },
        y: -80,
        delay: tlDuration / 2,
      });
```

### Animating the total count ###
### Constructing animated bursts! ###
1. Code:

```javascript
import React from "react";
import styles from "./index.css";
import mojs from "mo-js";

const initialState = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Higher Order Component
 */
const withClapAnimation = (WrappedComponent) => {
  class WithClapAnimation extends React.Component {
    animationTimeline = new mojs.Timeline();
    state = {
      animationTimeline: this.animationTimeline,
    };

    componentDidMount() {
      const tlDuration = 300;
      const scaleButton = new mojs.Html({
        el: "#clap",
        duration: tlDuration,
        scale: { 1.3: 1 },
        easing: mojs.easing.ease.out,
      });

      const countAnimation = new mojs.Html({
        el: "#clapCount",
        opacity: { 0: 1 },
        y: { 0: -30 },
        duration: tlDuration,
      }).then({
        opacity: { 1: 0 },
        y: -80,
        delay: tlDuration / 2,
      });

      const triangleBurst = new mojs.Burst({
        parent: "#clap",
        radius: { 50: 95 },
        count: 5,
        angle: 30,
        children: {
          shape: "polygon",
          radius: { 6: 0 },
          stroke: "rgba(211,54,0,0.5)",
          strokeWidth: 2,
          angle: 210,
          delay: 30,
          speed: 0.2,
          easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
          duration: tlDuration,
        },
      });

      const circleBurst = new mojs.Burst({
        parent: "#clap",
        radius: { 50: 75 },
        angle: 25,
        children: {
          shape: "circle",
          fill: "rgba(149,165,166,0.5)",
          delay: 30,
          radius: { 3: 0 },
          speed: 0.2,
          easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
          duration: tlDuration,
        },
      });

      const countTotalAnimation = new mojs.Html({
        el: "#clapCountTotal",
        opacity: { 0: 1 },
        delay: (3 * tlDuration) / 2,
        duration: tlDuration,
        y: { 0: -3 },
      });

      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";

      const newAnimationTimeline = this.animationTimeline.add([
        scaleButton,
        countTotalAnimation,
        countAnimation,
        triangleBurst,
        circleBurst,
      ]);
      this.setState({ animationTimeline: newAnimationTimeline });
    }

    render() {
      return (
        <WrappedComponent
          {...this.props}
          animationTimeline={this.state.animationTimeline}
        />
      );
    }
  }
  return WithClapAnimation;
};

const MediumClap = ({ animationTimeline }) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count, countTotal, isClicked } = clapState;

  const handleClapClick = () => {
    if (animationTimeline) {
      animationTimeline.replay();
    }
    setClapState((prevState) => {
      return {
        ...prevState,
        count: Math.min(prevState.count + 1, MAXIMUM_USER_CLAP),
        countTotal:
          count >= MAXIMUM_USER_CLAP
            ? prevState.countTotal
            : prevState.countTotal + 1,
        isClicked: true,
      };
    });
  };

  return (
    <button id="clap" className={styles.clap} onClick={handleClapClick}>
      <ClapIcon isClicked={isClicked} />
      <ClapCount count={count} />
      <CountTotal countTotal={countTotal} />
    </button>
  );
};

/**
 * subcomponents
 */
const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count }) => {
  return (
    <span id="clapCount" className={styles.count}>
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal }) => {
  return (
    <span id="clapCountTotal" className={styles.total}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */
const Usage = () => {
  const AnimatedMediumClap = withClapAnimation(MediumClap);
  return <AnimatedMediumClap />;
};

export default Usage;

```

## Custom Hooks: The first Fundamental Pattern ##
### (Bonus) New to hooks? ###
1. [https://www.udemy.com/course/the-complete-guide-to-advanced-react-patterns/learn/lecture/18078607#overview](https://www.udemy.com/course/the-complete-guide-to-advanced-react-patterns/learn/lecture/18078607#overview)

### Introduction to Custom Hooks ###
1. Custom hook
	1. It is a hook that we build ourselves
	2. They help us to extract component logic into re-usable functions (and more)
	3. They are important but not advanced
2. Rules
	1. Name starts with `use`
	2. Anything can come after
	3. Rules of hooks
		1. You can call them only at the top level
		2. You can call them only from React functions

### Building an animation custom hook ###
1. Refactoring
	1. `MediumClap`
		1. Invokes hook
		2. Hook returns a value
	2. `useClapAnimation` - handles all animation related logic

### Why reusability fails - important! ###
1. Sphere of influence - each component has one
	1. Two components must not access global variables
		1. What are those?
			1. `#id` - they live on global space - there should be only one in global space (any duplicates will influence the other)
				1. Fix: Logic must be constrained to its sphere of influence

### Custom hooks and refs ###
1. It applies to classes, too
	1. Solution: Add unique value attached to class name or id
	2. Solution: Using Refs
		1. Refs provide a way to access DOM nodes or React elements created in the render method
		2. Implementation:
			1. Way 1:
			
			```javascript
			class MyComponent extends React.Component {
			  constructor(props) {
			    super(props);
				this.myRef = React.createRef();
			  }
			  render() {
			    return <div ref={this.myRef} />;
			  }
			}
			
			// Accessing Refs
			const node = this.myRef.current; // contains reference to the node
			```
			
			2. Way 2: Pass a function instead. The function receives the React component instance or HTML DOM element as its argument, which can be stored and accessed elsewhere.
			
			```javascript
			class CustomTextInput extends React.Component {
			  constructor(props) {
			    super(props);
				
				this.textInput = null;
				
				this.setTextInputRef = element => {
				  this.textInput = element;
				};
				
				this.focusTextInput = () => {
				  // Focus the text input using the raw DOM API
				  if (this.textInput) this.textInput.focus();
				}
			  }
			}
			```

### When is my hook invoked? ###
1. `useEffect` is invoked after the `render` function
2. Code:

```javascript
import React, { useCallback, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const initialState = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

const MediumClap = () => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRefs] =
    React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  const handleClapClick = () => {
    if (animationTimeline) {
      animationTimeline.replay();
    }
    setClapState((prevState) => {
      return {
        ...prevState,
        count: Math.min(prevState.count + 1, MAXIMUM_USER_CLAP),
        countTotal:
          count >= MAXIMUM_USER_CLAP
            ? prevState.countTotal
            : prevState.countTotal + 1,
        isClicked: true,
      };
    });
  };

  return (
    <button
      ref={setRef}
      data-refkey="clapRef"
      className={styles.clap}
      onClick={handleClapClick}
    >
      <ClapIcon isClicked={isClicked} />
      <ClapCount count={count} setRef={setRef} />
      <CountTotal countTotal={countTotal} setRef={setRef} />
    </button>
  );
};

/**
 * subcomponents
 */
const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count, setRef }) => {
  return (
    <span ref={setRef} data-refkey="clapCountRef" className={styles.count}>
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal, setRef }) => {
  return (
    <span ref={setRef} data-refkey="clapCountTotalRef" className={styles.total}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */
const Usage = () => {
  return <MediumClap />;
};

export default Usage;
```

3. `useLayoutEffect` - for smooth animation

## The Compound Components Pattern ##
### Compound components in plain approachable language ###
1. `MediumClap` is just a large lump - one single entry point
2. Wrap components within a parent component
	1. We expose both child components and parent component
		1. They are bound internally

### Why compound components? ###
1. Benefit
	1. Customizability
		1. We can provide different customization props to the children
	2. Understandable API
		1. If we just expose the parent, the user doesn't know what's happening internally
	3. Props Overload
		1. If only parent is exposed, to pass props to child components, we need to pass them as props
		
		```javascript
		<MediumClap
		  clapProps={}
		  countTotalProps={}
		  clapIconProps={}
		/>
		```
		
		2. Solution:
		
		```javascript
		<MediumClap>
		  <ClapIcon clapProps={} />
		  <ClapCount clapCountProps={} />
		  <CountTotal countTotalProps={} />
		</MediumClap>
		```

### How to implement the pattern ###
1. Important logic is in the parent component
2. Instructions are passed to child components
3. A context object is created and child components use the context object

### Refactor to Compound components ###
1. Code:

```javascript
import React, { useCallback, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const initialState = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

const MediumClapContext = React.createContext();
const { Provider } = MediumClapContext; // Wraps the tree of components that needs the state

/**
 * MediumClap Component
 */
const MediumClap = ({ children }) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRefs] =
    React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  const handleClapClick = () => {
    if (animationTimeline) {
      animationTimeline.replay();
    }
    setClapState((prevState) => {
      return {
        ...prevState,
        count: Math.min(prevState.count + 1, MAXIMUM_USER_CLAP),
        countTotal:
          count >= MAXIMUM_USER_CLAP
            ? prevState.countTotal
            : prevState.countTotal + 1,
        isClicked: true,
      };
    });
  };

  const memoizedValue = React.useMemo(
    () => ({
      ...clapState,
      setRef,
    }),
    [clapState, setRef]
  ); // to avoid unnecessary re-renders

  return (
    <Provider value={memoizedValue}>
      <button
        ref={setRef}
        data-refkey="clapRef"
        className={styles.clap}
        onClick={handleClapClick}
      >
        {children}
      </button>
    </Provider>
  );
};

/**
 * subcomponents
 */
const ClapIcon = () => {
  const { isClicked } = React.useContext(MediumClapContext);
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = () => {
  const { count, setRef } = React.useContext(MediumClapContext);
  return (
    <span ref={setRef} data-refkey="clapCountRef" className={styles.count}>
      + {count}
    </span>
  );
};

const CountTotal = () => {
  const { countTotal, setRef } = React.useContext(MediumClapContext);
  return (
    <span ref={setRef} data-refkey="clapCountTotalRef" className={styles.total}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */
const Usage = () => {
  return (
    <MediumClap>
      <ClapIcon />
      <ClapCount />
      <CountTotal />
    </MediumClap>
  );
};

export default Usage;
```

### Alternative export strategy ###
1. Code:

```javascript
import React, { useCallback, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const initialState = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

const MediumClapContext = React.createContext();
const { Provider } = MediumClapContext; // Wraps the tree of components that needs the state

/**
 * MediumClap Component
 */
const MediumClap = ({ children }) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRefs] =
    React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  const handleClapClick = () => {
    if (animationTimeline) {
      animationTimeline.replay();
    }
    setClapState((prevState) => {
      return {
        ...prevState,
        count: Math.min(prevState.count + 1, MAXIMUM_USER_CLAP),
        countTotal:
          count >= MAXIMUM_USER_CLAP
            ? prevState.countTotal
            : prevState.countTotal + 1,
        isClicked: true,
      };
    });
  };

  const memoizedValue = React.useMemo(
    () => ({
      ...clapState,
      setRef,
    }),
    [clapState, setRef]
  ); // to avoid unnecessary re-renders

  return (
    <Provider value={memoizedValue}>
      <button
        ref={setRef}
        data-refkey="clapRef"
        className={styles.clap}
        onClick={handleClapClick}
      >
        {children}
      </button>
    </Provider>
  );
};

/**
 * subcomponents
 */
const ClapIcon = () => {
  const { isClicked } = React.useContext(MediumClapContext);
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = () => {
  const { count, setRef } = React.useContext(MediumClapContext);
  return (
    <span ref={setRef} data-refkey="clapCountRef" className={styles.count}>
      + {count}
    </span>
  );
};

const CountTotal = () => {
  const { countTotal, setRef } = React.useContext(MediumClapContext);
  return (
    <span ref={setRef} data-refkey="clapCountTotalRef" className={styles.total}>
      {countTotal}
    </span>
  );
};

MediumClap.Icon = ClapIcon;
MediumClap.Count = ClapCount;
MediumClap.Total = CountTotal;

/**
 * Usage
 */
// import MediumClap, { ClapIcon, ClapCount, CountTotal } from './MediumClap';
// import MediumClap from './MediumClap';
const Usage = () => {
  return (
    <MediumClap>
      <MediumClap.Icon />
      <MediumClap.Count />
      <MediumClap.Total />
    </MediumClap>
  );
};

export default Usage;
```

### Exposing state via a callback ###
### Invoking the useEffect callback only after mount! ###
1. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const initialState = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

const MediumClapContext = React.createContext();
const { Provider } = MediumClapContext; // Wraps the tree of components that needs the state

/**
 * MediumClap Component
 */
const MediumClap = ({ children, onClap }) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRefs] =
    React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      onClap && onClap(clapState);
    }
    componentJustMounted.current = false;
  }, [count]);

  const handleClapClick = () => {
    if (animationTimeline) {
      animationTimeline.replay();
    }
    setClapState((prevState) => {
      return {
        ...prevState,
        count: Math.min(prevState.count + 1, MAXIMUM_USER_CLAP),
        countTotal:
          count >= MAXIMUM_USER_CLAP
            ? prevState.countTotal
            : prevState.countTotal + 1,
        isClicked: true,
      };
    });
  };

  const memoizedValue = React.useMemo(
    () => ({
      ...clapState,
      setRef,
    }),
    [clapState, setRef]
  ); // to avoid unnecessary re-renders

  return (
    <Provider value={memoizedValue}>
      <button
        ref={setRef}
        data-refkey="clapRef"
        className={styles.clap}
        onClick={handleClapClick}
      >
        {children}
      </button>
    </Provider>
  );
};

/**
 * subcomponents
 */
const ClapIcon = () => {
  const { isClicked } = React.useContext(MediumClapContext);
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = () => {
  const { count, setRef } = React.useContext(MediumClapContext);
  return (
    <span ref={setRef} data-refkey="clapCountRef" className={styles.count}>
      + {count}
    </span>
  );
};

const CountTotal = () => {
  const { countTotal, setRef } = React.useContext(MediumClapContext);
  return (
    <span ref={setRef} data-refkey="clapCountTotalRef" className={styles.total}>
      {countTotal}
    </span>
  );
};

MediumClap.Icon = ClapIcon;
MediumClap.Count = ClapCount;
MediumClap.Total = CountTotal;

/**
 * Usage
 */
// import MediumClap, { ClapIcon, ClapCount, CountTotal } from './MediumClap';
// import MediumClap from './MediumClap';
const Usage = () => {
  const [count, setCount] = React.useState(0);
  const handleClap = (clapState) => {
    setCount(clapState.count);
  };
  return (
    <div style={{ width: "100%" }}>
      <MediumClap onClap={handleClap}>
        <MediumClap.Icon />
        <MediumClap.Count />
        <MediumClap.Total />
      </MediumClap>
      <div className={styles.info}>{`Clapped ${count} times!`}</div>
    </div>
  );
};

export default Usage;
```

## Patterns for Crafting Reusable Styles ##
### Introduction to reusable styles ###
1. Users must be able to change styles
	1. Strategy: JSX
		1. `className` - CSS class
		2. `style` - inline style
	2. We need the same mechanism for custom components
		
	```
	<MediumClap className="">...</MediumClap>
	```

### Extending styles via a style prop ###
1. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const initialState = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

const MediumClapContext = React.createContext();
const { Provider } = MediumClapContext; // Wraps the tree of components that needs the state

/**
 * MediumClap Component
 */
const MediumClap = ({ children, onClap, style: userStyles = {} }) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRefs] =
    React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      onClap && onClap(clapState);
    }
    componentJustMounted.current = false;
  }, [count]);

  const handleClapClick = () => {
    if (animationTimeline) {
      animationTimeline.replay();
    }
    setClapState((prevState) => {
      return {
        ...prevState,
        count: Math.min(prevState.count + 1, MAXIMUM_USER_CLAP),
        countTotal:
          count >= MAXIMUM_USER_CLAP
            ? prevState.countTotal
            : prevState.countTotal + 1,
        isClicked: true,
      };
    });
  };

  const memoizedValue = React.useMemo(
    () => ({
      ...clapState,
      setRef,
    }),
    [clapState, setRef]
  ); // to avoid unnecessary re-renders

  return (
    <Provider value={memoizedValue}>
      <button
        ref={setRef}
        data-refkey="clapRef"
        className={styles.clap}
        onClick={handleClapClick}
        style={userStyles}
      >
        {children}
      </button>
    </Provider>
  );
};

/**
 * subcomponents
 */
const ClapIcon = ({ style: userStyles = {} }) => {
  const { isClicked } = React.useContext(MediumClapContext);
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
        style={userStyles}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ style: userStyles = {} }) => {
  const { count, setRef } = React.useContext(MediumClapContext);
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={styles.count}
      style={userStyles}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ style: userStyles = {} }) => {
  const { countTotal, setRef } = React.useContext(MediumClapContext);
  return (
    <span
      ref={setRef}
      data-refkey="clapCountTotalRef"
      className={styles.total}
      style={userStyles}
    >
      {countTotal}
    </span>
  );
};

MediumClap.Icon = ClapIcon;
MediumClap.Count = ClapCount;
MediumClap.Total = CountTotal;

/**
 * Usage
 */
// import MediumClap, { ClapIcon, ClapCount, CountTotal } from './MediumClap';
// import MediumClap from './MediumClap';
const Usage = () => {
  const [count, setCount] = React.useState(0);
  const handleClap = (clapState) => {
    setCount(clapState.count);
  };
  return (
    <div style={{ width: "100%" }}>
      <MediumClap onClap={handleClap} style={{ border: "1ps solid red" }}>
        <MediumClap.Icon />
        <MediumClap.Count />
        <MediumClap.Total style={{ background: "#8cacea", color: "black" }} />
      </MediumClap>
      <div className={styles.info}>{`Clapped ${count} times!`}</div>
    </div>
  );
};

export default Usage;
```

### Extending styles via a className prop ###
1. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";
import userCustomStyles from "./usage.css";

const initialState = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

const MediumClapContext = React.createContext();
const { Provider } = MediumClapContext; // Wraps the tree of components that needs the state

/**
 * MediumClap Component
 */
const MediumClap = ({
  children,
  onClap,
  style: userStyles = {},
  className,
}) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRefs] =
    React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      onClap && onClap(clapState);
    }
    componentJustMounted.current = false;
  }, [count]);

  const handleClapClick = () => {
    if (animationTimeline) {
      animationTimeline.replay();
    }
    setClapState((prevState) => {
      return {
        ...prevState,
        count: Math.min(prevState.count + 1, MAXIMUM_USER_CLAP),
        countTotal:
          count >= MAXIMUM_USER_CLAP
            ? prevState.countTotal
            : prevState.countTotal + 1,
        isClicked: true,
      };
    });
  };

  const memoizedValue = React.useMemo(
    () => ({
      ...clapState,
      setRef,
    }),
    [clapState, setRef]
  ); // to avoid unnecessary re-renders

  // className -> 'clap-1234 classUser'
  const classNames = [styles.clap, className].filter(Boolean).join(" ").trim();
  return (
    <Provider value={memoizedValue}>
      <button
        ref={setRef}
        data-refkey="clapRef"
        className={classNames}
        onClick={handleClapClick}
        style={userStyles}
      >
        {children}
      </button>
    </Provider>
  );
};

/**
 * subcomponents
 */
const ClapIcon = ({ style: userStyles = {}, className }) => {
  const { isClicked } = React.useContext(MediumClapContext);
  const classNames = [styles.icon, isClicked ? styles.checked : "", className]
    .filter(Boolean)
    .join(" ")
    .trim();
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={classNames}
        style={userStyles}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ style: userStyles = {}, className }) => {
  const { count, setRef } = React.useContext(MediumClapContext);
  const classNames = [styles.count, className].filter(Boolean).join(" ").trim();
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={classNames}
      style={userStyles}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ style: userStyles = {}, className }) => {
  const { countTotal, setRef } = React.useContext(MediumClapContext);
  const classNames = [styles.total, className].filter(Boolean).join(" ").trim();
  return (
    <span
      ref={setRef}
      data-refkey="clapCountTotalRef"
      className={classNames}
      style={userStyles}
    >
      {countTotal}
    </span>
  );
};

MediumClap.Icon = ClapIcon;
MediumClap.Count = ClapCount;
MediumClap.Total = CountTotal;

/**
 * Usage
 */
// import MediumClap, { ClapIcon, ClapCount, CountTotal } from './MediumClap';
// import MediumClap from './MediumClap';
const Usage = () => {
  const [count, setCount] = React.useState(0);
  const handleClap = (clapState) => {
    setCount(clapState.count);
  };
  return (
    <div style={{ width: "100%" }}>
      <MediumClap onClap={handleClap} className={userCustomStyles.clap}>
        <MediumClap.Icon className={userCustomStyles.icon} />
        <MediumClap.Count className={userCustomStyles.count} />
        <MediumClap.Total className={userCustomStyles.total} />
      </MediumClap>
      <div className={styles.info}>{`Clapped ${count} times!`}</div>
    </div>
  );
};

export default Usage;
```

## The Control Props Pattern ##
### The Problem to be solved ###
1. What are control props?
	1. What if user wants to customize `count`, `countTotal`, and `isClicked`?

### What is control props? ###
1. Form elements must be controled components
	1. `<input type="text" value={this.state.val} onChange={this.handleChange} />
		1. We pass a state and a state updater
			1. Value controls the state
2. We want to make `MediumClap` a controlled component
	1. `<MediumClap values={} onClap={}>`
		1. `onClap` - state updater
		2. `values` - takes all the required state

### Implementing the pattern ###
### Practical usage of control props ###
1. If one clap is updated, the other clap is also updated.
2. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";
import userCustomStyles from "./usage.css";

const initialState = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

const MediumClapContext = React.createContext();
const { Provider } = MediumClapContext; // Wraps the tree of components that needs the state

/**
 * MediumClap Component
 */
const MediumClap = ({
  children,
  onClap,
  values = null,
  style: userStyles = {},
  className,
}) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRefs] =
    React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current && !isControlled) {
      onClap && onClap(clapState);
    }
    componentJustMounted.current = false;
  }, [count, isControlled, onClap, clapState]);

  const isControlled = !!values && onClap; // determine if controlled. !! -> convert to boolean
  const handleClapClick = () => {
    if (animationTimeline) {
      animationTimeline.replay();
    }
    isControlled
      ? onClap(clapState)
      : setClapState((prevState) => {
          return {
            ...prevState,
            count: Math.min(prevState.count + 1, MAXIMUM_USER_CLAP),
            countTotal:
              count >= MAXIMUM_USER_CLAP
                ? prevState.countTotal
                : prevState.countTotal + 1,
            isClicked: true,
          };
        });
  };

  const getState = useCallback(
    () => (isControlled ? values : clapState),
    [isControlled, values, clapState]
  ); // to avoid unnecessary re-renders. If isControlled or values or clapState changes, recreate the function.

  const memoizedValue = React.useMemo(
    () => ({
      ...getState(),
      setRef,
    }),
    [getState, setRef]
  ); // to avoid unnecessary re-renders

  // className -> 'clap-1234 classUser'
  const classNames = [styles.clap, className].filter(Boolean).join(" ").trim();
  return (
    <Provider value={memoizedValue}>
      <button
        ref={setRef}
        data-refkey="clapRef"
        className={classNames}
        onClick={handleClapClick}
        style={userStyles}
      >
        {children}
      </button>
    </Provider>
  );
};

/**
 * subcomponents
 */
const ClapIcon = ({ style: userStyles = {}, className }) => {
  const { isClicked } = React.useContext(MediumClapContext);
  const classNames = [styles.icon, isClicked ? styles.checked : "", className]
    .filter(Boolean)
    .join(" ")
    .trim();
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={classNames}
        style={userStyles}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ style: userStyles = {}, className }) => {
  const { count, setRef } = React.useContext(MediumClapContext);
  const classNames = [styles.count, className].filter(Boolean).join(" ").trim();
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={classNames}
      style={userStyles}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ style: userStyles = {}, className }) => {
  const { countTotal, setRef } = React.useContext(MediumClapContext);
  const classNames = [styles.total, className].filter(Boolean).join(" ").trim();
  return (
    <span
      ref={setRef}
      data-refkey="clapCountTotalRef"
      className={classNames}
      style={userStyles}
    >
      {countTotal}
    </span>
  );
};

MediumClap.Icon = ClapIcon;
MediumClap.Count = ClapCount;
MediumClap.Total = CountTotal;

/**
 * Usage
 */
// import MediumClap, { ClapIcon, ClapCount, CountTotal } from './MediumClap';
// import MediumClap from './MediumClap';
const INITIAL_STATE = {
  count: 0,
  countTotal: 2100,
  isClicked: false,
};
const MAXIMUM_USER_CLAP = 50;
const Usage = () => {
  const [state, setState] = React.useState(INITIAL_STATE);
  const handleClap = () => {
    setState(({ count, countTotal }) => ({
      count: Math.min(count + 1, MAXIMUM_USER_CLAP),
      countTotal: count < MAXIMUM_USER_CLAP ? countTotal + 1 : countTotal,
      isClicked: true,
    }));
  };
  return (
    <div style={{ width: "100%" }}>
      <MediumClap
        values={state}
        onClap={handleClap}
        className={userCustomStyles.clap}
      >
        <MediumClap.Icon className={userCustomStyles.icon} />
        <MediumClap.Count className={userCustomStyles.count} />
        <MediumClap.Total className={userCustomStyles.total} />
      </MediumClap>
      <MediumClap
        values={state}
        onClap={handleClap}
        className={userCustomStyles.clap}
      >
        <MediumClap.Icon className={userCustomStyles.icon} />
        <MediumClap.Count className={userCustomStyles.count} />
        <MediumClap.Total className={userCustomStyles.total} />
      </MediumClap>
    </div>
  );
};

export default Usage;
```

## Custom Hooks: A Deeper Look at the Foundational Pattern ##
### Introduction ###
1. Component - Logic + UI elements/components
	1. Logic can be broken down into smaller modules that can be re-usable
		1. Can be done using hooks
			1. Some users might need only one or more of them later

### useDOMRef ###
1. `<MediumClap />`
	1. `useClapAnimation`
	2. `useDOMRef`
	3. `useEffectAfterMount`
	4. `useClapState`

### useClapState ###
### useEffectAfterMount ###
### A practical and fun usage ###
1. If use has their own components but they can use individual hooks we built
2. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const INITIAL_STATE = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

/**
 * useDOMRef Hook
 */
const useDOMRef = () => {
  const [refs, setRefs] = React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);
  return [refs, setRef];
};

/**
 * custom hook for useClapState
 */
const useClapState = (initialState = INITIAL_STATE) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count, countTotal } = clapState;

  const updateClapState = useCallback(() => {
    setClapState(({ count, countTotal }) => {
      return {
        count: Math.min(count + 1, MAXIMUM_USER_CLAP),
        countTotal: count >= MAXIMUM_USER_CLAP ? countTotal : countTotal + 1,
        isClicked: true,
      };
    });
  }, [count, countTotal]);
  return [clapState, updateClapState];
};

/**
 * custom useEffectAfterMount hook
 */
const useEffectAfterMount = (cb, deps) => {
  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      return cb(); // returns a cleanup function
    }
    componentJustMounted.current = false;
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, deps);
};

/**
 * MediumClap, useDOMRef, useClapState, useClapAnimation
 */
const MediumClap = () => {
  const [clapState, updateClapState] = useClapState();
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRef] = useDOMRef();

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  useEffectAfterMount(() => {
    animationTimeline.replay();
  }, [count]);

  return (
    <button
      ref={setRef}
      data-refkey="clapRef"
      className={styles.clap}
      onClick={updateClapState}
    >
      <ClapIcon isClicked={isClicked} />
      <ClapCount count={count} setRef={setRef} />
      <CountTotal countTotal={countTotal} setRef={setRef} />
    </button>
  );
};

/**
 * subcomponents
 */
const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count, setRef }) => {
  return (
    <span ref={setRef} data-refkey="clapCountRef" className={styles.count}>
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal, setRef }) => {
  return (
    <span ref={setRef} data-refkey="clapCountTotalRef" className={styles.total}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */
const Usage = () => {
  return <MediumClap />;
};

export default Usage;
```

## The Props Collection Pattern ##
### An alternative export strategy ###
1. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const INITIAL_STATE = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

/**
 * useDOMRef Hook
 */
const useDOMRef = () => {
  const [refs, setRefs] = React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);
  return [refs, setRef];
};

/**
 * custom hook for useClapState
 */
const useClapState = (initialState = INITIAL_STATE) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count, countTotal } = clapState;

  const updateClapState = useCallback(() => {
    setClapState(({ count, countTotal }) => {
      return {
        count: Math.min(count + 1, MAXIMUM_USER_CLAP),
        countTotal: count >= MAXIMUM_USER_CLAP ? countTotal : countTotal + 1,
        isClicked: true,
      };
    });
  }, [count, countTotal]);
  return [clapState, updateClapState];
};

/**
 * custom useEffectAfterMount hook
 */
const useEffectAfterMount = (cb, deps) => {
  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      return cb(); // returns a cleanup function
    }
    componentJustMounted.current = false;
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, deps);
};

/**
 * MediumClap, useDOMRef, useClapState, useClapAnimation
 */
const MediumClap = () => {
  const [clapState, updateClapState] = useClapState();
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRef] = useDOMRef();

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  useEffectAfterMount(() => {
    animationTimeline.replay();
  }, [count]);

  return (
    <button
      ref={setRef}
      data-refkey="clapRef"
      className={styles.clap}
      onClick={updateClapState}
    >
      <ClapIcon isClicked={isClicked} />
      <ClapCount count={count} setRef={setRef} />
      <CountTotal countTotal={countTotal} setRef={setRef} />
    </button>
  );
};

/**
 * subcomponents
 */
const ClapContainer = ({ children, setRef, onClick, ...restProps }) => {
  return (
    <button
      ref={setRef}
      className={styles.clap}
      {...restProps}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count, setRef, ...restProps }) => {
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={styles.count}
      {...restProps}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal, setRef, ...restProps }) => {
  return (
    <span ref={setRef} className={styles.total} {...restProps}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */

// - custom hooks
// - UI components
const Usage = () => {
  const [clapState, updateClapState] = useClapState();
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRef] = useDOMRef();

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  useEffectAfterMount(() => {
    animationTimeline.replay();
  }, [count]);

  return (
    <ClapContainer
      setRef={setRef}
      onClick={updateClapState}
      data-refkey="clapRef"
    >
      {/* <ClapIcon isClicked={isClicked} /> */}
      <span>🎉</span>
      <ClapCount count={count} setRef={setRef} data-refkey="clapCountRef" />
      <CountTotal
        countTotal={countTotal}
        setRef={setRef}
        data-refkey="clapCountTotalRef"
      />
    </ClapContainer>
  );
};

export default Usage;
```

### What are props collections? ###
1. User must be able to pass a collection of props instead of individual props. We provide the collection (users likely need them).

```javascript
<Train collection />
```

### Implementing props collections ###
### Accessibility and props collections ###
1. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const INITIAL_STATE = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

/**
 * useDOMRef Hook
 */
const useDOMRef = () => {
  const [refs, setRefs] = React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);
  return [refs, setRef];
};

/**
 * custom hook for useClapState
 */
const useClapState = (initialState = INITIAL_STATE) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count, countTotal } = clapState;

  const updateClapState = useCallback(() => {
    setClapState(({ count, countTotal }) => {
      return {
        count: Math.min(count + 1, MAXIMUM_USER_CLAP),
        countTotal: count >= MAXIMUM_USER_CLAP ? countTotal : countTotal + 1,
        isClicked: true,
      };
    });
  }, [count, countTotal]);

  // accessibility
  // props collection for 'click'
  const togglerProps = {
    onClick: updateClapState,
    "aria-pressed": clapState.isClicked,
  };

  // props collection for 'count'
  const counterProps = {
    count,
    "aria-valuemax": MAXIMUM_USER_CLAP,
    "aria-valuemin": 0,
    "aria-valuenow": count,
  };

  return { clapState, updateClapState, togglerProps, counterProps };
};

/**
 * custom useEffectAfterMount hook
 */
const useEffectAfterMount = (cb, deps) => {
  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      return cb(); // returns a cleanup function
    }
    componentJustMounted.current = false;
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, deps);
};

/**
 * subcomponents
 */
const ClapContainer = ({ children, setRef, onClick, ...restProps }) => {
  return (
    <button
      ref={setRef}
      className={styles.clap}
      {...restProps}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count, setRef, ...restProps }) => {
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={styles.count}
      {...restProps}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal, setRef, ...restProps }) => {
  return (
    <span ref={setRef} className={styles.total} {...restProps}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */

// - custom hooks
// - UI components
const Usage = () => {
  const { clapState, togglerProps, counterProps } = useClapState();
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRef] = useDOMRef();

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  useEffectAfterMount(() => {
    animationTimeline.replay();
  }, [count]);

  return (
    <ClapContainer setRef={setRef} data-refkey="clapRef" {...togglerProps}>
      <ClapIcon isClicked={isClicked} />
      <div {...counterProps}>{count}</div> {/* alternative way */}
      <ClapCount setRef={setRef} data-refkey="clapCountRef" {...counterProps} />
      <CountTotal
        countTotal={countTotal}
        setRef={setRef}
        data-refkey="clapCountTotalRef"
      />
    </ClapContainer>
  );
};

export default Usage;
```

## The Props Getters Pattern ##
### What are props getters ###
1. Props getters are functions

### From collections to getters ###
### Use cases for prop getters ###
1. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect } from "react";
import styles from "./index.css";
import mojs from "mo-js";

const INITIAL_STATE = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

const callFnsInSequence =
  (...fns) =>
  (...args) => {
    fns.forEach((fn) => fn && fn(...args));
  };

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

/**
 * useDOMRef Hook
 */
const useDOMRef = () => {
  const [refs, setRefs] = React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);
  return [refs, setRef];
};

/**
 * custom hook for useClapState
 */
const useClapState = (initialState = INITIAL_STATE) => {
  const MAXIMUM_USER_CLAP = 50;
  const [clapState, setClapState] = React.useState(initialState);
  const { count, countTotal } = clapState;

  const updateClapState = useCallback(() => {
    setClapState(({ count, countTotal }) => {
      return {
        count: Math.min(count + 1, MAXIMUM_USER_CLAP),
        countTotal: count >= MAXIMUM_USER_CLAP ? countTotal : countTotal + 1,
        isClicked: true,
      };
    });
  }, [count, countTotal]);

  // accessibility
  // props collection for 'click'
  const getTogglerProps = ({ onClick, ...otherProps }) => ({
    onClick: () => callFnsInSequence(updateClapState, onClick)(),
    "aria-pressed": clapState.isClicked,
    ...otherProps,
  });

  // props collection for 'count'
  const getCounterProps = ({ ...otherProps }) => ({
    count,
    "aria-valuemax": MAXIMUM_USER_CLAP,
    "aria-valuemin": 0,
    "aria-valuenow": count,
    ...otherProps,
  });

  return { clapState, updateClapState, getTogglerProps, getCounterProps };
};

/**
 * custom useEffectAfterMount hook
 */
const useEffectAfterMount = (cb, deps) => {
  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      return cb(); // returns a cleanup function
    }
    componentJustMounted.current = false;
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, deps);
};

/**
 * subcomponents
 */
const ClapContainer = ({ children, setRef, onClick, ...restProps }) => {
  return (
    <button
      ref={setRef}
      className={styles.clap}
      {...restProps}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count, setRef, ...restProps }) => {
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={styles.count}
      {...restProps}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal, setRef, ...restProps }) => {
  return (
    <span ref={setRef} className={styles.total} {...restProps}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */

// - custom hooks
// - UI components
const Usage = () => {
  const { clapState, getTogglerProps, getCounterProps } = useClapState();
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRef] = useDOMRef();

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  useEffectAfterMount(() => {
    animationTimeline.replay();
  }, [count]);

  return (
    <ClapContainer
      setRef={setRef}
      data-refkey="clapRef"
      {...getTogglerProps({
        onClick: () => console.log("Clap!"),
        "aria-pressed": clapState.isClicked,
      })}
    >
      <ClapIcon isClicked={isClicked} />
      <div {...getCounterProps()}>{count}</div> {/* alternative way */}
      <ClapCount
        setRef={setRef}
        data-refkey="clapCountRef"
        {...getCounterProps()}
      />
      <CountTotal
        countTotal={countTotal}
        setRef={setRef}
        data-refkey="clapCountTotalRef"
      />
    </ClapContainer>
  );
};

export default Usage;
```

## The State Initialiser Pattern ##
### What are state initilializers? ###
1. Example:
	1. State managed = Motion
		1. Initial state: Not in motion
		2. Update state: Accelerator / Gas Pedal
			1. A way to update the state
		3. Reset State: Brake
			1. A way to reset the state to initial state
2. State initializer pattern
	1. Make it possible for user to set the initial state of the component
	2. Make it possible for user to reset the state to the initial state at any point int time

### First pattern requirement ###
### Handling resets ###
### Handling reset side effects ###
1. Side effect example: Sending updated state to the server
2. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect, useRef } from "react";
import styles from "./index.css";
import mojs from "mo-js";
import userStyles from "./usage.css";

const INITIAL_STATE = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

const callFnsInSequence =
  (...fns) =>
  (...args) => {
    fns.forEach((fn) => fn && fn(...args));
  };

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

/**
 * useDOMRef Hook
 */
const useDOMRef = () => {
  const [refs, setRefs] = React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);
  return [refs, setRef];
};

/**
 * custom hook for getting previous prop/state
 */
function usePrevious(value) {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  }, [value]);
  return ref.current;
}

/**
 * custom hook for useClapState
 */
const useClapState = (initialState = INITIAL_STATE) => {
  const MAXIMUM_USER_CLAP = 50;
  const userInitialState = useRef(initialState); // does not change between re-renders
  const [clapState, setClapState] = React.useState(initialState);
  const { count, countTotal } = clapState;

  const updateClapState = useCallback(() => {
    setClapState(({ count, countTotal }) => {
      return {
        count: Math.min(count + 1, MAXIMUM_USER_CLAP),
        countTotal: count >= MAXIMUM_USER_CLAP ? countTotal : countTotal + 1,
        isClicked: true,
      };
    });
  }, [count, countTotal]);

  // accessibility
  // props collection for 'click'
  const getTogglerProps = ({ onClick, ...otherProps }) => ({
    onClick: () => callFnsInSequence(updateClapState, onClick)(),
    "aria-pressed": clapState.isClicked,
    ...otherProps,
  });

  // props collection for 'count'
  const getCounterProps = ({ ...otherProps }) => ({
    count,
    "aria-valuemax": MAXIMUM_USER_CLAP,
    "aria-valuemin": 0,
    "aria-valuenow": count,
    ...otherProps,
  });

  // glorified counter for reset usage
  const resetDep = useRef(0); // 0, 1, 2, ...
  const prevCount = usePrevious(count);
  const reset = useCallback(() => {
    // if there's a change to state, reset
    if (prevCount !== count) {
      setClapState(userInitialState.current);
      resetDep.current += 1;
    }
  }, [prevCount, count, setClapState]);

  return {
    clapState,
    updateClapState,
    getTogglerProps,
    getCounterProps,
    reset,
    resetDep: resetDep.current,
  };
};

/**
 * custom useEffectAfterMount hook
 */
const useEffectAfterMount = (cb, deps) => {
  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      return cb(); // returns a cleanup function
    }
    componentJustMounted.current = false;
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, deps);
};

/**
 * subcomponents
 */
const ClapContainer = ({ children, setRef, onClick, ...restProps }) => {
  return (
    <button
      ref={setRef}
      className={styles.clap}
      {...restProps}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count, setRef, ...restProps }) => {
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={styles.count}
      {...restProps}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal, setRef, ...restProps }) => {
  return (
    <span ref={setRef} className={styles.total} {...restProps}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */

// - custom hooks
// - UI components
const userInitialState = {
  count: 0,
  countTotal: 1000,
  isClicked: false,
};

const Usage = () => {
  const { clapState, getTogglerProps, getCounterProps, reset, resetDep } =
    useClapState(userInitialState);
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRef] = useDOMRef();

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  useEffectAfterMount(() => {
    animationTimeline.replay();
  }, [count]);

  const [uploadingReset, setUploadingReset] = React.useState(false);
  useEffectAfterMount(() => {
    setUploadingReset(true);

    const timeoutId = setTimeout(() => {
      setUploadingReset(false);
    }, 3000);

    return () => clearTimeout(timeoutId);
  }, [resetDep]);

  return (
    <div>
      <ClapContainer
        setRef={setRef}
        data-refkey="clapRef"
        {...getTogglerProps({
          onClick: () => console.log("Clap!"),
          "aria-pressed": clapState.isClicked,
        })}
      >
        <ClapIcon isClicked={isClicked} />
        <div {...getCounterProps()}>{count}</div> {/* alternative way */}
        <ClapCount
          setRef={setRef}
          data-refkey="clapCountRef"
          {...getCounterProps()}
        />
        <CountTotal
          countTotal={countTotal}
          setRef={setRef}
          data-refkey="clapCountTotalRef"
        />
      </ClapContainer>
      <section>
        <button onClick={reset} className={userStyles.resetBtn}>
          reset
        </button>
        <pre className={userStyles.resetMsg}>
          {JSON.stringify({ count, countTotal, isClicked }, null, 2)}
        </pre>
        <pre className={userStyles.resetMsg}>
          {uploadingReset ? `Uploading reset ${resetDep}` : ""}
        </pre>
      </section>
    </div>
  );
};

export default Usage;
```

### How usePrevious works ###
1. First time we pass a `value` a `ref` object is created
	1. `useEffect` is not called until the return statement of the component is reached
		1. Once the `return ref.current` is executed, `useEffect` is run which sets the value `ref.current` to `value`
	2. When we click the second time, we call `usePrevious(count)`
		1. `ref` object is not re-created because it was created before
		2. `ref.current` is returned (previous value)
		3. `useEffect` runs and updates `ref.current` to `value`

## The State Reducer Pattern ##
### The state reducer pattern ###
1. Reducer is a function that takes a `state` and and `action` and returns a new state based off of action

```javascript
(state, action) => {
  return newState;
}
```

	1. We can allow user of the component or hook to pass in a `reducer` and give them the control to update your internal state from the outside
		1. Example: Control props
		
		```javascript
		<MediumClap values={state.values} onChange={handleChange} />
		```
			
			1. Callback can update internal state
	2. Example: With reducer
	
	```javascript
	<MediumClap reducer={reducer} />
	```
	
		1. User can pass a custom reducer

### 02 From useState to useReducer ###
1. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect, useRef } from "react";
import styles from "./index.css";
import mojs from "mo-js";
import userStyles from "./usage.css";

const INITIAL_STATE = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

const callFnsInSequence =
  (...fns) =>
  (...args) => {
    fns.forEach((fn) => fn && fn(...args));
  };

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

/**
 * useDOMRef Hook
 */
const useDOMRef = () => {
  const [refs, setRefs] = React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);
  return [refs, setRef];
};

/**
 * custom hook for getting previous prop/state
 */
function usePrevious(value) {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  }, [value]);
  return ref.current; // undefined - the first time.
}

/**
 * custom hook for useClapState
 */
// useReducer as opposed to useState
const reducer = ({ count, countTotal }, { type, payload }) => {
  switch (type) {
    case "CLAP":
      return {
        count: Math.min(count + 1, MAXIMUM_USER_CLAP),
        countTotal: count >= MAXIMUM_USER_CLAP ? countTotal : countTotal + 1,
        isClicked: true,
      };
    case "RESET":
      return payload;
    default:
      return { count, countTotal, isClicked: false };
  }
};

const MAXIMUM_USER_CLAP = 50;

const useClapState = (initialState = INITIAL_STATE) => {
  const userInitialState = useRef(initialState); // does not change between re-renders
  const [clapState, dispatch] = React.useReducer(reducer, initialState);
  const { count, countTotal } = clapState;

  const updateClapState = () => dispatch({ type: "CLAP" });

  // accessibility
  // props collection for 'click'
  const getTogglerProps = ({ onClick, ...otherProps }) => ({
    onClick: () => callFnsInSequence(updateClapState, onClick)(),
    "aria-pressed": clapState.isClicked,
    ...otherProps,
  });

  // props collection for 'count'
  const getCounterProps = ({ ...otherProps }) => ({
    count,
    "aria-valuemax": MAXIMUM_USER_CLAP,
    "aria-valuemin": 0,
    "aria-valuenow": count,
    ...otherProps,
  });

  // glorified counter for reset usage
  const resetDep = useRef(0); // 0, 1, 2, ...
  const prevCount = usePrevious(count);
  const reset = useCallback(() => {
    // if there's a change to state, reset
    if (prevCount !== count) {
      dispatch({ type: "RESET", payload: userInitialState.current });
      resetDep.current += 1;
    }
  }, [prevCount, count, dispatch]);

  return {
    clapState,
    updateClapState,
    getTogglerProps,
    getCounterProps,
    reset,
    resetDep: resetDep.current,
  };
};

/**
 * custom useEffectAfterMount hook
 */
const useEffectAfterMount = (cb, deps) => {
  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      return cb(); // returns a cleanup function
    }
    componentJustMounted.current = false;
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, deps);
};

/**
 * subcomponents
 */
const ClapContainer = ({ children, setRef, onClick, ...restProps }) => {
  return (
    <button
      ref={setRef}
      className={styles.clap}
      {...restProps}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count, setRef, ...restProps }) => {
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={styles.count}
      {...restProps}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal, setRef, ...restProps }) => {
  return (
    <span ref={setRef} className={styles.total} {...restProps}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */

// - custom hooks
// - UI components
const userInitialState = {
  count: 0,
  countTotal: 1000,
  isClicked: false,
};

const Usage = () => {
  const { clapState, getTogglerProps, getCounterProps, reset, resetDep } =
    useClapState(userInitialState);
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRef] = useDOMRef();

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  useEffectAfterMount(() => {
    animationTimeline.replay();
  }, [count]);

  const [uploadingReset, setUploadingReset] = React.useState(false);
  useEffectAfterMount(() => {
    setUploadingReset(true);

    const timeoutId = setTimeout(() => {
      setUploadingReset(false);
    }, 3000);

    return () => clearTimeout(timeoutId);
  }, [resetDep]);

  return (
    <div>
      <ClapContainer
        setRef={setRef}
        data-refkey="clapRef"
        {...getTogglerProps({
          onClick: () => console.log("Clap!"),
          "aria-pressed": clapState.isClicked,
        })}
      >
        <ClapIcon isClicked={isClicked} />
        <div {...getCounterProps()}>{count}</div> {/* alternative way */}
        <ClapCount
          setRef={setRef}
          data-refkey="clapCountRef"
          {...getCounterProps()}
        />
        <CountTotal
          countTotal={countTotal}
          setRef={setRef}
          data-refkey="clapCountTotalRef"
        />
      </ClapContainer>
      <section>
        <button onClick={reset} className={userStyles.resetBtn}>
          reset
        </button>
        <pre className={userStyles.resetMsg}>
          {JSON.stringify({ count, countTotal, isClicked }, null, 2)}
        </pre>
        <pre className={userStyles.resetMsg}>
          {uploadingReset ? `Uploading reset ${resetDep}` : ""}
        </pre>
      </section>
    </div>
  );
};

export default Usage;
```

### Passing a user custom reducer ###
1. `<MediumClap reducer={reducer} />`
	1. User needs to write all the logic of the reducer. The user doesn't want to do that.
2. Code:

```javascript
import React, { useCallback, useEffect, useLayoutEffect, useRef } from "react";
import styles from "./index.css";
import mojs from "mo-js";
import userStyles from "./usage.css";

const INITIAL_STATE = {
  count: 0,
  countTotal: 267,
  isClicked: false,
};

const callFnsInSequence =
  (...fns) =>
  (...args) => {
    fns.forEach((fn) => fn && fn(...args));
  };

/**
 * Custom Hook for Animation
 */
const useClapAnimation = ({ clapEl, clapCountEl, clapCountTotalEl }) => {
  const [animationTimeline, setAnimationTimeline] = React.useState(
    () => new mojs.Timeline()
  ); // lazy init

  useLayoutEffect(() => {
    if (!clapEl || !clapCountEl || !clapCountTotalEl) {
      return;
    }

    const tlDuration = 300;
    const scaleButton = new mojs.Html({
      el: clapEl,
      duration: tlDuration,
      scale: { 1.3: 1 },
      easing: mojs.easing.ease.out,
    });

    const countAnimation = new mojs.Html({
      el: clapCountEl,
      opacity: { 0: 1 },
      y: { 0: -30 },
      duration: tlDuration,
    }).then({
      opacity: { 1: 0 },
      y: -80,
      delay: tlDuration / 2,
    });

    const triangleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 95 },
      count: 5,
      angle: 30,
      children: {
        shape: "polygon",
        radius: { 6: 0 },
        stroke: "rgba(211,54,0,0.5)",
        strokeWidth: 2,
        angle: 210,
        delay: 30,
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const circleBurst = new mojs.Burst({
      parent: clapEl,
      radius: { 50: 75 },
      angle: 25,
      children: {
        shape: "circle",
        fill: "rgba(149,165,166,0.5)",
        delay: 30,
        radius: { 3: 0 },
        speed: 0.2,
        easing: mojs.easing.bezier(0.1, 1, 0.3, 1),
        duration: tlDuration,
      },
    });

    const countTotalAnimation = new mojs.Html({
      el: clapCountTotalEl,
      opacity: { 0: 1 },
      delay: (3 * tlDuration) / 2,
      duration: tlDuration,
      y: { 0: -3 },
    });

    if (typeof clapEl === "string") {
      const clap = document.getElementById("clap");
      clap.style.transform = "scale(1, 1)";
    } else {
      clapEl.style.transform = "scale(1, 1)";
    }

    const newAnimationTimeline = animationTimeline.add([
      scaleButton,
      countTotalAnimation,
      countAnimation,
      triangleBurst,
      circleBurst,
    ]);
    setAnimationTimeline(newAnimationTimeline);
  }, [clapEl, clapCountEl, clapCountTotalEl]);

  return { animationTimeline, setAnimationTimeline };
};

/**
 * useDOMRef Hook
 */
const useDOMRef = () => {
  const [refs, setRefs] = React.useState({});
  const setRef = useCallback((node) => {
    if (node) {
      setRefs((prevRefs) => ({ ...prevRefs, [node.dataset.refkey]: node }));
    }
  }, []);
  return [refs, setRef];
};

/**
 * custom hook for getting previous prop/state
 */
function usePrevious(value) {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  }, [value]);
  return ref.current; // undefined - the first time.
}

/**
 * custom hook for useClapState
 */
// useReducer as opposed to useState
const internalReducer = ({ count, countTotal }, { type, payload }) => {
  switch (type) {
    case "CLAP":
      return {
        count: Math.min(count + 1, MAXIMUM_USER_CLAP),
        countTotal: count >= MAXIMUM_USER_CLAP ? countTotal : countTotal + 1,
        isClicked: true,
      };
    case "RESET":
      return payload;
    default:
      return { count, countTotal, isClicked: false };
  }
};

const MAXIMUM_USER_CLAP = 50;

const useClapState = (
  initialState = INITIAL_STATE,
  reducer = internalReducer
) => {
  const userInitialState = useRef(initialState); // does not change between re-renders
  const [clapState, dispatch] = React.useReducer(reducer, initialState);
  const { count, countTotal } = clapState;

  const updateClapState = () => dispatch({ type: "CLAP" });

  // accessibility
  // props collection for 'click'
  const getTogglerProps = ({ onClick, ...otherProps }) => ({
    onClick: () => callFnsInSequence(updateClapState, onClick)(),
    "aria-pressed": clapState.isClicked,
    ...otherProps,
  });

  // props collection for 'count'
  const getCounterProps = ({ ...otherProps }) => ({
    count,
    "aria-valuemax": MAXIMUM_USER_CLAP,
    "aria-valuemin": 0,
    "aria-valuenow": count,
    ...otherProps,
  });

  // glorified counter for reset usage
  const resetDep = useRef(0); // 0, 1, 2, ...
  const prevCount = usePrevious(count);
  const reset = useCallback(() => {
    // if there's a change to state, reset
    if (prevCount !== count) {
      dispatch({ type: "RESET", payload: userInitialState.current });
      resetDep.current += 1;
    }
  }, [prevCount, count, dispatch]);

  return {
    clapState,
    updateClapState,
    getTogglerProps,
    getCounterProps,
    reset,
    resetDep: resetDep.current,
  };
};

/**
 * custom useEffectAfterMount hook
 */
const useEffectAfterMount = (cb, deps) => {
  const componentJustMounted = React.useRef(true); // to avoid calling onClap on initial mount
  useEffect(() => {
    if (!componentJustMounted.current) {
      return cb(); // returns a cleanup function
    }
    componentJustMounted.current = false;
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, deps);
};

/**
 * subcomponents
 */
const ClapContainer = ({ children, setRef, onClick, ...restProps }) => {
  return (
    <button
      ref={setRef}
      className={styles.clap}
      {...restProps}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const ClapIcon = ({ isClicked }) => {
  return (
    <span>
      <svg
        id="clapIcon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="-549 338 100.1 125"
        className={`${styles.icon} ${isClicked ? styles.checked : ""}`}
      >
        <path d="M-471.2 366.8c1.2 1.1 1.9 2.6 2.3 4.1.4-.3.8-.5 1.2-.7 1-1.9.7-4.3-1-5.9-2-1.9-5.2-1.9-7.2.1l-.2.2c1.8.1 3.6.9 4.9 2.2zm-28.8 14c.4.9.7 1.9.8 3.1l16.5-16.9c.6-.6 1.4-1.1 2.1-1.5 1-1.9.7-4.4-.9-6-2-1.9-5.2-1.9-7.2.1l-15.5 15.9c2.3 2.2 3.1 3 4.2 5.3zm-38.9 39.7c-.1-8.9 3.2-17.2 9.4-23.6l18.6-19c.7-2 .5-4.1-.1-5.3-.8-1.8-1.3-2.3-3.6-4.5l-20.9 21.4c-10.6 10.8-11.2 27.6-2.3 39.3-.6-2.6-1-5.4-1.1-8.3z" />
        <path d="M-527.2 399.1l20.9-21.4c2.2 2.2 2.7 2.6 3.5 4.5.8 1.8 1 5.4-1.6 8l-11.8 12.2c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l34-35c1.9-2 5.2-2.1 7.2-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l28.5-29.3c2-2 5.2-2 7.1-.1 2 1.9 2 5.1.1 7.1l-28.5 29.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.4 1.7 0l24.7-25.3c1.9-2 5.1-2.1 7.1-.1 2 1.9 2 5.2.1 7.2l-24.7 25.3c-.5.5-.4 1.2 0 1.7.5.5 1.2.5 1.7 0l14.6-15c2-2 5.2-2 7.2-.1 2 2 2.1 5.2.1 7.2l-27.6 28.4c-11.6 11.9-30.6 12.2-42.5.6-12-11.7-12.2-30.8-.6-42.7m18.1-48.4l-.7 4.9-2.2-4.4m7.6.9l-3.7 3.4 1.2-4.8m5.5 4.7l-4.8 1.6 3.1-3.9" />
      </svg>
    </span>
  );
};

const ClapCount = ({ count, setRef, ...restProps }) => {
  return (
    <span
      ref={setRef}
      data-refkey="clapCountRef"
      className={styles.count}
      {...restProps}
    >
      + {count}
    </span>
  );
};

const CountTotal = ({ countTotal, setRef, ...restProps }) => {
  return (
    <span ref={setRef} className={styles.total} {...restProps}>
      {countTotal}
    </span>
  );
};

/**
 * Usage
 */

// - custom hooks
// - UI components
const userInitialState = {
  count: 0,
  countTotal: 1000,
  isClicked: false,
};

const Usage = () => {
  const reducer = (state, action) => {
    switch (action.type) {
      case "CLAP":
        return {
          ...state,
          count: state.count + 1,
          countTotal: state.countTotal + 1,
          isClicked: true,
        };
      case "RESET":
        return { ...state, ...action.payload };
      default:
        return state;
    }
  };
  const { clapState, getTogglerProps, getCounterProps, reset, resetDep } =
    useClapState(userInitialState, reducer);
  const { count, countTotal, isClicked } = clapState;

  const [{ clapRef, clapCountRef, clapCountTotalRef }, setRef] = useDOMRef();

  const { animationTimeline } = useClapAnimation({
    clapEl: clapRef,
    clapCountEl: clapCountRef,
    clapCountTotalEl: clapCountTotalRef,
  });

  useEffectAfterMount(() => {
    animationTimeline.replay();
  }, [count]);

  const [uploadingReset, setUploadingReset] = React.useState(false);
  useEffectAfterMount(() => {
    setUploadingReset(true);

    const timeoutId = setTimeout(() => {
      setUploadingReset(false);
    }, 3000);

    return () => clearTimeout(timeoutId);
  }, [resetDep]);

  return (
    <div>
      <ClapContainer
        setRef={setRef}
        data-refkey="clapRef"
        {...getTogglerProps({
          onClick: () => console.log("Clap!"),
          "aria-pressed": clapState.isClicked,
        })}
      >
        <ClapIcon isClicked={isClicked} />
        <div {...getCounterProps()}>{count}</div> {/* alternative way */}
        <ClapCount
          setRef={setRef}
          data-refkey="clapCountRef"
          {...getCounterProps()}
        />
        <CountTotal
          countTotal={countTotal}
          setRef={setRef}
          data-refkey="clapCountTotalRef"
        />
      </ClapContainer>
      <section>
        <button onClick={reset} className={userStyles.resetBtn}>
          reset
        </button>
        <pre className={userStyles.resetMsg}>
          {JSON.stringify({ count, countTotal, isClicked }, null, 2)}
        </pre>
        <pre className={userStyles.resetMsg}>
          {uploadingReset ? `Uploading reset ${resetDep}` : ""}
        </pre>
      </section>
    </div>
  );
};

export default Usage;
```

### Exposing the internal reducer and types ###
1. With state reducer pattern, there is inversion of control with the user doing very little on their side.
2. We can also expose `dispatch` function

## (Bonus) Classifying the Patterns: How to choose the best API ##
### How the classification works ###
1. Choosing the best API for re-usable components
	1. How to implement given a use-case
2. Classifying patterns based on criteria
	1. Chart
		1. X-axis: What matters to you the most
			1. `User Interface` ----- `Logic` (that we want to share)
				1. Re-usable components - UI focus
				2. beautiful-react-hooks - Logic focus (no UI components)
		2. Y-axis: Difficulty level
			1. How hard is it to build the pattern?

### Making the right API choice ###
1. Logic focused
	1. Custom Hooks
		1. Slighty more difficult
			1. `beautiful-react-hooks`
	2. State Reducer (related to components)
		1. More difficult
	3. Control Props
		1. Slighty more difficult
2. User Interface focused
	1. Reusable Styles
		1. Easy to implement
	2. Compound Components
		1. Slighty harder to implement
3. Both
	1. State Initializers
		1. Decent difficulty level
		2. It offers UIs or logic to users
			1. Offers ease to users
	2. Props Collection & Getters
		2. Easier to implement

## Conclusion ##
### Thank you! ###