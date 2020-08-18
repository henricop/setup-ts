# Setup project typescript

## Starting ( In this setup I'm using yarn but you can change all for npm)
```
- git init
- yarn init -y
```

## Now install typescript with development 
```
- yarn add typescript -D
- yarn tsc --init
```

## Some libraries require to install the typescript dependency
- express is the example
```
- yarn add @types/express
```

## Now for development install the "reload" typescript
```
yarn add ts-node-dev
```
- This dependency execute tsc, node and nodemon.
- tsc 👉 transpile the code **TS** in **JS**
- node 👉 the engine of the code **JS**
- nodemon 👉 monitors the code 

### Write the script bellow in your **package.json**

```
"script": {
  "dev": "ts-node-dev --respawn --transpileOnly --ignore-watch node_modules --no-notify src/server.ts"
}
```