var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var itemSchema = new Schema ({
    "itemId" : {type: String, index: {unique: true}},
    "itemName": String,
    "price": Number,
    "currency" : String,
    "categories": [String]
});

var CatalogItem = mongoose.model('Item', itemSchema);

mongoose.connect('mongodb://localhost/catalog');
var db = mongoose.connection;

db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  var watch = new CatalogItem({
    itemId: 9 ,
    itemName: "Sports Watch1",
    brand: 'А1',
    price: 100,
    currency: "EUR",
    categories: ["Watches", "Sports Watches"]
  });
    watch.save((error, item, affectedNo)=> {
      if (!error) {
        console.log('Item added successfully to the catalog');
      } else {
        console.log('Cannot add item to the catlog');
      }
    });
});

db.once('open', function() {
  var filter = {
    'itemName' : 'Sports Watch1',
    'price': 100
  }
  
  CatalogItem.find(filter, (error, result) => {
    if (error) {
      consoloe.log('Error occured');
    } else {
      console.log('Results found:'+ result.length);
      console.log(result);
    }
  });
});

db.once('open', function() {
  var filter = {
    'itemName' : 'Sports Watch1',
    'price': 100
  }
  CatalogItem.findOne(filter, (error, result) => {
    if (error) {
      consoloe.log('Error occured');
    } else {
      console.log(result);
    }
  });
});
