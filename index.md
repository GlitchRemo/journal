---
journalStartData: 27th May
InspiredFrom: Jayanth
Upcoming sections: Music playlist, Marvel Movies
Suggestions: Build common keywords links for easy access, start todo with a verb
---

{::options parse_block_html="true" /}

# TODO

- [ ] Take feedback on Jun 9 notes on Inheritance
- [ ] Implement tic-tac-toe with game and controller class
- [ ] Take input in save the goat
- [ ] Jump the dino
- [ ] Appear balloon in Balloon Shooter

---

# STEP Classes

<details><summary markdown = "span">topics covered</summary>

1. [mock fn](#mock-function)
1. [stub fn](#stub-function)

</details>

<details><summary markdown = "span">datewise log</summary>

1. [Jun 10](#jun-10)
1. [Jun 9](#jun-9)
1. [Jun 8](#jun-8)
1. [Jun 7](#jun-7)
1. [Jun 6](#jun-6)
1. [Jun 5](#jun-5)
1. [Jun 2](#jun-2)
1. [Jun 1](#jun-1)
1. [May 30](#may-30)
1. [May 28](#may-28)
1. [May 27](#may-27)

</details>

---

# Jun 10

- Mocking using `it` predefined
- For asynchronous function testing, `it` callback accept a `done` function
- `done` promises that asserts will be executed only when it `done` is executed
- Problem arises with testing set Interval callback

```js
const timedCounterListener = (count) => {
  if (count === 2) {
    tc.pause();
    done();
    assert.strictEqual(count, 2); // this assert will not be executed before the above statement is executed
  }
};
```

- for that write `it` as

```js
it("testName", (context, done) => {
  // body of callback
});
```

- ### use of context

> ### Code

```js
resume() {
  this.#intervalId = this.#scheduler.schedule(() => {
    this.emit("tick", this.#timesTicked);
    this.#timesTicked++;
  }, this.#interval * 1000);
}
```

> ### Test

```js
it("should count two time", (context) => {
  const schedule = context.mock.fn((callback, delay) => {
    callback();
    callback();
    assert.deepEqual(delay, 1000);
  });
  const unschedule = context.mock.fn();
  const scheduler = { schedule, unschedule };
  const spyListener = context.mock.fn();
  const tc = new TimedCounter(1, scheduler);

  tc.on("tick", spyListener);
  tc.resume();

  assert.deepEqual(spyListener.mock.callCount(), 2);
  assert.deepEqual(spyListener.mock.calls[0].arguments[0], 1);
  assert.deepEqual(spyListener.mock.calls[1].arguments[0], 2);
});
```

### Stub Function

- here schedule is a stub function
- A stub acts as a small piece of code that replaces another component during testing

### Mock Function

- here unschedule is a mock function
- Mock functions allow you to test the links between code by erasing the actual implementation of a function, capturing calls to the function (and the parameters passed in those calls), capturing instances of constructor functions when instantiated with new , and allowing test-time configuration of return values.

- `eventEmitter.on()` -> registers an event
- `eventEmitter.emit()` -> emits/executes/run an event
- `setInterval(() =>eventEmitter.emit(), 100)` -> schedule an event, emits an event in suitable time
- Event scheduling is the activity of finding a suitable time for an event

### MVC architecture

[click here](https://developer.mozilla.org/en-US/docs/Glossary/MVC)

<img src="https://developer.mozilla.org/en-US/docs/Glossary/MVC/model-view-controller-light-blue.png" alt="MVC architecture" style="height: 500px; width:800px;"/>

- expalined with Tic-Tac-Toe Game by Jayanth

[tic-tac-toe](./tic-tac-toe/)

# Jun 9

- Inheritance

  - We can inherit properties and behaviours of a class
  - ```js
    class Derived extends Base {
      constructor() {
        super(); // reference to Base class
      }
    }
    ```
  - super should be the first thing to call inside a derived class constructor
  - it internally calls the Base class constructor with the argument the constructor need
  - using super keyword we can access the public fields of Base class
  - there is a `is a` relationship between Base class and Derived class
  - for example

  ```js
  class TimedCounter extends EventEmitter
  ```

````

- TimedCounter `is a` EventEmitter
- Every type in javascript is an Object
- Object class has a toString()

  - as every variable is an instance of a prototype, thats why every instance has a toString() method

> Other Learnings

- Inject process.stdout as an dependency as writer
- Inject color/styler as dependency

- Ask relevant questions to relevant class
- Modularize `controller` further as `game` and `controller`
- `controller` will interact with user and game
- `game` contains all gaming logic

# Jun 8

- Jayanth's perspective of game modelling

  - Entities
    1. Model
    2. Controller
    3. View
  - Controller should take input from input source, give it to model, and sync changes of model with view
  - Every entities should be independent of each other
  - No entities should know about any other entity other than controller

- Started bulding dino game with bittu
- Things I appreciates of Bittu:
  - Free style of problem solving
  - Think very small, implement it with most simple logic
  - Do not think of structuring, write code in main
  - Started with moving things
  - This will give speed and can try different thing in very minimum time

# Jun 7

> ### Games day

1. Planning starts with Balloon Shooter

- Appear balloon randomly within particular sections of screen
- A shooter will shoot one bullet at a time
- If a bullet touch any balloon, the balloon will disappear and score increase
- If a balloon touch upper wall, the balloon will blast and one life will decrease
- ## Games Components
  1. Shooter
  2. Screen
  3. Bullet
  4. Balloon
  5. Scoreboard
- Plan ->
  - Setup screen
  - Show screen
  - Start game after 3 sec timeout
  - Start appearing balloons
  - Take input from user
  - Move shooter or Fire shooter
  - Update score
  - Loop
- ### Components of each class
- Shooter
  1. Bullet
  1. Fire
  1. Shoot
- Screen
  1. Shooter
  2. Balloons
- Balloon
  1. Appear
  2. Blast
- Bullet
  1. Shape
  2. Position

### Swamiji showed:-

1. Buffer class

- const b = Buffer.alloc(10)
- const c = Buffer.alloc(20)
- b.copy(c);
- b.write(c);
- b.write("abcd");
- b.write([1, 2, 3]);
- b.readInt8(1);
  Buffers are useful for optimization. We dont need to write every time to the screen. Instead we can create and edit a buffer according to our need and paste the whole buffer at last. With methods like `readInt8` and `readInt32BE` we can show the buffer as we want to show it. Its like editing in a grid and then display the whole grid.

- const a = new Buffer("abcd");
  - The first argument must be of type string or an instance of Buffer, ArrayBuffer, or Array or an Array-like Object. Received undefined
- a.toString();

2. Read raw input from stdin
3. Write to screen
4. Erase a particular object

# Jun 6

> ### process.stdout methods

1.  TTY
1.  setRawMode

```js
process.stdin.setEncoding("utf8");
const fn = (data) => {
  if (data === "e") {
    process.stdin.destroy();
    return;
  }
  process.stdout.write(data);
};

process.stdin.setRawMode(true);
process.stdin.on("data", fn);
```

2.  cursorTo
3.  windowSize
4.  clearScreenDown

```js
process.stdout.clearScreenDown();
console.log(process.stdout.getWindowSize());
process.stdout.write("a");
process.stdout.cursorTo(118, 16, () => {});
process.stdout.write("a");
process.stdout.cursorTo(18, 10, () => {});
process.stdout.write("a");
process.stdout.cursorTo(118, 16, () => {});
process.stdout.write("\n");
```

> ### packages

- npm init, start, install
- a package can consume a package
- we can make a package by `npm init` and specifying an entry point in `main` key of package.json file that is created during `npm init`
  - eg. "main": "index.js"
- to use any package, `npm init` in current directory or create a package.json manually
- add a command `start: node main.js` key in `script` of package.json
- specify test command as `node --test`
- install required package by `npm --save install pathOfPackageDir`
  - this will add `dependencies` to `package.json`, if not present will create one and then add
- install sees the package.json `dependencies` and copy that package into our local in `node-modules` dir
- `node help` to see all commands
- we can write commands in `scripts` and run using `node run <command>`
- while pushing into remote repo add `node-modules` into .gitignore
- npmjs.org is a official website for publishing and installing packages
- colors and table are useful packages

# Jun 5

- Define events
- A feature of node
- Event is an concept used to seperate work of two different persons from each other
- There are events and event listeners, we register listeners to listen to a particular event
- StdinReader
- EventEmitter
- fs.createReadStream
- Example Shown:
  1. StdinReader class
  2. Timer class
  3. Finding number of vowels in each line using Set class

# Jun 2

- Tags in md
  - heading and summary tag
- Github pages
  - entry file name :-
    - index.md
    - README.md
    - index.html
- Further we can link other pages in entry page

# Jun 1

- Installed and created first file in Obsidian
- Inspired by Nitin
- Write purpose of a task before starting it

---

# May 30

- Nitin followed Getting Things Done during his project for tracking his todos
- Tracking every learning, note things while learning

---

# May 28

morning learnings

- how to test callbacks
- send a spy function to capture the callback reference
- call the callback from outside and test the working of it
- implemented in testing `readFromFiles` and `readFromStdin`

evening learnings

- `console.log` is not a bound function while `process.stdout.write` is a bound method
- generally methods are not easy to pass while fns are
- `console.log` fn does not have a state while `process.stdout` has its own state which it maintains
- that's why when we pass process.stdout, it doesn't have a state
- this is determined on how a method is called

- Jayanth's example for the same

<details><summary markdown="span"> code snippet </summary>

```js
const identity = (x) => x;
const doSomething = (f) => f(identity);
doSomething([1, 2, 3].map);
```

</details>

- how is process.stdout.write a bounded fn?

- started testing closures
- got a way to test closures of `wc()`. Have to verify from ashish

---

# May 27

- started testing reader functions of wc

- Dheeraj told to identify external dependencies by seeing which part of our logic need external
  functions and to inject that part from outside

- Swamiji's session on IOC

- yesterday we made io, repl and calculator classes
- today he tested all classes using dependency injection
- created spy function

<details><summary markdown="span"> code snippet </summary>

```js
const createSpyFunction = () => {
  let callCount = 0;
  const fn = (...args) => {
    fn.calls = [...(fn.calls || []), ...args];
    callCount++;
  };

  fn.wasCalledOnce = (arg) => callCount === 1 && fn.calls[0] === arg;
  fn.wasCalledTwice = () => callCount === 2;
  return fn;
};
```

```js
const renderer = createSpyFunction();
const calc = new Calculator();
calc.render(renderer);
assert.ok(renderer.wasCalledOnce(0));
```

</details>

- We want to make every unit independently testable
- That's why we mock external dependencies and inject to the tested functions
- Especially the asynchronous functions we want to mock
- eg. setInterval, clearInterval, process.stdin, process.stdout, fs, stdin.\_readable.stopped = true
- 3 ways to inject dependencies :- - through constructor - through function parameters - through setters

<details><summary markdown="span"> code snippet </summary>

```js
describe.skip;
describe.only; // node --test run-only
beforeEach(() => {
  const write = createSpyFunction();
});
```

</details>

- beforeEach is called before each it under the describe
- before() is called only after entering into the current describe
- similary we have after()
- before and after are used to setting something before testing and clearing before leaving

- we write test reversely as we write code

* Jayanth's example of IOC:
  - Games wallpaper settings
  - Levels in a game
  - Configuration of vimrc
  - IOC gives control to the callee from the called function

---

# Step-8 Games Takeaways

- Games demo by seniors

1. Scottland Yard

   - Praful's map design
   - Real-time game feelings
   - cool cards

2. Cashflow

   - Money Management
   - Multiple rules
   - Multiple paths

3. Cludo

   - Cool UI
   - Multiple decisions
   - Handled data security

4. Acquire
   - Save and restore feature
   - Long flowcharts
   - Planning in flow charts in iteration 0
   - Working with 56 files
   - Proper documentation, guidelines and 100% test coverage
   - Started with first cut and implemented features afterwards
   - Simple and sophisticated login page
   - Join through link shared by host

- Common Takeaways
  - Thinking of a large picture
  - Write top level idea
  - Talk in top level while doing demo
  - Every game has a
    1. login page
    2. lobby
    3. log
    4. players details
    5. database
    6. some private area
    7. host

---

# Presentation Takeaways

> `Presentors: Lakshmi and Subhash`

- Account name:- Atlassian
- Project Name: Provisioning Life Cycle

> `Presentors: Nitin and Manikantha`

- Account Name:- E4R
- Project of
  - Nitin -> Yaska
- Strategies used by Nitin
  - Ask WHY?
  - Getting Things Done

> `Presentor: Sakshi`

- Account Name: tdm growth partners
- Project Name: Turbo Portal and Turbo Client Portal
- To solve problems related to maintaing scaled data in Excel Sheet
- MFA - Multifactored Authorization
- Interesting Tech Stack
  1. Jira
  2. Confluence
  3. Twillo

> `Presentors: Chhavi, Ankamma, Azhar, Praful`

- Account: UBS Bank
- Track your work
- Build a habit

> `Presentor: Prajakta`

- Account Name: MCIP
- Project Name: Metro
- MCIP- Metro Customer Individual Pricing
- BFF - Backend For Frontend
- Have depth and breadth of knowledge
- Try different approaches
- Learn the way you want to explain to others

> `Presentor: Ritika`

- Account Name: Mckinsay
- Project Name: Engaging
- Tech Stack:
  - Docker
  - System Design
- Maintained card for test cases
- increased from 32% -> 72% test converage

> `Presentors: Swapnil, Nilam, Vivek, Tanmay`

- Account Name: Mercedes Benz
- Project Name:
  - Swapnil: Product and Merchandise Data(PMD)
  - Nilam, Vivek, Tanmay: One Touch Retail(OTR)
- used nice jargans
- Appreciate qualities of people which you like to possess
- SonarQube for test coverage checking
- Opportunity to observe things
- became billable

> `Presentors: Sampriti, Abin, Dileep, Sanjana`

- Account Name: Axis Bank
- Project Name: MLP(Maximus Lending Platform)
- Steal Ideas
- Maintain notes
- Take ownership
- Build trust
- Self reflection
- Projecting capabilities
- Teach others
- Give feedback

---

# My Tech Interests Area

- Started developing interests in Creative coding.[link here](https://youtube.com/playlist?list=PLUG_f-krxzVrRCOjGFwOuYj3QarVfPWXK)
- Got a MIT playlist on Deep Learning.[link here](https://youtube.com/playlist?list=PLUG_f-krxzVrRCOjGFwOuYj3QarVfPWXK)

---

{::options parse_block_html="false" /}
````
