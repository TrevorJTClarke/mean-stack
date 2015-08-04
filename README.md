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
  * [Babeljs](https://babeljs.io/)
  * [Sass](http://sass-lang.com/)
  * [npm](https://www.npmjs.com/)
  * [grunt cli](http://gruntjs.com/using-the-cli)
  * [JSCS](http://jscs.info/)
  * [Regex Helper](http://scriptular.com/)
  * [Yeoman](http://yeoman.io/)
  * [Ionic](http://ionicframework.com/)
  * [Electron](http://electron.atom.io/)


### 1. Build Scripts (Gulp or Grunt)

There are a few options for automating the client side dirty work. Keep in mind, each runner has strengths and weaknesses. Gulp has the best file/data overhead management, Grunt is the easiest to start/understand, Fly is cutting edge and works with the latest ecmascript.

  * [Gulp](http://gulpjs.com/) - The best cli/task runner, is the best choice for build tasks.
    * Most useful packages: gulp, gulp-sass, gulp-rename, gulp-uglify, gulp-concat, gulp-ng-templates, gulp-htmlmin, gulp-sourcemaps, browser-sync
  * [Grunt](http://gruntjs.com/) - The most popular runner, has the most support for many tasks.
    * Most useful packages: grunt-aws, grunt-contrib-concat, grunt-contrib-copy, grunt-contrib-jshint, grunt-contrib-uglify, grunt-contrib-sass, grunt-contrib-angular-templates, grunt-svgstore
  * [Fly](https://github.com/flyjs/fly) - The early version of the next big task runner, will be perfect if using ES6/ES7. (This is still very early in development)


### 2. Client App Setup


### 3. API Setup


### 4. User & Config Data


### 5. Data Models


### 6. Channels & Workers


### 7. API Endpoints


### 7. Client App Philosophy & Roadmap


    