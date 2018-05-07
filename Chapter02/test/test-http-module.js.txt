var sinon = require('sinon');
exports.handleGetRequestTest =  (test) => {
  var response = {'writeHead' : () => {}, 'end': () => {}};
var responseMock = sinon.mock(response);
   responseMock.expects('end').once().withArgs('Get action was requested');
   responseMock.expects('writeHead').once().withArgs(200, {
    'Content-Type' : 'text/plain'});

    var request = {};
    var requestMock = sinon.mock(request);
    requestMock.method = 'GET';

    var http_module = require('../modules/http-module');
    http_module.handleRequest(requestMock, response);
    responseMock.verify();
    test.done();
};
