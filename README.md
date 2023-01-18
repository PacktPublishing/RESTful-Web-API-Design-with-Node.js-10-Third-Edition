


# RESTful Web API Design with Node.js 10 - Third Edition
This is the code repository for [RESTful Web API Design with Node.js 10 - Third Edition](https://www.packtpub.com/web-development/restful-web-api-design-nodejs-10-third-edition?utm_source=github&utm_medium=repository&utm_campaign=9781788623322), published by [Packt](https://www.packtpub.com/?utm_source=github). It contains all the supporting project files necessary to work through the book from start to finish.
## About the Book
This book targets developers who want to enrich their development skills by learning how
to develop scalable, server-side, RESTful applications based on the Node.js platform. You
also need to be aware of HTTP communication concepts and should have a working
knowledge of the JavaScript language. Keep in mind that this is not a book that will teach
you how to program in JavaScript. Knowledge of REST will be an added advantage but is
definitely not a necessity.
## Instructions and Navigation
All of the code is organized into folders. Each folder starts with a number followed by the application name. For example, Chapter02.



The code will look like the following:
```
router.get('/v1/item/:itemId', function(request, response, next) {
 console.log(request.url + ' : querying for ' + request.params.itemId);
 catalogV1.findItemById(request.params.itemId, response);
});
router.get('/v1/:categoryId', function(request, response, next) {
 console.log(request.url + ' : querying for ' +
request.params.categoryId);
 catalogV1.findItemsByCategory(request.params.categoryId, response);
});
```

## Related Products
* [Mastering Node.js - Second Edition](https://www.packtpub.com/web-development/mastering-nodejs-second-edition?utm_source=github&utm_medium=repository&utm_campaign=9781785888960)

* [Learning Node.js Development](https://www.packtpub.com/web-development/learning-nodejs-development?utm_source=github&utm_medium=repository&utm_campaign=9781788395540)
### Download a free PDF

 <i>If you have already purchased a print or Kindle version of this book, you can get a DRM-free PDF version at no cost.<br>Simply click on the link to claim your free PDF.</i>
<p align="center"> <a href="https://packt.link/free-ebook/9781788623322">https://packt.link/free-ebook/9781788623322 </a> </p>