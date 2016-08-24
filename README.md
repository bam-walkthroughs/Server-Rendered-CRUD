## HOW TO CREATE A EXPRESS APP

- (1) Open terminal
- (2) Express app_name --hbs --css sass
- (3) Cd app_name
- (4) npm install gitignore -g (if you don't have gitignore installed globally)
- (5)Gitignore node
- (6) Npm install
	 - -this will Installs dependencies

##SET UP KNEX, PG, BOOKSHELF(if wanted)
- (7)npm install knex pg dotenv bookshelf --save
 - -this Installs dotenv module and adds to the dependencies in package.json(this loads the environment variables)Installs pg and knex and add them to the dependencies in the package.json
- (8)Knex init
	- -Creates knexfile.js
- (9)Git init
 - -Initialize git repo
- (10)Echo node_modules > .gitignore
	-	-moves node modules to a .gitignore file
- (11)Touch .env 	 
	- -Makes a empty .env file in the root directory
- (12)echo .env >> .gitignore
	- 	-adds .env file to .gitignore so git doesn't track it
- (14) Npm init
	- -make sure that in package.json your start is on ./bin/www
- (15)Atom .
	- -open atom

- (16)Change knexfile.js
```require('dotenv').config();
module.exports = {
  	development: {
   	 client: 'pg',
    	connection: 'postgres://localhost/DATABASE_NAME'
 	 },
 	 production:{
    	client: 'pg',
    	connection: process.env.DATABASE_URL + '?ssl=true'
  	}
};```



- (17)Create directory called db
- (18)Makefile knex.js
-	-Add to knex.js

	```	var environment = process.env.NODE_ENV || 'development';
var config = require('../knexfile')[environment];
var knex = require('knex')(config);
module.exports= knex;```

	-	(19)-Go into index.js and add in

```var knex=require('../db/knex');
var pg = require('pg');```


## SASS SETUP
- (1) In view go to view/layout.hbs add in cdn for css reset
```<link href="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.css"/>```
-	-to use sass go into app.js and change indentedSyntax to  false (line 26)
-	-in public/stylesheets make a new file called style.css
-	-make new files as needed called style.scss  and  @import ‘otherfilename’;
Such as font.scss color.scss


## SETTING UP DATABASE
- (1) Open Terminal
- (2) Createdb db_name
- (3) go into knexfile.js and add database name to development connection
		```(connection: 'postgres://localhost/DATABASE NAME YOU JUST CREATED')```
- ```Knex migrate:make table_name
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
};```

- (4) Knex migrate:latest
- -this adds tables to your database
```Knex seed:make 0_seed_name
	-start with reset seed
exports.seed = function(knex, Promise) {
   		 	return knex(table.name).del()
    		.then(function(){
    			return knex(table_name).del()
   		 .then(function(){
      		return knex(table_name).del()
  	 	 })
 	 	})
};```
-Add in a number so the seeds will run in order
- (5) Knex seed:run
-	-this adds data to your table



## HEROKU SETUP
- in terminal
- (1) Git add .
- (2) Git commit -m “message”
- (3) heroku create app-name
- (4) heroku addons:create heroku-postgresql
- (5) heroku config
- (6) Add url to .env
```DATABASE_URL=heroku url```

- (7) knex migrate:latest --env production
	- -runs the latest migration to heroku
- (8) knex seed:run --env production
	- runs the latest seed to your production
- (9) git push heroku master
	- push master branch to heroku
- (10) heroku open
