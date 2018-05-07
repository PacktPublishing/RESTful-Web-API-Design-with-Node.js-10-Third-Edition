var expressApp = require('../../app');
var chai = require('chai');
var chaiHttp = require('chai-http');
var mongoose = require('mongoose');
var should = chai.should();


mongoose.createConnection('mongodb://localhost/catalog-test');

chai.use(chaiHttp);


describe('/get', function() {
  it('get test', function(done) {
    chai.request(expressApp)
      .get('/catalog/v2')
      .end(function(error, response) {
        should.equal(200  , response.status);
        done();
      });
    });
  });

describe('/post', function() {
     it('post test', function(done) {
       var item ={
      	"itemId":19,
          "itemName": "Sports Watch 10",
          "price": 100,
          "currency": "USD",
          "__v": 0,
          "categories": [
              "Watches",
              "Sports Watches"
          ]
      };
     chai.request(expressApp)
           .post('/catalog/v2')
           .send(item )
           .end(function(err, response){
               should.equal(201, response.status)
             done();
           });
     });
   });

   describe('/delete', function() {
        it('delete test', function(done) {
          var item ={
         	"itemId":19,
             "itemName": "Sports Watch 10",
             "price": 100,
             "currency": "USD",
             "__v": 0,
             "categories": [
                 "Watches",
                 "Sports Watches"
             ]
         };
        chai.request(expressApp)
              .delete('/catalog/v2/item/19')
              .send(item )
              .end(function(err, response){
                  should.equal(200, response.status)
                done();
              });
        });
      });
