# VS Code SCM API Instructions

Getting going with the API is surprisingly simple and of course pending your feedback we will work to make it even easier.

## The Basics
The SCM Extension you will create is just like any other extension for VS Code.  We have a good overview of [how to get going with a basic 'Hello World' extension](https://code.visualstudio.com/docs/extensions/example-hello-world) which covers off all of the tool chain (incl. debugging and self hosting) and the structure that is created around an extension. 

## Enabling the Preview API
The API is currently in a preview state (this will change in the next release - early April).  Preview API's have a few constraints:

1. They are only available in the Insiders build
2. They can't be packaged or published to the marketplace
3. There are some minor additional steps required for development time

### Change the VS Code Engine
In your `package.json` update the engine to be include the most recent version of VS Code.  This will ensure that API is available and that the extension cannot be installed on older versions of VS Code.

> Change `engines.vscode` to `^1.11.0`

### Acknowledge You want to use the Preview API
This will not be required once the API moves out of preview.  But we have it here to ensure extension authors understand that an API is not 'finished' yet.

> Add `"enableProposedAPI":true` to your `package.json`.

### Run `npm install`

### Add the Proposed API to your `src` folder
To get full IntelliSense and access to the API you need to copy in the latest version of the API File to our extensions `src` folder.

> Go grab the [latest version](https://raw.githubusercontent.com/Microsoft/vscode/master/src/vs/vscode.proposed.d.ts) and copy it in.



## Seeing other Implementations

It can be useful to review how others are adoption the API and there is [a list of repos and samples](https://github.com/Microsoft/vscode-SCMBuilders/wiki) to review.  We would love you to add a reference to any work you are doing to that list as well.

