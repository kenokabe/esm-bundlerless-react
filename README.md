

# esm-bundlerless-react

ESM (ES6 Modules) Bundlerless Front-end Development tool

ESM (ES6 Modules)  simplifies JavaScript application development since there is no need to bundle on deploy, modules works as it is on browsers.

**This article will show you how you can develop and deploy JavaScript front-end applications with ES modules in the browser today without bundlers such as webpack/Browserify.**

This project provides a basic concept and a minimal prototype with React.  
*It's recommended to read https://github.com/kenokabe/esm-bundlerless for the most simple project without React prior to this article.*


## ES6 Modules support in modern browsers today
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#Browser_compatibility

![compati.png](https://kenokabetech.github.io/img/ts-react-electron/compati.png)

## Robust dependencies

- [TypeScript 3.0](https://www.typescriptlang.org/)  
For React JSX applications, there is a need to transpile JSX to vanilla JavaScript, and until now we needed to use webpack+babel, that has been a very complicated setup.  
Amazingly TypeScript has an ability to transpile JSX(TSX) to JS.  Hence, as long as sticking to TypeScript, another transpiler such as babel is not necessary.  

**index.tsx**  
![Screenshot from 2018-08-19 16-41-42.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-41-42.png)  
**index.js**  
![Screenshot from 2018-08-19 16-42-15.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-42-15.png)

- [Electron 3.0](https://electronjs.org/)  
Electron is built on Chromium and Node.js technology, so it's a hybrid environment of both web browser and local node runtime.  
Therefore, with Electron, I presume anything can be done, however, the fact is there is some issue to take advantage of ESM - [Issue: Contexts: supporting new Node's ESM Loader (without hacking)](https://github.com/electron/node/issues/33)  
While I commented there, the member of the team of Electron and the developer of [lodash](https://www.npmjs.com/package/lodash) replied on me to suggest to use [esm](https://www.npmjs.com/package/esm) library that is his another brilliant work, and that technically resolved the issue.  

![esm-dependency.png](https://kenokabetech.github.io/img/ts-react-electron/esm-dependency.png)

With React,  
![Screenshot from 2018-08-19 16-52-56.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-52-56.png)


- [Visual Studio Code ](https://code.visualstudio.com/)  
I highly recommend using Visual Studio Code than any other IDE including AtomEditor(by GitHub).  
VisualStudio code is optimized to use TypeScript out of the box, and in fact, VisualStudio Code is purely developed in TypeScript(Anders Hejlsberg explained so in some Microsoft keynote.)    
VisualStudio Code is developed by Microsoft and build on Electron, and it's one of the reasons Microsoft acquired GitHub. Electron is originally a core unit of AtomEditor developed by GitHub, so essentially, Electron is now Microsoft's asset.  
Very interestingly, all tools, TypeScript, Electron and VisualStudio Code are maintained by Microsoft. 

## TypeScript to JavaScript on save

The most of the work is done by TypeScript transpiler
[tsc --watch option](https://www.typescriptlang.org/docs/handbook/compiler-options.html)
>Run the compiler in watch mode. Watch input files and trigger recompilation on changes. The implementation of watching files and directories can be configured using environment variable. See [configuring watch](https://www.typescriptlang.org/docs/handbook/configuring-watch.html) for more details.
>
![Screenshot from 2018-08-19 16-48-09.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-48-09.png)
![Screenshot from 2018-08-19 16-46-44.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-46-44.png)

## This tool adds the `.js` file extension to the end of module specifiers in TypeScript transpile
https://github.com/Microsoft/TypeScript/issues/16577

![esm-src.png](https://kenokabetech.github.io/img/ts-react-electron/esm-ts.png)

![esm-src.png](https://kenokabetech.github.io/img/ts-react-electron/esm-js.png)

## This tool maps the npm library to the ESM path in TypeScript transpile

![Screenshot from 2018-08-19 16-43-39.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-43-39.png)

Since React developers currently depend on webpack/browserify. React16.* has not released ESM version, but probably in ver17, so I obtained ESM version by myself.  
React npm packages are necessary either way because TypeScript @types needs them.  
On deployment, the npm dependency should be replaced to the native esm react modules, so here we need to map the ESM path.

TypeScript transpile process does not support this maping feature. See:

https://github.com/Microsoft/TypeScript/issues/16640

https://github.com/Microsoft/TypeScript/issues/10866


## Automatic reload and clean console log in a child window of Electron

![Screenshot_00.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot_00.png)

![enter image description here](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-41-05.png)

## Deploy

![Screenshot from 2018-08-19 16-46-44.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-46-44.png)

The `dist` directory with `index.html` can be exported and it should work on modern browsers. 

https://kenokabetech.github.io/demo/esm-bundlerless-react/dist/index.html

![dist-react](https://kenokabetech.github.io/img/ts-react-electron/reactdeploy.png)



Firefox should be able to run the local `dist/index.html` file directly with no problem, Chrome generates an error with a security issue.

 ## Use the latest TypeScript version installed in the local project not global

It's a good manner to install typescript npm package 
- not to global  
`npm install -g typescript`  
- but to local --save-dev.  
`npm install -D typescript`


In VisualStudio Code, by clicking the TypeScript Version, it's easy to switch to use the project local(WorkSpace) installed version.

![Screenshot from 2018-08-19 16-55-15.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2016-55-15.png)

 
![Screenshot from 2018-08-19 17-05-21.png](https://kenokabetech.github.io/img/ts-react-electron/Screenshot%20from%202018-08-19%2017-05-21.png) 
  


 