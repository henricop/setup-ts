# Setup project typescript 🔄🆕
<img align="justify"  src="https://img.shields.io/static/v1?label=node&message=LTS&color=green&style=for-the-badge&logo=node.js"/>
<img  align="justify" src="https://img.shields.io/static/v1?label=react&message=LTS&color=blue&style=for-the-badge&logo=react"/>
<img align="justify"  src="https://img.shields.io/static/v1?label=javascript&message=LTS&color=yellow&style=for-the-badge&logo=javascript"/>
<img align="justify" src="https://img.shields.io/static/v1?label=typescript&message=LTS&color=blue&style=for-the-badge&logo=typescript"/>
<img align="justify" src="https://img.shields.io/static/v1?label=babel&message=LTS&color=yellow&style=for-the-badge&logo=babel"/>
<img align="justify" src="https://img.shields.io/static/v1?label=jest&message=LTS&color=blue&style=for-the-badge&logo=jest"/>
<img align="justify" src="https://img.shields.io/static/v1?label=eslint&message=LTS&color=blue&style=for-the-badge&logo=eslint"/>

![TS CONFIG NODE](./assets/tsnode.svg)

<p align="justify">This document is to start your and my projects</p>

### Starting ( In this setup I'm using yarn but you can change all for npm) ✅
```
- git init
- yarn init -y
```

### Now install typescript with development  ✅
```
- yarn add typescript -D
- yarn tsc --init
```

### Some libraries require to install the typescript dependency ✅
- express is the example
```
- yarn add @types/express
```

### Now for development install the "reload" typescript ✅
```
yarn add ts-node-dev
```
- This dependency execute tsc, node and nodemon.
- tsc 👉 transpile the code **TS** in **JS**
- node 👉 the engine of the code **JS**
- nodemon 👉 monitors the code 

### Write the script bellow in your **package.json** 🔽 ✅

```
"script": {
  "dev": "ts-node-dev --respawn --transpileOnly --ignore-watch node_modules --no-notify src/server.ts"
}
```
### Now on ```tsconfig.json``` ✅
The transpile code must go to a separate folder for production
- modify **outDir** and **rootDir**
```
"outDir": "./dist"
"rootDir": "./src"
```
- You must verify your "**target**", the node can use **JS** version **es2017** and by default **TS** use **Vanilla JS**
- ```"removeComments": true``` 👉 remove all comments on building process 
- Other amazing target is :  ```"resolveJsonModule": true``` 👉 this function allows you import json into the code

# Config ESLINT 🆕

**ESLint** is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code, with the goal of making code more consistent and avoiding bugs

### Starting ✅

```
yarn add eslint 
yarn eslint --init
```

The Eslint gives to you many options, choose the makes more sense for you.

Me 👉 **airbnb**

Them, he gives you many options for plugins you must install, but the tool gives only install for ```npm``` and I using **yarn**, so we need just copy the code and write on terminal with **yarn add**

# Config Jest 🆕

**Jest** is a **JS** testing framework designed to ensure correctness of any **JS** codebase.

### Starting ✅

```
yarn add jest -D
yarn jest --init 
```
- the init gives you options, I choose ```(yes,node,no,yes)``` ever 
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

### Into ```eslintrc.json``` must added 🔽 ✅
  ```
  "env": {
    "es2020": true,
    "node": true,
    "jest": true
  }
  ```

# Config BABEL 🆕

**Babel** is a **JS** compile. Is a tool that helps you write code in the latest version of javascript

### Starting

```
yarn add -D @babel/cli @babel/core @babel/node @babel/preset-env @babel/preset-typescript babel-plugin-module-resolver
```
- Make a new file with name 👉 ```babel.config.js``` and add configurations bellow 🔽
```
module.exports = {
  presets: [
    [
      '@babel/preset-env',
      {
        targets: {
          node: 'current'
        }
      }
    ],
    '@babel/preset-typescript'
  ],
  plugins: [
    ['module-resolver', {
      alias: {
        '@modules': './src/modules',
        '@core': './src/core',
        '@shared': './src/shared',
        '@infra': './src/infra',
      }
    }]
  ],
  ignore: [
    '**/*.spec.ts'
  ]
}
```

### Now in package.json we need create a script of build, into "scripts"
```
"scripts": {
  "build": "babel src --extensions \*.js,.ts\* --out-dir dist --copy-files --no-copy-ignored",
}
```
# Lastly we make the script for run in production

```"start": "node dist/server.js"```