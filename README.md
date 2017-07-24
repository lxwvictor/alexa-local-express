# Alexa-Local-Express
This is the testing bed of alexa apps running on local nodejs express server.
## Preparing the environments
1. Install node.js and npm
2. `npm install`
3. `node index.js` (Do note some platforms require elevated priviledge to bind port 443)
## Functions
### Open a webpage or any local files
A `openSthIntent` intent from Alexa will trigger a webpage or any local file.
Alternative way of testing can also be achieved by using `alexaApp.request()`.
```javascript
alexaApp.request(intentStr)
  .then(function(response) {
    console.log(JSON.stringify(response, null, 3));
  });
```
Reprompt function is included to ask user's next request. Answer "no", "nope" or "stop" will trigger the `AMAZON.StopIntent` to stop the session.
