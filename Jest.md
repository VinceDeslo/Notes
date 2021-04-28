# Jest

- unit test
- integration test
- UI testing

```bash
# installation:
npm i jest --save-dev

# Create folder for tests in project
mkdir __tests__
```

```tsx
// Add test execution to package.json
"scripts":{
	"test": "jest"
	// "test": "jest --coverage" for direct code coverage
},

// Add code coverage
"jest": {
	"collectCoverage": true
	"coverageReporters": ["html"]
},
```

```tsx
import {functionName} from './src/folder'

// Create a test suite within a [function].spec.js file
describe("Function name", () => {
	
	// test contents and assertions
	test("Function should do so and so", () => {
		
		// Define the inputs
		const input = [
			{ id: 1, url: "https://www.url1.dev" }
			{ id: 2, url: "https://www.url2.dev" }
		];

		// Define expected output
		const output = [{ id: 1, url: "https://www.url1.dev" }];

		// Test (call and matcher)
		expect(functionName(input)).toEqual(output); // first test case
		expect() // second test case
		expect() // third test case ...
	});
});
```

```bash
# Run the suite
npm test

# Run code coverage
npm test --coverage
```