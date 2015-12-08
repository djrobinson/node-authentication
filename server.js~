
//get the tools used for the app

var express	= require('express');
var app 		= express();
var port 	= process.env.PORT || 8080;
var mongoose= require('mongoose');
var passport= require('passport');
var flash	= require('connect-flash');

var morgan			= require('morgan');
var cookieParser	= require('cookie-parser');
var bodyParser		= require('body-parser');
var session			= require('express-session');

var configDB	= require('./config/database.js');

//configuration

mongoose.connect(configDB.url); //connects db

require('./config/passport')(passport); // pass passport for configuration

//setup express app
app.use(morgan('dev')); //log every request to the console
app.use(cookieParser()); //read cookies for auth
app.use(bodyParser()); //get information from html forms

app.set('view engine', 'ejs'); //sets up ejs for templating

//passport configs
app.use(session({ secret: 'secretsecret' }));
app.use(passport.initialize());
app.use(passport.session()); //persisten login sessions
app.use(flash()); //use connect-flash for flash messages stored in session

//routes
require('./app/routes.js')(app, passport); //load routes and pass the configured passport

//starts the app
app.listen(port);
console.log('App is running on port ' + port);

