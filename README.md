# React Native Architecture
Core principles, patterns and best practices for building a react native application

## Tech Stack

### Application Blueprint

* Always up-to-date [React Native](https://facebook.github.io/react-native/) scaffolding
* Modular and well-documented structure for application code
* [Expo](https://expo.io/) Easy to build a React Native app without any build configuration
* [Redux](http://redux.js.org/) for safe and reasonable state management
* Painless React forms with [formik](https://github.com/jaredpalmer/formik)
* [React Navigation](https://reactnavigation.org/) for awesome navigation with 60fps transitions
* [Typescript](https://www.typescriptlang.org/) for static type checking
* [Ramda](https://github.com/ramda/ramda) and [Ramda Adjunct](https://github.com/char0n/ramda-adjunct) for functional Javascript
* [Recompose](https://github.com/acdlite/recompose) for building higher order components
* [Glamorous Native](https://github.com/robinpowered/glamorous-native) for creating UI components
* Feature flags
* Clean and testable service layer for interacting with GraphQL queries and mutations
* :star: Multi-environment configuration (dev, staging, production,...) for iOS and Android
* :star: Built-in error handling, loading, updating and customizable screens

### Testing Setup

* [Jest](https://facebook.github.io/jest/) for unit testing application code and providing coverage information
* [Enzyme](https://github.com/airbnb/enzyme) and fully mocked React Native for unit testing UI components

### Dev tools

* [TSLint](https://palantir.github.io/tslint/) An extensible linter for the TypeScript language
* [Prettier](https://github.com/prettier/prettier) as an opinionated code formatter
* [lint-staged](https://github.com/okonet/lint-staged) Run linters on git staged files
* [insomnia](https://insomnia.rest/) Powerful HTTP and GraphQL tool belt

## Style guide

### Core ideology
WRITE SMALL, REUSABLE AND COMPOSABLE FUNCTIONS

### Code structure

* No duplicate file name in the whole application. Every file need to have a suffix to explain its type
> Why? It's easier to search for a file and reduce confusing of same file names

```bash
./src/modules/Login/
├── Login.lifecycle.tsx
├── Login.handler.tsx
├── Login.reducer.tsx
├── Login.screen.tsx
├── Login.selector.tsx
├── Login.view.tsx
```

* Organize your files around product features, not roles. Also, place your test files next to their implementation.
> Why? Instead of a long list of files, you will create small modules that encapsulate one responsibility including its test and so on. It gets much
easier to navigate through and things can be found at a glance.
* A separate directory for each component, module, higher order component,...
> Why? It's easier to extend and organize files. Make a change on a component won't affect to the structure of its parent directory

```bash
./src/components/
├── MenuItem/
├── MenuList/
├── LoadingMask/
└── UI/
```

* Only use index.{js|tsx?} for indexing (logic code is not allowed)
> Why? Using index files make it more comfortable to import files in a deep structure. However, putting logic code in it could end up being an
anti‑pattern which contains a hidden logic in an unexpected place.

* Every main (under ./src) directory must have a README file
> Why? Have no clue about how a directory is organized? What's the naming convention? How do things work together? Add a README to explain
them

* Put all export at the end
> Why? Randomly export variables, functions, interfaces,...is hard to keep track of what have been exported, especially in a large file

```js
// thousands of lines of code
...
export { myVar,myFunction, IMyInterface, MyTypeAlias }
export default myModule
```

### Code convention

* Use TSLint to enforce code style.

* Depending on the size of the task use //TODO: comments or open a ticket.
> Why? So then you can remind yourself and others about a small task (like refactoring a function or updating a comment). For larger tasks use
//TODO(#3456) which is enforced by a lint rule and the number is an open ticket.

* Always comment and keep them relevant as code changes. Remove commented blocks of code.
> Why? Your code should be as readable as possible, you should get rid of anything distracting. If you refactored a function, don't just comment out
the old one, remove it.

* Avoid irrelevant or funny comments, logs or naming.
> Why? While your build process may(should) get rid of them, sometimes your source code may get handed over to another company/client and
they may not share the same banter.

* Make your names search‑able with meaningful distinctions avoid shortened names. For functions use long, descriptive names. A function name
should be a verb or a verb phrase, and it needs to communicate its intention.
> Why? It makes it more natural to read the source code.

* Organize your functions in a file according to the step‑down rule. Higher level functions should be on top and lower levels below.
> Why? It makes it more natural to read the source code.

* We use Prettier with a pre‑commit hook to format code.
> Why? While prettier itself can be very powerful, it's not very productive to run it simply as a npm task alone each time to format code. This is
where lint-staged (and husky) come into play.

### Testing guidelines

* Place your test files next to the tested modules using a naming convention, like `componentName.component.test.tsx`.
> Why? You don't want to dig through a folder structure to find a unit test.

* Put your additional test files into a separate test folder to avoid confusion.
> Why? Some test files don't particularly relate to any specific implementation file. You have to put it in a folder that is most likely to be found by
other developers: `__test__` folder.

* Write testable code, avoid side effects, extract side effects, write pure functions
> Why? You want to test a business logic as separate units. You have to "minimize the impact of randomness and nondeterministic processes on the
reliability of your code". A pure function is a function that always returns the same output for the same input. Conversely, an impure function is one that may have side effects or depends on conditions from the outside to produce a value. That makes it less predictable.

* Run tests locally before making any pull requests to develop.
> Why? You don't want to be the one who caused production‑ready branch build to fail. Run your tests after your rebase and before pushing your
feature‑branch to a remote repository.

## Contributing guidelines
If you find any problems, please open an issue or submit a fix as a pull request.

We welcome new features, but for large changes let's discuss first to make sure the changes can be accepted and integrated smoothly.

### Git rules

* Perform work in a feature branch.
* Branch out from `master`
* Never push into `master`. Make a Pull Request.
* Update your local `master` branch and do an interactive rebase before pushing your feature and making a Pull Request.
* Resolve potential conflicts while rebasing and before making a Pull Request.
* Delete local and remote feature branches after merging.
* Before making a Pull Request, make sure your feature branch builds successfully and passes all tests (including code style checks).

### Writing good commit messages
* Separate the subject from the body with a newline between the two.
* Use the body to explain what and why as opposed to how.
* We use [validate‑commit](https://github.com/willsoto/validate-commit/blob/master/conventions/angular.md) (angular preset) to validate commit messages
