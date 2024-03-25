## Parts of a chrome extension
> More info: https://developer.chrome.com/docs/extensions/mv3/architecture-overview/
### manifest.json
manifest records important metadata, defines resources, declares permissions, and identifies which files to run in the background and on the page, etc.

### service workers
Listens to events and performs tasks. It can use all chrome apis but not the browser apis (it cannot directly interact with the contents of a webpage).

### content scripts
They execute javascript, read and modify dom, etc in a web page.

### additional pages
-> popup page
-> options page
All these pages have access to the chrome api

## Loading extension
https://developer.chrome.com/docs/extensions/mv3/getstarted/development-basics/#load-unpacked