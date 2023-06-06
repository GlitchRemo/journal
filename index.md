---
journalStartData: 27th May
InspiredFrom: Jayanth
STEP Classes journalStartDate: 5th June
Upcoming sections: Presentation Takeaways, Music playlist, Marvel Movies, Technological Playlist
---

{::options parse_block_html="true" /}

# TODO

- [ ] addListener
- [ ] Tic-tac-toe
- [ ] Save the goat
- [ ] child-process -> exec -> asplay

---

# STEP Classes

# Jun 7

> ### process.stdout methods

1. setRawMode

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
process.stdin.setRawMode(false);
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

4.  TTY

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

---

# Daily Journal

<details><summary markdown = "span">contents</summary>

1. [May 27](#may-27)
2. [May 28](#may-28)
3. [May 30](#may-30)
4. [Jun 1](#jun-1)
5. [Jun 2](#jun-2)
6. [Jun 5](#jun-5)

</details>

# Jun 5

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

# Jun 2

- Tags in md
  - heading and summary tag
- Github pages
  - entry file name :-
    - index.md
    - README.md
    - index.html
- Further we can link other pages in entry page
- Started developing interests in Creative coding.[link here](https://youtube.com/playlist?list=PLUG_f-krxzVrRCOjGFwOuYj3QarVfPWXK)
- Got a MIT playlist on Deep Learning.[link here](https://youtube.com/playlist?list=PLUG_f-krxzVrRCOjGFwOuYj3QarVfPWXK)

---

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

</details>

---

# Presentation Takeaways

> `Presentors: Lakshmi and Subhash`

- Account name:- Atlassian
- Ppt by Nitin and Manikantha
- Account Name:- E4R
- Project of ...
  - Nitin -> Yaska

{::options parse_block_html="false" /}
