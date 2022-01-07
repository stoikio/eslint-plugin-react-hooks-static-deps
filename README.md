# eslint-plugin-react-hooks-static-deps

<a href="https://www.npmjs.com/package/eslint-plugin-react-hooks-static-deps" target="_blank">
  <img src="https://img.shields.io/npm/v/eslint-plugin-react-hooks-static-deps?" alt="npm version" height="18">
</a>

A custom ESLint rule to allow static deps in React Hooks ⚛️

## Motivation

`react-hooks/exhaustive-deps` is a really nice ESLint rule to avoid forgetting dependencies in React hoks like `useCallback` and `useMemo`.

However, it can become really annoying, especially when you know that one of the "missing" dependencies comes from a custom hook you wrote, and whose return value won't change (if it's a function for example).

**This package allows you to declare which hooks return values should be ignored in `exhaustive-deps` checks.**

## Installation

```sh
npm i -D eslint-plugin-react-hooks-static-deps
```
or
```sh
yarn add -D eslint-plugin-react-hooks-static-deps
```

## Usage

1. Add the plugin to your ESLint config file :
```js
{
  ...
  plugins: [... , "react-hooks-static-deps"]
  ...
}
```

2. To avoid conflicts, disable React's default `exhaustive-deps` rule if you use it :
```js
{
  ...
  rules: {
    ...
    "react-hooks/exhaustive-deps": "off",
    ...
  }
  ...
}
```

3. Define which hooks return static values. Example :
```js
{
  ...
  rules: {
    ...
    "react-hooks-static-deps/exhaustive-deps": [
      "warn", // or "error"
      {
        staticHooks: {
          // the whole return value of the hook will be considered static
          useHook: true,

          // for hooks that return an array: here only the second item return by the hook will be considered static
          useArrayHook: [false, true],

          // for hooks that return an object: here only the property prop1 will be considered static
          useObjectHook : {
            prop1: true,
            prop2: false
          }
        }
      }
    ],
    ...
  }
  ...
}
```