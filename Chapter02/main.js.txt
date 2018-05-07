var http = require('http');
var port = 8180;

var httpModule = require('./modules/http-module');

http.createServer(httpModule.handleRequest).listen(8180, '127.0.0.1', () => {
  console.log('Started Node.js http server at http://127.0.0.1:8180');
});
