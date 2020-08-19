# Setup project typescript

![TS CONFIG NODE](https://raw.githubusercontent.com/TypeStrong/ts-node/HEAD/logo.svg?sanitize=true);

### Starting ( In this setup I'm using yarn but you can change all for npm)
```
- git init
- yarn init -y
```

### Now install typescript with development 
```
- yarn add typescript -D
- yarn tsc --init
```

### Some libraries require to install the typescript dependency
- express is the example
```
- yarn add @types/express
```

### Now for development install the "reload" typescript
```
yarn add ts-node-dev
```
- This dependency execute tsc, node and nodemon.
- tsc 👉 transpile the code **TS** in **JS**
- node 👉 the engine of the code **JS**
- nodemon 👉 monitors the code 

### Write the script bellow in your **package.json** 🔽

```
"script": {
  "dev": "ts-node-dev --respawn --transpileOnly --ignore-watch node_modules --no-notify src/server.ts"
}
```
### Now on ```tsconfig.json```
The transpile code must go to a separate folder for production
- modify **outDir** and **rootDir**
```
"outDir": "./dist"
"rootDir": "./src"
```
- You must verify your "**target**", the node can use **JS** version **es2017** and by default **TS** use **Vanilla JS**
- ```"removeComments": true``` 👉 remove all comments on building process 
- Other amazing target is :  ```"resolveJsonModule": true``` 👉 this function allows you import json into the code

# Config ESLINT

**ESLint** is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code, with the goal of making code more consistent and avoiding bugs

### Starting

```
yarn add eslint 
yarn eslint --init
```

The Eslint gives to you many options, choose the makes more sense for you.

Me 👉 **airbnb**

Them, he gives you many options for plugins you must install, but the tool gives only install for ```npm``` and I using **yarn**, so we need just copy the code and write on terminal with **yarn add**

# Config Jest

**Jest** is a **JS** testing framework designed to ensure correctness of any **JS** codebase.

### Starting

```
yarn add jest -D
yarn jest --init (yes,node,no,yes)
```
- To default Jest don't work with **TS** so we need instals other plugin

```
yarn add ts-jest -D
yarn add @types/jest -D
```
- Into ```jest.config.js``` we need changed the **preset**
```
const { compilerOptions} = require('./tsconfig.json');

preset: 'ts-jest';
```

### Into ```eslintrc.json``` must added:
  ```
  "env": {
    "es2020": true,
    "node": true,
    "jest": true
  }
  ```

# Config BABEL

**Babel** is a **JS** compile. Is a tool that helps you write code in the latest version of javascript

### Starting

```
yarn add -D @babel/cli @babel/core @babel/node @babel/preset-env @babel/preset-typescript babel-plugin-module-resolver
```
- Make a new file with name 👉 ```babel.config.js``` and add configurations bellow 🔽