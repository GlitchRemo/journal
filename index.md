---
journalStartData: 27th May
InspiredFrom: Jayanth
STEP Classes journalStartDate: 5th June
---

# STEP Classes

![picture-info](./image.jpeg)

# TODO

# Contents

1. [May 27](#may-27)
2. [May 28](#may-28)
3. [May 30](#may-30)
4. [Jun 1](#jun-1)
5. [Jun 2](#jun-2)

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

# Jun 1

- Installed and created first file in Obsidian
- Inspired by Nitin
- Write purpose of a task before starting it

# May 30

- Ppt by Lakshmi and Subhash
- Account name:- Atlassian
- Ppt by Nitin and Manikantha
- Account Name:- E4R
- Project of ...
  - Nitin -> Yaska
- Nitin followed Getting Things Done during his project for tracking his todos
- Tracking every learning, note things while learning

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

{::options parse_block_html="true" /}

<details><summary markdown="span"> code snippet </summary>
  
  ```js 
  const identity = (x) => x;
  const doSomething = (f) => f(identity);

doSomething([1, 2, 3].map);

````
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
{::options parse_block_html="false" /}

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
````
