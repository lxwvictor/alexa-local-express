# Alexa-Local-Express
This is the testing bed of alexa apps running on local nodejs express server.
## Preparing the environments
1. Install node.js and npm
2. `npm install`
3. https is mandatory for Alexa calls. Below is simple guide on creating self-signed certificate.
`// create a self signed cert
openssl req -x509 -newkey rsa:2048 -sha256 -exfile v3.ext -keyout key.pem -out cert.pem -days 3650
openssl rsa -in key.pem -out newkey.pem && mv newkey.pem key.pem

// create a local CA and use it to sign cert
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 2048 -out rootCA.pem
sudo openssl req -new -sha256 -nodes -out server.csr -newkey rsa:2048 -keyout server.key -config csr.cnf
sudo openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 500 -sha256 -extfile v3.ext
openssl x509 -text -in server.crt -noout

// create a pfx file from the crt and key files
openssl pkcs12 -export -out domain.name.pfx -inkey domain.name.key -in domain.name.crt`
4. `node index.js` (Do note some platforms require elevated priviledge to bind port 443)
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
