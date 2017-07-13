#### TDD OUTPUT  
```
    Testable Code
    Feedback Loop
    Write Test to Drive Design
    TDD Rhythm[Red Green Refactor + Baby Steps]
    Think Before Code
```

##### Check NVM & NodeJS installation
```js
$node --version
```
##### Set up Project
```js
$npm init
or
$yarn init
// then take a look at package.json
```
##### Install dependencies
```js
npm install jest --save-dev // -g
or
yarn add jest --dev // -g
```

##### Module?
```js
module.exports

module.functionName
```

##### Test Frame Work [Jest]
```js
npm install jest --save-dev // -g
or
yarn add jest --dev // -g
```

##### Unit Test Life cycle
```js
beforeEach(() => {});
testcase('', () => {});
afterEach(() => {});
```

##### Assertion

#### Design with Positive, Negative, and Exception Tests
Writing tests before writing code is a skill. It may appear hard at first, but it gets better with practice. The result of that effort is a more modular, cohesive, and loosely coupled design.  
By writing tests first, we put ourselves in the shoes of the person who will be using our code before we write it.

#### Focus on Behavior Rather than State
When you start the design of a function, visualize the types of tests you'd write to verify the behavior of the function.

```quote
Write or change the minimum code to make it and other existing tests pass.
```
