# Mean Stack Resources

Helpful links, processes, and architecture notes for the MEAN stack.

### Key Workflow & Concepts

  1. [Start build scripts First.](#1-build-scripts-gulp-or-grunt)
  2. [Define main client app and folder structure.](#2-client-app-setup)
  3. [Setup baseline API server with sessions/security middleware.](#3-api-setup)
  4. [Setup User and Config Data Contracts.](#4-user--config-data)
  5. [Establish data models for static and dynamic content.](#5-data-models)
  6. [Establish pub/sub channels and workers/queues.](#6-channels--workers)
  7. [Begin working through API endpoints, setup auto-managed references.](#7-api-endpoints)
  8. [Begin building client app to be used in multiple release environments.](#8-client-app-philosophy--roadmap)


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

### Load Testing Resources
  * [Blitz](https://www.blitz.io/) - Saas quick testing, the free tier is free and great at single node snapshots
  * [Siedge](http://www.nginxtips.com/nginx-benchmarking-using-siedge/) - More laborsome but its a free reliable solution
  * [Nginx Websocket Testing](https://www.nginx.com/blog/nginx-websockets-performance/) - Haven't tried this, but looks super promising for Websocket testing
  * [Raygun](https://raygun.io/) - Logger, super helpful

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

##### Channels

There are several wonderful pub/sub Saas products, many of which work well with the client/server. These are great for starting quickly and not having to maintain/build servers with the same functionality.

It is recommended that a Saas service be used unless the scale of the app reaches need for higher volume. 

Once this is the case, there are several things to be aware of:

  * Hosting pub/sub servers can become highly expensive when allowing for large concurrent connections. This is usually the largest point of failure.
  * Keep all key/value pairs abstract enough to allow for lower total subscriptions.
  * Build for latencies and fallbacks. Websockets do not run consistently across browsers. A good rule of thumb is keep messages to increments of 200ms, any faster and things could start to fail.
  * Use polling for extreme fallbacks only. This can drastically increase performance especially if the request stops the user from continuing through an action.

##### Workers

Keep long processes outside of your request time with worker processes. See [zeromq](http://zeromq.org/) along with [haproxy](http://www.haproxy.org/), this can be setup to run a distributed queue for managing laborsome read/write tasks.
Workers should handle any request that has multiple writes or needs to be manipulated in some way. Redis is a great simple data store, 

Another great use case is using workers to send push notifications to the different providers (APNS, GCM).


### 7. API Endpoints

The best way for both client/server to develop is through an automated system of endpoints with data requirements. Swagger, a tool for API documentation, can be setup for taking all data models/endpoints and generating a functional UI for testing. This is especially useful when creating new endpoints and communicating them with the client side developer.

### 8. Client App Philosophy & Roadmap

##### Philosophy

The client side core logic is the most important thing to keep separate. If done properly, client side code can be a separate package that can be re-used within each client distribution profile.

##### Roadmap

In an ideal world, a platform can be built once and then distributed everywhere to any device. 

The easiest way to accomplish this with angular is to setup modules. The main app module will consist of core functionality that should act the same for any release. Each distribution will then consist of importing the core module, and performing override logic specific to the hardware.

Sample workflow: 

  1. Setup web app
  2. Create distribution build scripts that import core
  3. Create distribution project with minor tweaks separate from core
  4. Run full build script, packaging core and distributions into separate releases.
  5. Test & Deploy

  



