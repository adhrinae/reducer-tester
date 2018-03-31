# reducer-tester

[![Build Status](https://travis-ci.org/akameco/reducer-tester.svg?branch=master)](https://travis-ci.org/akameco/reducer-tester)
[![tested with jest](https://img.shields.io/badge/tested_with-jest-99424f.svg)](https://github.com/facebook/jest)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
[![All Contributors](https://img.shields.io/badge/all_contributors-1-orange.svg?style=flat-square)](#contributors)

> reducer tester

## Install

```
$ yarn add --dev reducer-tester
```

## Usage

```js
// reducer.js
export const initialState = { count: 0, other: 'other' }

export default (state = initialState, action) => {
  switch (action.type) {
    case 'inc':
      return { ...state, count: state.count + 1 }
    case 'dec':
      return { ...state, count: state.count - 1 }
    default:
      return state
  }
}

// reducer.test.js
import reducerTester from 'reducer-tester'
import reducer, { initialState } from './reducer'

reducerTester({
  reducer,
  state: initialState,
  tests: [{ type: 'inc' }, { type: 'dec' }],
})
```

### Snapshot

```diff
// Jest Snapshot v1, https://goo.gl/fbAQLP

exports[`handle initial state 1`] = `
"Snapshot Diff:
Compared values have no visual difference."
`;

exports[`dec 1`] = `
"Snapshot Diff:
- Before
+ After

  Object {
-   "count": 0,
+   "count": -1,
    "other": "other",
  }"
`;

exports[`inc 1`] = `
"Snapshot Diff:
- Before
+ After

  Object {
-   "count": 0,
+   "count": 1,
    "other": "other",
  }
`;
```

## Full example

```js
import reducerTester from 'reducer-tester'
import reducer, { initialState } from './reducer'

reducerTester({
  reducer, // #required
  state: initialState, // #required
  tests: [{ type: 'inc' }, { type: 'dec' }], // #required
  initialTest: false, // # optional, default: true
  titlePrefix: 'handle ', // # optional, default: ''
})
```

```diff
// Jest Snapshot v1, https://goo.gl/fbAQLP

exports[`handle dec 1`] = `
"Snapshot Diff:
- Before
+ After

  Object {
-   "count: 0,
+   count: -1,
  }
`;

exports[`handle inc 1`] = `
"Snapshot Diff:
- Before
+ After

  Object {
-   count: 0,
+   count: 1,
  }
`;
```

### Tips

#### Atom Editor User

Install `language-diff` and `file-types`. And open `config.json` and edit as blow.

```cson
"*":
  "file-types":
    "\\.js\\.snap$": "source.diff"
```

Hooray! Very readable!

[![https://gyazo.com/3b9bda2abe162d0232c73ae49ab4dc4d](https://i.gyazo.com/3b9bda2abe162d0232c73ae49ab4dc4d.png)](https://gyazo.com/3b9bda2abe162d0232c73ae49ab4dc4d)

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->

<!-- prettier-ignore -->
| [<img src="https://avatars2.githubusercontent.com/u/4002137?v=4" width="100px;"/><br /><sub>akameco</sub>](http://akameco.github.io)<br />[💻](https://github.com/akameco/reducer-tester/commits?author=akameco "Code") [📖](https://github.com/akameco/reducer-tester/commits?author=akameco "Documentation") [⚠️](https://github.com/akameco/reducer-tester/commits?author=akameco "Tests") [🚇](#infra-akameco "Infrastructure (Hosting, Build-Tools, etc)") |
| :---: |

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification. Contributions of any kind welcome!

## License

MIT © [akameco](http://akameco.github.io)
