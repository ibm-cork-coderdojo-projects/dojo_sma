# [IBM Cork CoderDojo - Student Management Webapp (dojo_sma)](https://dojo-sma.mybluemix.net)

This is the source code repo for the on-going development of the IBM Cork CoderDojo Student Management Webapp (dojo_sma) for short, by Eric Moynihan and Michael O'Sullivan. Currently in rapid prototype phase.

This is a Node.js application, which uses the Express framework to implement a web-app on-top of the Node.js engine.

## Table of contents

* [Quick Start](#quick-start)
* [URL Endpoints for Views](#url-endpoints-for-views)
* [Directory Structure](#directory-structure)


## Quick Start

NOTE: ALL development should take place on the `development` Git branch, not `master` - i.e. `git push` should only push up to `development`. Pull requests will be required for merges of changes in the `development` branch, into the `master` branch.

To begin, you must have Node.js installed on your computer, as well as npm, the node package manager. Installing Node.js will install npm for you. Get the latest stable version of Node.js v6 from https://nodejs.org/en/

Then, to run the application locally for development, perform the following steps:

* Clone this repo: `git clone https://github.com/ibm-cork-coderdojo-projects/dojo_sma`
* `cd` into the cloned `dojo_sma` directory on your machine
* Install the required npm dependencies of the app: `npm install`
* Install the nodemon npm plugin globally: `npm install -g nodemon`
* Run `nodemon` to start the app running (this does an `npm start` behind the scenes)
* Open your web browser, and navigate to `http://localhost:3000` which will bring up the current index page, which will be the list of students.

Using `nodemon` to run the application instead of `npm start` will allow node to automatically detect changes in the application source code, and these will then be reflected immediately in your browser, without having to restart the app with npm manually after each change.

Alternatively, the app is running on IBM Bluemix as a Cloud Foundry application with the node.js buildpack. Have a look by navigating to https://dojo-sma.mybluemix.net in your browser.

## URL Endpoints for Views

The following are the routes used by the Express routing middleware (as specified in `routes/index.js`) which connect URLs accessed in the browser to the `controllers/students.js` controller, which in turn render the appropriate view from the `views` directory.

* `http://<domain>:<port>/` -> Index page - loads the `student-list.pug` view, which will show the list of all students.
* `http://<domain>:<port>/student` -> Student Details page - loads the `student-info.pug` view, which will show all the details of of a given student.
* `http://<domain>:<port>/student/add` -> Add New Student page - loads the `add-student-form.pug` view, which presents a form to be filled in when adding a new student (current form action goes nowhere).

For local development:

`<domain>` will be `localhost`, and `<port>` will be `3000`.

To view live on the IBM Bluemix Cloud:

`<domain>` will be `dojo-sma.mybluemix.net`, and `<port>` should not be specified.

## Directory Structure

When you clone the app, you will find the following files and directories:

```
app_server/
├── controllers/
│   ├── students.js
├── routes/
│   ├── index.js
│   └── users.js
├── views/
│   ├── add-student-form.pug
│   ├── error.pug
│   ├── index.pug
│   ├── layout.pug
│   ├── student-info.pug
│   └── student-list.pug
bin/
├── www
public/
├── fonts/
│   ├── FontAwesome.otf
│   ├── fontawesome-webfont.eot
│   ├── fontawesome-webfont.svg
│   ├── fontawesome-webfont.ttf
│   ├── fontawesome-webfont.woff
│   └── fontawesome-webfont.woff2
├── javascripts/
│   └── bootstrap.min.js
├── stylesheets/
│   ├── bootstrap.min.css
│   ├── font-awesome.min.css
│   └── style.css
```

The main source code for the app is divided up within the subdirectories of the `app_server` directory.

* `controllers` contains the Express controllers. This is where the business logic of the application is coded. Right now, there is only one controller, `students.js`, which handles the rendering of all the existing views of the application.
* `routes` containers the Express routing middleware files, which define what controllers should be called when different URL endpoints of the application are accessed in the browser. There are two files, `index.js`, and `users.js`. Only `index.js` is used at the moment.
* `views` contains the Jade/PUG layout templates that define the views of the application. All views extend `layout.pug`, which defines the HTML of the header and footer of all pages, as well as a placeholder container for the body of each page. The container holds only a PUG block, called `content`. This is where all the HTML defined in the other PUG view files is placed on each webpage of the app. The important views right now are `student-list.pug`, which is the index page of the app, showing the list of all students; `student-info.pug`, which shows all the detailed information of an individual student; and `add-student-form.pug`, which is the page containing a HTML form for adding new students. `error.pug` and `index.pug` are currently un-used.

Outside of `app_server` the other important folder is `public`, which contains all the static files used by the site, including the `fonts`, `javascripts`, and `stylesheets` directories. `fonts` includes font files used by FontAwesome. `javascripts` contains the main Bootstrap Javascript file. `stylesheets` contains CSS files used by FontAwesome, Bootstrap, and our own `style.css` file defining our own CSS for the app.

Finally, the `bin` folder contains one file, `www`, which contains all the Node.js configuration for the app, such as the default port it should listen on (3000). This should not have to be changed right now.