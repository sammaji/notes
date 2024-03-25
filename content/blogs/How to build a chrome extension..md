## Parts of a chrome extension
Before trying to build anything, let's try to understand the different parts of a chrome extension.
### manifest.json
The `manifest.json` file is the configuration file for your browser extension. Here, we specify all the information your browser needs to run your extensions, like, location of assets, permissions, when to run a script, etc.
### Service Workers
Service workers are scripts that run in the background. They can listen to events and performs tasks but they cannot directly interact with the contents of a web page. They can use all chrome apis except the browser api.
### Content Scripts
They execute JavaScript, read and modify dom, etc in a web page.
### Popup Page
The page that shows up when you click on your extension. They too can access all the chrome apis.

## Loading extension
https://developer.chrome.com/docs/extensions/mv3/getstarted/development-basics/#load-unpacked
1. Go to your browser and click on the extension tab.
2. Enable developer mode.
3. Click on "Load Unpacked" and open the `dist` folder of your project as that is where our generated `manifest.json` will live.