HOW TO CREATE A EXPRESS APP
Open terminal
Express app_name --hbs --css sass
(2)Cd app_name
npm install gitignore -g (if you don't have gitignore installed globally)
(3)Gitignore node
(4)Npm install
	-Installs dependencies
SET UP KNEX, PG, BOOKSHELF(if wanted)
(5)npm install knex pg dotenv bookshelf --save
-Installs dotenv module and adds to the dependencies in package.json(this loads the environment variables)Installs pg and knex and add them to the dependencies in the package.json
(6)Knex init
	-Creates knexfile.js
(7)Git init
-Initialize git repo
(8)Echo node_modules > .gitignore
		-moves node modules to a .gitignore file
(9)Touch .env 	 
	-Makes a empty .env file in the root directory
(10)echo .env >> .gitignore
		-adds .env file to .gitignore so git doesn't track it
(11)Npm init
	-make sure that in package.json your start is on ./bin/www
(12)Atom .
	-open atom

(13)Change knexfile.js
require('dotenv').config();
module.exports = {
  	development: {
   	 client: 'pg',
    	connection: 'postgres://localhost/DATABASE_NAME'
 	 },
 	 production:{
    	client: 'pg',
    	connection: process.env.DATABASE_URL + '?ssl=true'
  	}
};



(14)Create directory called db
(15)Makefile knex.js
	(16)-Add to knex.js
		var environment = process.env.NODE_ENV || 'development';
var config = require('../knexfile')[environment];
var knex = require('knex')(config);
module.exports= knex;

		(17)-Go into index.js and add in
var knex=require('../db/knex');
var pg = require('pg');


SASS SETUP
In view go to view/layout.hbs add in cdn for css reset
<link href="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.css"/>
	-to use sass go into app.js and change indentedSyntax to  false (line 26)
	-in public/stylesheets make a new file called style.css
	-make new files as needed called style.scss  and  @import ‘otherfilename’;
Such as font.scss color.scss


SETTING UP DATABASE
Open Terminal
Createdb db_name
	-go into knexfile.js and add database name to development connection
		(connection: 'postgres://localhost/DATABASE NAME YOU JUST CREATED')
Knex migrate:make table_name
	exports.up = function(knex, Promise) {
 		 return knex.schema.createTable(table_name, function(table){
   		 table.increments();
   		 table.string(‘column_name’);
   	 	table.text('column_name');
table.boolean(name);
table.integer(‘column_name’).references('table_referance’');
 	 	});
};
exports.down = function(knex, Promise) {
 	 	return knex.schema.dropTableIfExists(‘table_name’);
};

Knex migrate:latest
Adds tables to your database
Knex seed:make 0_seed_name
	-start with reset seed
exports.seed = function(knex, Promise) {
   		 	return knex(table.name).del()
    		.then(function(){
    			return knex(table_name).del()
   		 .then(function(){
      		return knex(table_name).del()
  	 	 })
 	 	})
};
-Add in a number so the seeds will run in order
Knex seed:run
	-adds data to your table



HEROKU SETUP
Git add .
Git commit -m “message”
heroku create app-name
heroku addons:create heroku-postgresql
heroku config
Add url to .env
-DATABASE_URL=heroku url
knex migrate:latest --env production
	-runs the latest migration to heroku
knex seed:run --env production
	-runs the latest seed to your production
git push heroku master
	-push master branch to heroku
heroku open









 
