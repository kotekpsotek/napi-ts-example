# Show how to import N-API Node.js modules within TypeScript EsModule syntax
Exists the differences between CommonJS and ES-Modules syntax especially when you'd like to leverage native-like performance node.js modules:
1. For import CommonJS uses the require("src") function which is able to recognize the ".node" existension modules (Native Node.js Modules), js and mjs files
2. ES-Modules uses the import * from "src" which is only able to catch: ".mjs", ".js" (when you've settled allowJs as true) and ".ts"

## **Prerequsites**
1. ``tsconfig.json`` file should have:
```json
    {
        "module": "CommonJS", // Says that output will be CommonJS, thing with whose node.js is coping
    }
```
> Without this setting your node.js project won't work

## Define what are the rules:
- The rule of TypeScript is to provide you explicit type awareness for project, it's not runtime, which in this case is node.js. Therefore you know, your trouble is backed in typing
- The rule of Node.js is to run your code. To make TypeScript output executable for Node.js, the output of TypeScript have to be ``CommonJS JavaScript files-set``

## Trouble Shot
Here I will explain you, the way to solve your issue with code snippets:

1. **Copy and paste** ``.node`` file to your project, (if you already have, bypass step)
2. **Make** ```index.node.d.ts``` file in same location as is your ``.node`` file. Write within syntax:
```ts
    export function hello(): string;
```
- In this file you specify types for your TypeScript purpose therefore this should be in such raw form, 
3. **Turn to your import location** and use such apporach:
```ts
    import { hello } from "../index.node" // It's location to your .node file. When is different, change

    console.log(hello())
```
- **Solved!!!** Now you'll have clear output without any trouble

> ### How does it work?
TypeScript to successfull transiple your code have to have full correctness, means also correct with types. Prior wasn't able to see typings, now is.
**You should approach to this trouble as to force TypeScript to make doesn't know stuff for him thankfully to its fooliness**


### Project Directory content
```
-- src - folder with import location
    -- main.ts - import location
index.node - native node.js component
index.node.d.ts - tricky file which restore your gut
```
