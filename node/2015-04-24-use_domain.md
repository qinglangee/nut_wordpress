# use domain handle Exceptions


	var domain = require('domain');
	var d = domain.create();
	var fs = require('fs');

	d.on('error', function(err) {
	  console.error(err);
	});

	d.run(function() {
	  fs.readFile('somefile.txt', function (err, data) {
	    if (err) throw err;
	    console.log(data);
	  });
	});

console.log("Error: %s", er.stack || er.message)

uncaught exceptions should not happen. If they do use a program that restarts your entire application when its crashing (nodemon, forever, supervisor)


refs:  
[Uncaught Exceptions in Node.js](http://shapeshed.com/uncaught-exceptions-in-node/)  
[node-js-best-practice-exception-handling](http://stackoverflow.com/questions/7310521/node-js-best-practice-exception-handling)  
[官方exception指导](https://www.joyent.com/developers/node/design/errors)  
