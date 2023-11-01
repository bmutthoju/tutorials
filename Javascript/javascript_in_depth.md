# JavaScript in Depth #
## What are JavaScript modules? ##
JavaScript modules are a way to **organize and encapsulate code** in JavaScript applications. They provide a mechanism for breaking down a program into **smaller, reusable modules, each with its own scope, dependencies, and exports**.

JavaScript modules allow developers to create **self-contained units of functionality that can be easily shared and imported by other parts of an application**. This modular approach **promotes code reusability, maintainability, and encapsulation**.

Prior to the introduction of native JavaScript modules, various module systems and patterns were used in JavaScript, such as the **CommonJS module pattern** and the **AMD (Asynchronous Module Definition) format**. However, with the release of **ECMAScript 2015 (ES6)**, **native support for modules was introduced in JavaScript**.

Native JavaScript modules use the `import` and `export` keywords **to control the dependencies and exports of a module**. Here's a brief overview of how modules work:

1. **Exporting**: In a module, you can use the `export` keyword to specify **which functions, variables, or objects should be accessible to other modules**. For example:

		// module.js
		export function add(a, b) {
		  return a + b;
		}

		export const PI = 3.14159;

2. **Importing**: In another module, you can use the import keyword **to bring in functionality from other modules**. You **can import specific exports or the entire module as a whole**. For example:

		// main.js
		import { add, PI } from './module.js';

		console.log(add(2, 3)); // Output: 5
		console.log(PI); // Output: 3.14159

3. **Default Exports**: Additionally, a module can have **a default export, which represents the main functionality or value of the module**. **Only one default export is allowed per module**. Importing a default export does not require braces {}. For example:

		// module.js
		export default function multiply(a, b) {
		  return a * b;
		}

		// main.js
		import multiply from './module.js';

		console.log(multiply(2, 3)); // Output: 6

JavaScript modules are widely supported in modern browsers and can also be used in Node.js applications. They provide **a standardized way of organizing and sharing code, enabling better code organization, dependency management, and code reuse in JavaScript projects**.