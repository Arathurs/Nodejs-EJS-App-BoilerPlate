## App.js EJS Template Boilerplate for Node/MongoDB

#### [Link to Repo](https://github.com/Arathurs/Nodejs-EJS-App-BoilerPlate.git/)  

### About the Project

Boiler plate code for a Node App.js file which uses EJS for UI templates and connects to a MongoDB database. 

Note the use of the `serve_partials()` function in app.use to help our server look in the proper folder for template views.  

It can be found defined below the code used to tell our server where to find static files `app.use(express.static(path.join(__dirname, 'public')));`:

```
// uncomment after placing your favicon in /public
//app.use(favicon(path.join(__dirname, 'public', 'favicon.ico')));
app.use(logger('dev'));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));



function serve_partials (req, res) {
	var name = req.params.name;
	
	var requestedView = '../public/views/'+name;
	res.render(requestedView, function(err, ejs) {
		console.log('Looking for view partial ' +name);
		if (err) {
			res.render('404');
		} else {
			res.send(ejs);
		}
	});
}
```

Before being fed as the second argument to `app.use()` in the next line of code:

```
function serve_partials (req, res) {
	var name = req.params.name;
	
	var requestedView = '../public/views/'+name;
	res.render(requestedView, function(err, ejs) {
		console.log('Looking for view partial ' +name);
		if (err) {
			res.render('404');
		} else {
			res.send(ejs);
		}
	});
}

app.use('/views/:name', serve_partials);
```