var math = require('../modules/math');
exports.addTest = function (test) {
  test.equal(math.add(1, 1), 3);
  test.done();
};
exports.subtractTest = function (test) {
  test.equals(math.subtract(4,2), 2);
  test.done();
};
