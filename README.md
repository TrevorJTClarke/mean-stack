# Mean Stack Resources

Helpful links, processes, and architecture notes for the MEAN stack.

### Key Workflow & Concepts

  1. Start build scripts First.
  2. Define main client app and folder structure.
  3. Setup baseline API server with sessions/security middleware.
  4. Setup User and Config Data Contracts.
  5. Establish data models for static and dynamic content.
  6. Establish pub/sub channels and workers/queues.
  7. Begin working through API endpoints, setup auto-managed references.
  8. Begin building client app to be used in multiple release environments.


### Helpful Resources

  * [Angularjs](https://code.angularjs.org/1.3.16/docs/api)
  * [Nodejs](https://nodejs.org/)
  * [Babeljs](https://babeljs.io/) - ES Transpiler
  * [Sass](http://sass-lang.com/) - Sass Language (CSS Compiler)
  * [npm](https://www.npmjs.com/) - node package manager
  * [grunt cli](http://gruntjs.com/using-the-cli) - CLI tools for Grunt
  * [JSCS](http://jscs.info/) - JS Styleguide and linters
  * [Karma](http://karma-runner.github.io/0.13/index.html) - Test runner
  * [Mocha](http://mochajs.org/) - Unit testing
  * [Jasmine](jasmine.github.io/2.0/introduction.html) - Unit testing
  * [Scriptacular](http://scriptular.com/) - Regex Helper
  * [Yeoman](http://yeoman.io/) - Project generators
  * [Ionic](http://ionicframework.com/) - Hyrid Mobile with Cordova
  * [Electron](http://electron.atom.io/) - node + webkit
  * [Swagger](http://swagger.io/) - API Documentation
  * [SwaggerUI](https://github.com/swagger-api/swagger-ui) - API Documentation UI
  * [Postman](https://www.getpostman.com/) - Helpful API testing tool
  * [SocketIO](http://socket.io/) - pub/sub for nodejs


### 1. Build Scripts (Gulp or Grunt)

There are a few options for automating the client side dirty work. Keep in mind, each runner has strengths and weaknesses. Gulp has the best file/data overhead management, Grunt is the easiest to start/understand, Fly is cutting edge and works with the latest ecmascript.

  * [Gulp](http://gulpjs.com/) - The best cli/task runner, is the best choice for build tasks.
    * Most useful packages: gulp, gulp-sass, gulp-rename, gulp-uglify, gulp-concat, gulp-ng-templates, gulp-htmlmin, gulp-sourcemaps, browser-sync
  * [Grunt](http://gruntjs.com/) - The most popular runner, has the most support for many tasks.
    * Most useful packages: grunt-aws, grunt-contrib-concat, grunt-contrib-copy, grunt-contrib-jshint, grunt-contrib-uglify, grunt-contrib-sass, grunt-contrib-angular-templates, grunt-svgstore
  * [Fly](https://github.com/flyjs/fly) - The early version of the next big task runner, will be perfect if using ES6/ES7. (This is still very early in development)


### 2. Client App Setup

A quick start to setting up a project can be found on the yeoman site. These are great for initial project setup or simply testing out a type of project structure. 

While there are many great project setups, I have not found anything better than the below setup example. This is because most projects do not span multiple distribution channels.

##### Folder Structure

	/app
		/css
			/config
			/modules
			/pages
		/fonts
		/img
		/js
			/controllers
			/directives
			/filters
			/services
		/libs
		/templates
	/assets
	/config
	/releases
		/0.0.1
			/web
			/desktop
			/ios
			/android
	/reference
	/tasks
	/tests
		/js
			/controllers
			/directives
			/filters
			/services

With this setup, the tasks can manage files accourdingly and move/minify/test/etc to ensure a stable platform.

### 3. API Setup

The key to getting an API setup correctly is keeping modules as abstract as possible, allowing re-usability.

##### Folder Structure

	/0.0.1
		/auth
		/config
		/modules
		/routes
		/workers

The goal with this setup is to maintain backward compatibility for endpoints. Server instances can be routed traffic to specific versions of the codebase.

Setup of API should be focussed on establishing sessions and middleware that will affect all future routes. 

### 4. User & Config Data

Establishing User data as well as the baseline Configuration early on, will allow for easier integration. 

The key for the configuration data is for Environment scoped variables (such as API base endpoint, or environment specific keys), API headers, CDN variables, etc.

User data models work well if they are as similar as possible with both client/server. The best solution for this is to create a User class that returns data through methods. This way the data can be re-usable, can change in a single place, and provide easy helper methods for data getter/setters.
See [Backbonejs Model](http://backbonejs.org/docs/backbone.html#section-50), for a good example of this design.

### 5. Data Models

Similar to the User Data model, generic data should have a pre-defined model to follow. Follow the [DRY](http://www.amazon.com/gp/product/020161622X/ref=as_li_ss_tl?ie=UTF8&linkCode=as2&camp=1789&creative=390957&creativeASIN=020161622X) development flow, and create models for any models that are the foundation of the platform. 

A simple example:

You have a user, that owns projects.

	user: {
		id: 12354,
		projects: ["fdsa1234"]
	}
	
	projects: [{
		id: "fdsa1234",
		title: "Great Project"
	}]

With defined models, the User contract could define a simple helper method for returning associated project data. If done well, both client/server could utilize the same contracts.

### 6. Channels & Workers



### 7. API Endpoints



### 8. Client App Philosophy & Roadmap

