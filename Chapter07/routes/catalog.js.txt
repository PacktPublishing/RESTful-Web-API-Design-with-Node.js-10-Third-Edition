const express = require('express');
const url = require('url');
const mongoose = require('mongoose');
const Grid = require('gridfs-stream');
const router = express.Router();
const CacheControl = require("express-cache-control")

const catalogV1 = require('../modules/catalogV1');
const catalogV2 = require('../modules/catalogV2');

const model = require('../model/item.js');

var cache = new CacheControl().middleware;

router.get('/v1/', function(request, response, next) {
  catalogV1.findAllItems(response);
});

router.get('/v1/item/:itemId', function(request, response, next) {
  console.log(request.url + ' : querying for ' + request.params.itemId);
  catalogV1.findItemById(request.params.itemId, response);
});



router.get('/v1/:categoryId', function(request, response, next) {
  console.log(request.url + ' : querying for ' + request.params.categoryId);
  catalogV1.findItemsByCategory(request.params.categoryId, response);
});

router.post('/v1/', function(request, response, next) {
  catalogV1.saveItem(request, response);
});

router.put('/v1/', function(request, response, next) {
  catalogV1.saveItem(request, response);
});

router.put('/v1/:itemId', function(request, response, next) {
  catalogV1.saveItem(request, response);
});

router.delete('/v1/item/:itemId', function(request, response, next) {
  catalogV1.remove(request, response);
});

router.get('/v2/:categoryId', function(request, response, next) {
  console.log(request.url + ' : querying for ' + request.params.categoryId);
  catalogV2.findItemsByCategory(request.params.categoryId, response);
});

router.get('/v2/item/:itemId', function(request, response, next) {
  console.log(request.url + ' : querying for ' + request.params.itemId);
  var gfs = Grid(model.connection.db, mongoose.mongo);

  catalogV2.findItemById(gfs, request, response);
});

router.post('/v2/', function(request, response, next) {
  catalogV2.saveItem(request, response);
});

router.put('/v2/', function(request, response, next) {
  catalogV2.saveItem(request, response);
});

router.put('/v2/:itemId', function(request, response, next) {
  catalogV1.saveItem(request, response);
});

router.delete('/v2/item/:itemId', function(request, response, next) {
  catalogV2.remove(request, response);
});

router.get('/', function(request, response) {
  console.log('Redirecting to v2');
  response.writeHead(302, {'Location' : '/catalog/v2/'});
  response.end('Version 2 is is available at /catalog/v2/: ');
});

router.get('/v2/', cache('minutes', 1), function(request, response) {
    var getParams = url.parse(request.url, true).query;
    if (getParams['page'] !=null || getParams['limit'] != null) {
      catalogV2.paginate(model.CatalogItem, request, response);
    } else {
      var key = Object.keys(getParams)[0];
      var value = getParams[key];
      catalogV2.findItemsByAttribute(key, value, response);
    }
});

router.get('/v2/item/:itemId/image',
  function(request, response){
    var gfs = Grid(model.connection.db, mongoose.mongo);
    catalogV2.getImage(gfs, request, response);
});

router.get('/item/:itemId/image',
  function(request, response){
    var gfs = Grid(model.connection.db, mongoose.mongo);
    catalogV2.getImage(gfs, request, response);
});

router.post('/v2/item/:itemId/image',
  function(request, response){
    var gfs = Grid(model.connection.db, mongoose.mongo);
    catalogV2.saveImage(gfs, request, response);
});

router.post('/item/:itemId/image',
  function(request, response){
    var gfs = Grid(model.connection.db, mongoose.mongo);
    catalogV2.saveImage(gfs, request.params.itemId, response);
});

router.put('/v2/item/:itemId/image',
  function(request, response){
    var gfs = Grid(model.connection.db, mongoose.mongo);
    catalogV2.saveImage (gfs, request.params.itemId, response);
});

router.put('/item/:itemId/image',
function(request, response){
  var gfs = Grid(model.connection.db, mongoose.mongo);
  catalogV2.saveImage(gfs, request.params.itemId, response);
});

router.delete('/v2/item/:itemId/image',
function(request, response){
  var gfs = Grid(model.connection.db, mongoose.mongo);
  catalogV2.deleteImage(gfs, model.connection,
  request.params.itemId, response);
});

router.delete('/item/:itemId/image',
function(request, response){
  var gfs = Grid(model.connection.db, mongoose.mongo);
  catalogV2.deleteImage(gfs, model.connection,  request.params.itemId, response);
});

module.exports = router;
